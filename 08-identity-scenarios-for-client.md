# Supplier Portal — Identity Scenarios & Architecture Options

**To:** HighRadius Product Team
**From:** Metapointer
**Date:** 2026-03-14

---

## Executive Summary

Adding the Supplier Portal means external users — suppliers — will log into a platform that currently serves only buyer teams. Before implementation, we need alignment on the identity scenarios the platform must handle.

We identified **9 scenarios** ranging from a single supplier submitting invoices to bidirectional trading between Fortune 5000 companies (e.g., Nvidia supplies GPUs to Walmart while Walmart provides logistics to Nvidia). All scenarios require one login per user, strict cross-tenant privacy, and a low-friction onboarding path.

Three architecture options are presented:

| Option      | Approach                                                                   | Infrastructure change | Whitelabel isolation           |
| ----------- | -------------------------------------------------------------------------- | --------------------- | ------------------------------ |
| **A** | Extend existing shared Keycloak realm                                      | None                  | Cosmetic (theme + domain)      |
| **B** | Separate realm per whitelabel customer, migrate to shared realm on upgrade | Medium                | True (separate user directory) |
| **C** | Central Hub realm + product-specific realms                                | High                  | Cosmetic (themed per tenant)   |

All three handle all 9 scenarios. The choice depends on how HighRadius views whitelabel isolation and how much infrastructure change is acceptable.

**We need decisions on:**

1. Whether whitelabel requires true infrastructure isolation or cosmetic branding is sufficient
2. Which scenarios must work at launch vs. later phases
3. Expected bulk onboarding volume (largest day-one supplier upload)

---

## Characters Used in This Document

| Name           | Company | Role                                                   |
| -------------- | ------- | ------------------------------------------------------ |
| Raj_Supplier   | Bosch   | Supplier contact — submits invoices, acknowledges POs |
| Lisa_APManager | Nvidia  | AP Manager — approves invoices, manages vendors       |
| Mike_APManager | Walmart | AP Manager — approves invoices, manages vendors       |

- **Nvidia** and **Walmart** are HighRadius customers (buyers)
- **Bosch** is a supplier — not a HighRadius customer

---

## Scenarios

### 1. Single-Buyer Supplier

Bosch supplies auto parts to Nvidia. Nvidia's AP team invites Raj.

```
Raj_Supplier@bosch.com  →  Nvidia Supplier Portal
                              Submit invoices, acknowledge POs, track payments
```

---

### 2. Multi-Buyer Supplier

Bosch supplies both Nvidia and Walmart. Raj logs in once and picks which buyer's portal to work in.

Nvidia cannot see that Bosch also supplies Walmart. Walmart cannot see that Bosch supplies Nvidia.

```
Raj_Supplier@bosch.com  →  Workspace picker
                              ├── Nvidia Supplier Portal
                              └── Walmart Supplier Portal

Nvidia and Walmart have no visibility into each other.
```

---

### 3. Customer Who Is Also a Supplier

Nvidia is a HighRadius customer. Nvidia also supplies GPUs to Walmart (also a HighRadius customer).

```
Lisa_APManager@nvidia.com  →  Workspace picker
                                 ├── Nvidia — Accounts Payable (AP Manager)
                                 │     Approves invoices, manages Nvidia's vendors
                                 │
                                 └── Walmart — Supplier Portal (Invoice Submitter)
                                       Submits GPU invoices to Walmart
```

One login. Both workspaces on her home screen. Permissions scoped per workspace.

---

### 4. Bidirectional Trading

Nvidia supplies GPUs to Walmart. Walmart supplies logistics to Nvidia. Both are HighRadius customers. Both are each other's supplier.

```
Lisa_APManager@nvidia.com              Mike_APManager@walmart.com
  ├── Nvidia AP (buyer)                  ├── Walmart AP (buyer)
  │   Reviews Walmart's logistics        │   Reviews Nvidia's GPU
  │   invoice                            │   invoice
  │                                      │
  └── Walmart Supplier Portal            └── Nvidia Supplier Portal
      Submits GPU invoice                    Submits logistics invoice
      to Walmart                             to Nvidia
```

Common among Fortune 5000 companies. Buyer-supplier is a directional relationship per tenant, not a label on the company.

---

### 5. Graduated Onboarding

Nvidia invites Bosch as a supplier. Raj receives an email with a one-time link.

```
Day 1   Click link → portal access, no password needed
        Complete company profile, upload documents

Day 2+  Set password on next visit

Day 8+  MFA required going forward
```

Low friction at entry, security tightens over time.

---

### 6. Supplier Becomes a Customer

Bosch has been supplying Nvidia for two years. Bosch now purchases HighRadius AP Automation.

Raj should not need a new account.

```
Before:  Raj_Supplier@bosch.com  →  Nvidia Supplier Portal

After:   Raj_Supplier@bosch.com  →  Workspace picker
                                       ├── Bosch — Accounts Payable (NEW)
                                       └── Nvidia — Supplier Portal (existing)
```

---

### 7. Whitelabel

Nvidia wants suppliers to see Nvidia branding — logo, colors, custom domain (suppliers.nvidia.com). Walmart wants the same. Suppliers don't see HighRadius.

```
suppliers.nvidia.com             suppliers.walmart.com
┌──────────────────────┐         ┌──────────────────────┐
│  [Nvidia Logo]       │         │  [Walmart Logo]      │
│  Supplier Portal     │         │  Supplier Portal     │
│  Email: [_________]  │         │  Email: [_________]  │
│  [Sign In]           │         │  [Sign In]           │
└──────────────────────┘         └──────────────────────┘
```

Same infrastructure, different skin per tenant.

---

### 8. Whitelabel Supplier Upgrades to HighRadius Customer

Bosch has been using Nvidia's whitelabeled portal (suppliers.nvidia.com). Bosch now purchases HighRadius AP Automation directly.

In options where whitelabel runs on a separate realm, Bosch's users are **migrated** from the whitelabel realm into the HighRadius shared realm. Credentials (password, MFA) are transferred — Raj doesn't need to re-register or reset anything.

```
Before:  Raj_Supplier@bosch.com  →  suppliers.nvidia.com (Nvidia's whitelabel realm)

During:  Bosch users exported from Nvidia whitelabel realm
         → imported into HighRadius shared realm (credentials intact)
         → Nvidia's whitelabel portal configured to accept shared realm tokens

After:   Raj_Supplier@bosch.com  →  Workspace picker (shared realm)
                                       ├── Bosch — Accounts Payable (NEW)
                                       └── Nvidia — Supplier Portal (existing, same access)

Raj's login credentials unchanged. One account, one realm.
```

---

### 9. Bulk Onboarding

Walmart goes live and uploads 2,000 suppliers on day one. Each supplier has 1-5 contacts — up to 10,000 invitations in one batch. ~3,000 users may click through on day one. Existing tenants must not be affected.

---

## Architecture Options

### Option A — Extend the Shared Realm

Add Supplier Portal as a new feature flag in the existing Keycloak realm. Suppliers join the same user directory as buyers. Whitelabel is cosmetic — per-tenant themes and custom domains, same underlying realm.

```
Existing Keycloak shared realm
  ├── AP, Treasury, AR users (unchanged)
  └── Supplier Portal (new feature flag)
        Suppliers in same realm
        Magic link for onboarding, MFA for regular use
        Per-tenant login themes for whitelabel
        Roles scoped to user + tenant
```

| Scenario                  | How it works                                                 |
| ------------------------- | ------------------------------------------------------------ |
| 1. Single-buyer supplier  | New user, one tenant context                                 |
| 2. Multi-buyer supplier   | Same user, multiple tenant contexts, workspace picker        |
| 3. Customer + supplier    | Same user, buyer role on own tenant + supplier role on other |
| 4. Bidirectional trading  | Symmetric — both sides have buyer + supplier contexts       |
| 5. Graduated onboarding   | Conditional auth flow: magic link → password → MFA         |
| 6. Supplier → customer   | Add buyer context. No new account.                           |
| 7. Whitelabel             | Keycloak client theme + custom domain. Cosmetic only.        |
| 8. Whitelabel → customer | Already in shared realm. Add buyer context. No migration.    |
| 9. Bulk onboarding        | Async user creation, rate-limited invitations                |

**Pros:**

- Zero infrastructure change — extends existing realm with a feature flag
- No migration needed — whitelabel suppliers already in the shared realm
- One realm, one user directory, simplest to operate
- No Identity Brokering or cross-realm SSO required

**Cons:**

- Whitelabel is cosmetic — supplier users exist in HighRadius infrastructure regardless of branding
- Supplier volume (potentially millions) in the same directory as buyer users
- Supplier and buyer auth flows share one realm, separated by conditional logic only
- Shared realm breach exposes all user types

---

### Option B — Whitelabel Realms + Migration on Upgrade

Whitelabeled portals get their own Keycloak realm. Suppliers exist only in the whitelabel realm. When a supplier company purchases HighRadius products, their users are **migrated** from the whitelabel realm into the shared realm (credentials intact). The whitelabel portal is configured to accept shared realm tokens so supplier access continues uninterrupted.

```
Phase 1: Bosch is a supplier only
  Nvidia Whitelabel Realm                HighRadius Shared Realm
    Raj_Supplier@bosch.com                 (Bosch not here yet)
    (supplier access to Nvidia)

Phase 2: Bosch buys HighRadius AP
  Nvidia Whitelabel Realm                HighRadius Shared Realm
    (Bosch users removed)        ──▶       Raj_Supplier@bosch.com
                                           ├── Bosch AP (buyer)
  Nvidia whitelabel portal now             └── Nvidia Supplier Portal
  accepts shared realm tokens                  (same access, new realm)
```

| Scenario                  | How it works                                                             |
| ------------------------- | ------------------------------------------------------------------------ |
| 1. Single-buyer supplier  | User in buyer's whitelabel realm                                         |
| 2. Multi-buyer supplier   | User in each buyer's whitelabel realm (separate accounts)                |
| 3. Customer + supplier    | User in shared realm with buyer + supplier contexts                      |
| 4. Bidirectional trading  | Both parties in shared realm with symmetric contexts                     |
| 5. Graduated onboarding   | Magic link into whitelabel realm, MFA after grace period                 |
| 6. Supplier → customer   | Migrate users from whitelabel realm to shared realm                      |
| 7. Whitelabel             | True isolation — separate realm, separate user directory, fully branded |
| 8. Whitelabel → customer | Migrate to shared realm. Credentials transferred. No re-registration.    |
| 9. Bulk onboarding        | Users created in whitelabel realm, isolated from shared realm            |

**Pros:**

- True whitelabel isolation — suppliers don't exist in HighRadius infrastructure until they upgrade
- Buyer can tell suppliers "this is our system" — it genuinely is at the infrastructure level
- Supplier volume isolated per buyer realm — shared directory stays lean
- Breach in one whitelabel realm doesn't expose other buyers or internal users
- No ongoing cross-realm SSO — migration is a one-time event, not a permanent link
- After migration, user has one account in one realm — simple to manage

**Cons:**

- Multi-buyer supplier has separate accounts in separate whitelabel realms before migration
- Migration is a planned operation — needs coordination (export users, configure portal trust, remove from whitelabel realm)
- One realm per whitelabel customer — realm count scales with customer base
- Whitelabel portals need to accept tokens from both their own realm and the shared realm (post-migration)

---

### Option C — Hub Realm + Product Realms

Central Hub realm for identity only. Each product (AP, Supplier Portal) gets its own realm. Users log into Hub once, SSO into product realms. Whitelabel handled via themed Supplier Portal realm clients.

```
Hub Realm (identity only)
  ├── SSO → AP Realm
  ├── SSO → Supplier Portal Realm (per-tenant themes for whitelabel)
  └── SSO → Treasury, AR Realms (future)
```

| Scenario                  | How it works                                                      |
| ------------------------- | ----------------------------------------------------------------- |
| 1. Single-buyer supplier  | Hub account + Supplier Portal realm session                       |
| 2. Multi-buyer supplier   | Hub account + Supplier Portal realm session, tenant picker        |
| 3. Customer + supplier    | Hub account + AP realm + Supplier Portal realm sessions           |
| 4. Bidirectional trading  | Symmetric — Hub identity, sessions in both product realms        |
| 5. Graduated onboarding   | Magic link into Supplier Portal realm, Hub account auto-created   |
| 6. Supplier → customer   | Hub identity exists. Grant AP realm access.                       |
| 7. Whitelabel             | Per-tenant theme on Supplier Portal realm client                  |
| 8. Whitelabel → customer | Hub identity already exists. Add AP realm access.                 |
| 9. Bulk onboarding        | Users created in Hub + Supplier Portal realm, AP realm unaffected |

**Pros:**

- Each product has its own security boundary, auth policies, and audit trail
- "Supplier → customer" is seamless — Hub identity already exists
- Scales to new products — Treasury, AR, Cash App each get a realm
- Fixed realm count — whitelabel handled via themes, not additional realms

**Cons:**

- Largest infrastructure change — new Hub realm, existing shared realm migrated to AP realm
- Three realms minimum (Hub + AP + Supplier Portal) from day one
- Identity Brokering required between Hub and all product realms
- Whitelabel is themed, not truly isolated — suppliers exist in the Supplier Portal realm

---

## Comparison

| Factor                    | A (Shared Realm) | B (Whitelabel Realms)             | C (Hub + Product Realms) |
| ------------------------- | ---------------- | --------------------------------- | ------------------------ |
| Infrastructure change     | None             | Medium                            | High                     |
| Whitelabel isolation      | Cosmetic         | True                              | Cosmetic                 |
| Multi-buyer supplier UX   | Single account   | Multiple accounts (pre-migration) | Single account           |
| Supplier → customer path | Add context      | Migrate to shared realm           | Add realm access         |
| Realm count               | 1 (existing)     | 1 + N whitelabel                  | 3+ (Hub, AP, Supplier)   |
| Operational complexity    | Low              | High (scales with customers)      | Medium (fixed count)     |
| Identity Brokering        | Not needed       | Not needed (migration instead)    | Required                 |
| Breach blast radius       | All users        | One buyer's realm                 | One product's realm      |

---
