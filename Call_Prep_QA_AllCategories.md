# AP Supplier Portal — Call Prep: Expected Questions & Answers

## HighRadius Call — 13 March 2026, 4 PM

**Source:** Metapointer Proposals (01–05), Old Proposals (Doc1–Doc4), RFP, Functional & Non-Functional Requirements spreadsheet

---

## 1. PRODUCT (Prem)

### Q1: Walk us through the 42 wireframe gaps — how did you identify them?

**Answer:**
We performed a systematic analysis of the HighRadius User Journey wireframes (11 journey folders, 55+ screens) against the Product Backlog Requirements (PBR) spreadsheet and the RFP. The 42 gaps fall into 6 categories:

| Gap Category                     | Count        |
| -------------------------------- | ------------ |
| Missing / To-Be-Designed Screens | 10           |
| Validation Gaps                  | 12           |
| Logic Complexity Gaps            | 7            |
| Missing API Endpoints            | 3            |
| Technical Gaps                   | 9            |
| Workflow Gaps                    | 6            |
| **Total**                  | **42** |

Key point: HighRadius wireframes cover 19 of 29 screens (66%). The remaining 10 (34%) — all admin/manager/workflow screens — need to be designed from scratch. All supplier-facing transaction screens (Dashboard, PO List/Detail, Invoice List/Detail, PO Flip, Blank Invoice, Supplier Profile, Files Tab) ARE wireframed. We identified gaps by mapping every RFP requirement and PBR line item to a wireframe screen — anything without a wireframe or with incomplete specification is a gap.

All 42 gaps are fully accounted for in our estimation and delivery plan — no hidden costs, no surprise change requests.

---

### Q2: 10 of 29 screens (34%) are undesigned — who designs them?

**Answer:**
All 10 screens are designed during Sprint 0 (Weeks 1–2) in a dedicated design sprint. Our 3 Frontend Engineers handle UX design — they're senior React developers with G4 DSL experience who design and build.

The 10 screens to be designed (all admin/manager — supplier-facing screens are wireframed):

| #  | Screen                     | Persona          | Complexity |
| -- | -------------------------- | ---------------- | ---------- |
| 1  | Manager Dashboard          | Supplier Manager | High       |
| 2  | Screening Dashboard        | Supplier Manager | Medium     |
| 3  | Approval Worklist          | Supplier Manager | Medium     |
| 4  | Admin Settings             | Admin            | High       |
| 5  | User/Role Management       | Admin            | High       |
| 6  | Audit Trail                | Admin            | Medium     |
| 7  | Form Builder               | Admin            | High       |
| 8  | Workflow Configuration     | Admin            | High       |
| 9  | Notification Center        | Cross-cutting    | Medium     |
| 10 | Master Data Change Request | Supplier/Manager | Medium     |

The 19 wireframed screens (Supplier Dashboard, PO List/Detail, Invoice List/Detail, PO Flip, Blank Invoice, Registration 5-step, Supplier List, Invitation Modal, Supplier Profile, Files Tab) provide the UX foundation for all supplier-facing journeys. UX runs 1 sprint ahead of development throughout.

---

### Q3: How does the dynamic form builder work?

**Answer:**
The Form Builder (Admin screen #8, High complexity) allows tenant administrators to configure onboarding forms without code changes:

- **Field ordering**: Drag-and-drop arrangement of form fields per tenant
- **Validation rules**: Configure required/optional, format masks, regex patterns per field
- **Visibility conditions**: Show/hide fields based on supplier category, region, or other attributes
- **Multi-language labels**: i18n label management system (Technical Gap #3) — labels stored in a dedicated label store schema, cached in Redis
- **Reusable templates**: Save form configurations as templates; clone across tenants

This is one of our Logic Complexity Gap #2 — the wireframes show a static form layout, but actual implementation requires tenant-specific configuration, conditional logic, and multi-language support.

Backend: Form template definitions stored in the common schema (shared across tenants, read-only for tenant services). Redis caching ensures sub-second load times.

---

### Q4: What's the PO-flip flow for partial invoicing with tax/discount across multi-ERP?

**Answer:**
This is Logic Complexity Gap #4. The flow:

1. Supplier opens a PO in the portal (imported from SAP/Oracle/NetSuite via ERP adapter)
2. Clicks "Create Invoice" — enters the PO Flip screen
3. **Line-item selection**: Supplier selects which PO lines to invoice (can select 1 of N lines — partial invoicing)
4. **Auto-population**: Selected lines auto-populate invoice fields from PO data (quantities, unit prices, descriptions)
5. **Tax/discount lines**: Supplier adds tax lines and discount lines manually or via configured rules
6. **Multi-currency**: Invoice currency derived from PO; exchange rate applied if applicable
7. **Attachment inheritance**: Documents attached to PO are optionally carried forward to invoice
8. **Validation**: Field-level validation before submission — PO quantity bounds enforced ("Cannot exceed PO quantity" — Validation Gap #8), invoice amount reconciliation against PO total (Validation Gap #9)
9. **Submit**: Invoice syncs to AP system via Portal Invoice Creation agent

The ERP adapter pattern isolates SAP/Oracle/NetSuite-specific logic. Each ERP has its own adapter handling PO field mapping, status codes, and sync protocols. Dead-letter queue handles sync failures.

---

### Q5: Supplier deactivation after post-activation sanctions match — what's the workflow?

**Answer:**
This is Workflow Gap #4 — not shown in wireframes but required for compliance:

1. Supplier is already active and onboarded
2. A periodic re-screening job (or manual trigger via Screening retry API — Missing API #2) detects a new sanctions match (e.g., supplier added to OFAC list after activation)
3. System auto-deactivates the supplier — portal access revoked via Keycloak
4. Supplier Manager is notified with the screening failure details
5. Supplier is notified of deactivation with reason
6. Supplier Manager can initiate a review — if the match is a false positive, they can reactivate through the Supplier Approval workflow
7. All actions logged in the immutable audit trail

This ties into the RFP requirement for 100% screening coverage — not just at onboarding, but ongoing compliance monitoring.

---

### Q6: What does "25+ core features" mean? List them.

**Answer:**
Based on the RFP functional requirements spreadsheet (25 line items) and our proposal scope:

| #  | Feature                                  | Agent                   |
| -- | ---------------------------------------- | ----------------------- |
| 1  | Invite New Suppliers (individual)        | Supplier Onboarding     |
| 2  | Invite Existing Suppliers                | Supplier Onboarding     |
| 3  | Multi-Language Support for Forms         | Supplier Onboarding     |
| 4  | Configure Onboarding Forms (templates)   | Supplier Onboarding     |
| 5  | Submit Onboarding Form                   | Supplier Onboarding     |
| 6  | Supplier Onboarding Worklist             | Supplier Onboarding     |
| 7  | Bulk CSV Onboarding                      | Supplier Onboarding     |
| 8  | Draft Save & Resume                      | Supplier Onboarding     |
| 9  | Duplicate Supplier Detection             | Supplier Onboarding     |
| 10 | Address Verification                     | Supplier Screening      |
| 11 | TIN Validation                           | Supplier Screening      |
| 12 | Sanctions Screening (OFAC/EU/UN)         | Supplier Screening      |
| 13 | Real-time Screening Verification         | Supplier Screening      |
| 14 | Bank Account Details Verification        | Bank Account Validation |
| 15 | Real-time Bank Verification              | Bank Account Validation |
| 16 | Supplier Onboarding Approval Workflow    | Supplier Approval       |
| 17 | Master Data Change Request Workflow      | Supplier Approval       |
| 18 | Payment Method and Terms Update Workflow | Supplier Approval       |
| 19 | PO Import (single customer)              | Purchase Order          |
| 20 | PO Import across Multiple Customers      | Purchase Order          |
| 21 | PO Acknowledgement                       | Purchase Order          |
| 22 | PO Status Update to AP and ERP           | Purchase Order          |
| 23 | Manual Invoice Creation                  | Portal Invoice Creation |
| 24 | PO Flip to Invoice                       | Portal Invoice Creation |
| 25 | Sync Invoices to AP Applications         | Portal Invoice Creation |
| 26 | Supplier Manager Dashboard               | Cross-cutting           |
| 27 | Supplier Dashboard                       | Cross-cutting           |

These map 1:1 to the HighRadius PBR spreadsheet rows 2–25 plus 2 dashboard features.

---

### Q7: How do you handle invitation expiry, re-invite, and expired link UX?

**Answer:**
Workflow Gap #1. Our Sprint 0 design deliverable covers:

- **Expiry period**: Configurable per tenant (default: 7 days). Stored in invitation record with `expiry` timestamp.
- **Expired link handling**: Supplier clicks expired link → lands on a "Link Expired" page with clear messaging and a "Request New Invitation" button
- **Re-invite flow**: Supplier Manager can re-send invitation from the Supplier Onboarding Worklist — generates a new secure time-limited link. Previous link invalidated.
- **Auto-expiry notifications**: System sends reminder email at configurable intervals (e.g., 48 hours before expiry)
- **Audit**: All invitation send/expire/re-invite events logged

---

### Q8: What's included in the Validation Error State Library?

**Answer:**
Sprint 0 deliverable — all 12 validation types documented before Sprint 1:

| Type                          | UX Pattern                                         |
| ----------------------------- | -------------------------------------------------- |
| Email format                  | Inline error state below field                     |
| TIN format/checksum           | Real-time feedback indicator (green check / red X) |
| Bank account format           | Field-level error + toast notification             |
| Required field enforcement    | Visual asterisk indicator + submit blocking        |
| File type/size                | Error toast + list of supported formats            |
| Duplicate supplier detection  | Warning modal showing existing supplier match      |
| Approval chain completeness   | Pre-save validation + error summary panel          |
| PO quantity bounds            | Inline error: "Cannot exceed PO quantity"          |
| Invoice amount reconciliation | Warning banner when total deviates from PO         |
| Date range validation         | Inline date picker constraints                     |
| Session timeout/token expiry  | Modal overlay with re-login prompt                 |
| Concurrent edit conflict      | Toast notification + refresh prompt                |

The library includes: exact error message text, toast vs. inline vs. modal decision, colour/icon specifications per G4 DSL, screen-by-screen mapping, and i18n label keys for multi-language support.

---

### Q9: KPI target >90% onboarding completion — what if suppliers abandon registration?

**Answer:**
The >90% KPI measures "% of invitations resulting in completed registrations." Our design mitigates abandonment through:

- **Draft save & resume**: Auto-save every 30 seconds. Supplier can close and return later via the same link. Resume from last completed step.
- **5-step wizard with progress indicator**: Clear visual progress reduces dropout
- **Multi-language support**: Removes language barriers for international suppliers
- **Reminder emails**: Auto-send reminders at configurable intervals for incomplete registrations
- **Supplier Manager visibility**: Onboarding Worklist shows "Invited" vs "In Progress" vs "Completed" — manager can follow up on stalled registrations

If the 90% target isn't met, the root cause is typically: bad email addresses (bounced invitations) or suppliers who don't intend to complete onboarding. The KPI is measured excluding bounced/invalid invitations per the acceptance criteria framework.

---

### Q10: Invoice rejection and resubmission versioning?

**Answer:**
Workflow Gap #6. The flow:

1. Supplier submits invoice → syncs to AP via Portal Invoice Creation agent
2. AP team rejects invoice with a **rejection reason** (captured in a structured reason field — Rejection Reason Modal)
3. Supplier receives notification with rejection reason
4. Supplier creates a **new corrected invoice** (not editing the rejected one — rejected invoices are immutable)
5. New invoice links to the original via `parent_invoice_id` for version tracking
6. New invoice goes through the same validation and submission flow
7. All versions visible in Invoice Detail view with status history timeline

Key design decision: rejected invoices are NOT editable. A new invoice is created each time. This preserves the audit trail and prevents disputes about what was submitted vs. what was changed.

---

## 2. ENGINEERING / BACKEND (Priya)

### Q1: Why Spring Cloud Gateway? We have G4 API Gateway.

**Answer:**
Spring Cloud Gateway is proposed as a default based on the Spring Boot 3.x ecosystem alignment. However, this is subject to HighRadius's architecture decision. If G4 already provides an API Gateway with JWT validation, rate limiting, and tenant injection capabilities, we will integrate with it instead of deploying a separate gateway.

Sprint 0 architecture finalisation will confirm the gateway choice. Our API Gateway layer needs 4 capabilities:

1. JWT validation (Keycloak token verification)
2. Rate limiting and throttling
3. Tenant ID injection (from JWT claims into request context)
4. RBAC middleware (role-based route access)

If G4 Gateway supports all 4, we use G4. If not, we supplement with Spring Cloud Gateway or a lightweight filter chain.

---

### Q2: PostgreSQL OLAP — why OLAP for a transactional system?

**Answer:**
This is a labelling clarification. The portal is a transactional (OLTP) system. PostgreSQL is used as the primary transactional database. The "OLAP" reference in the proposal refers to the **read replica configuration** used for dashboard analytics queries — separating read-heavy dashboard/reporting queries from write-heavy transactional operations.

Architecture:

- **Primary**: PostgreSQL OLTP — handles all writes (supplier registration, invoice creation, approval workflows)
- **Read Replicas**: PostgreSQL read replicas serve dashboard queries, reporting, and analytics — preventing heavy reads from impacting transactional performance

This should be corrected in the document to avoid confusion.

---

### Q3: Schema-per-tenant — how does this scale to 1,100+ customers?

**Answer:**
Schema-per-tenant provides the strongest data isolation but requires careful scaling:

- **Schema creation**: Automated via tenant provisioning API (Technical Gap #4). New tenant = new schema + Flyway migration execution
- **Connection pooling**: Shared connection pool with tenant-aware routing. Each request's tenant_id (from JWT) determines which schema to target
- **Migration overhead**: Flyway tenant-aware migrations run per schema. For 1,100 tenants, migrations are parallelised with a configurable batch size
- **Monitoring**: Schema count, migration status, and per-tenant resource usage tracked via Prometheus/Grafana

Alternative considered: Row-level security (RLS) only with shared schema — simpler at scale but weaker isolation. We chose schema-per-tenant because:

1. HighRadius serves enterprise customers who demand physical data isolation
2. RLS is still applied as a defence-in-depth safety net
3. Schema-per-tenant allows per-tenant backup/restore and independent scaling

If HighRadius has a preferred multi-tenancy pattern for G4 applications, we will align in Sprint 0.

---

### Q4: 12 microservices across 6 domains — isn't that over-engineered for 66 APIs?

**Answer:**
The 12 services map cleanly to domain boundaries:

| Domain        | Services                                                   | APIs | Rationale                                                                             |
| ------------- | ---------------------------------------------------------- | ---- | ------------------------------------------------------------------------------------- |
| Onboarding    | Invitation Service, Registration Service, Draft Management | 12   | Invitation and registration have different lifecycles and scaling needs               |
| Compliance    | Screening Orchestrator, Bank Validation Adapter            | 10   | Screening orchestrates 4 parallel checks; bank validation is a separate external call |
| Approval      | Approval Workflow Engine, Master Data Change Service       | 14   | Workflow engine is reused across onboarding approval AND master data change           |
| PO            | PO Import Service, ERP Adapter                             | 10   | ERP adapter isolates SAP/Oracle/NetSuite specifics from PO business logic             |
| Invoice       | Invoice Creation Service, PO-Flip Engine, AP Sync Service  | 11   | PO-flip is complex enough to warrant separation; AP sync is async                     |
| Cross-cutting | Audit, Notification, Admin Config                          | 9    | Shared services used by all domains                                                   |

Average: ~5.5 APIs per service — reasonable service size. Not over-engineered — this is standard domain-driven design. Each service is independently deployable and scalable.

---

### Q5: How does bi-directional ERP sync conflict resolution work?

**Answer:**
Logic Complexity Gap #7. The pattern:

1. **PO Import** (ERP → Portal): PO data imported via ERP adapter. Each PO record has an `erp_version` field
2. **Status sync-back** (Portal → ERP): When supplier acknowledges/rejects PO, status syncs back to ERP
3. **Conflict detection**: Before sync-back, system checks if the ERP-side PO has been modified (version mismatch). If PO was updated in ERP while supplier was viewing it in portal, conflict is detected
4. **Resolution**: Conflict flagged to Supplier Manager. Options: force portal version, accept ERP version, or manual merge
5. **Retry queue**: Failed syncs go to a retry queue with exponential backoff (1s → 2s → 4s → 8s → max 5 minutes)
6. **Dead-letter queue**: After configurable max retries (default: 5), message moves to dead-letter queue for manual review
7. **Monitoring**: Dead-letter queue depth tracked as a KPI in Manager Dashboard

---

### Q6: Screening results retention is 7 years but audit log is 2 years — why different?

**Answer:**
Different retention periods serve different compliance requirements:

- **Screening results (7 years)**: Regulatory compliance — OFAC/sanctions screening results must be retained for audit and regulatory inquiry. If a regulator asks "was this supplier screened when you onboarded them 5 years ago?" — we need the evidence.
- **Audit log (2 years minimum)**: Per RFP mandate — operational audit trail for action tracking. The 2-year figure is the RFP minimum; actual retention can be configured higher per tenant.

Both are stored in immutable append-only tables. No UPDATE or DELETE operations permitted.

Note: The old proposal had "2-year retention" for everything. The Metapointer proposal upgraded screening/approval/PO/invoice to 7 years for compliance. This is a stronger position if HighRadius asks about SOX compliance.

---

### Q7: Circuit breaker config — threshold and fallback behaviour?

**Answer:**
All 7 external integrations use the same resilience pattern:

- **Circuit breaker threshold**: Opens after 5 consecutive failures or 50% failure rate in a 60-second window
- **Open state duration**: 30 seconds — no calls attempted, immediate fallback response
- **Half-open**: After 30s, allows 1 probe request. If succeeds, circuit closes. If fails, stays open for another 30 seconds
- **Fallback behaviour by integration**:

| Integration               | Fallback When Down                                                                                                                          |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| Screening APIs            | Queue screening request for retry; show "Screening Pending" status to user                                                                  |
| Bank Validation           | Queue for retry; block supplier activation until validated                                                                                  |
| ERP (SAP/Oracle/NetSuite) | Queue PO sync; show "Sync Pending" status; retry from queue when available                                                                  |
| Keycloak                  | Token refresh fails → force re-login; if Keycloak is fully down, portal is inaccessible (auth is mandatory)                                |
| Vault                     | Fallback to environment variables in dev/QA; in production, Vault downtime blocks new secret retrieval (existing cached secrets still work) |
| S3 Storage                | Upload queued for retry; user sees "Upload in progress"                                                                                     |
| Notifications             | Async delivery; failures stored in notification centre as fallback                                                                          |

All configurable via Spring Cloud CircuitBreaker + Resilience4j in Sprint 0.

---

### Q8: How do Flyway tenant-aware migrations work? What if migration fails on 1 tenant?

**Answer:**

- **Execution model**: On deployment, Flyway runs each migration script against every tenant schema sequentially. A migration runner iterates over the tenant registry and applies pending migrations per schema.
- **Failure handling**: If migration fails on tenant X:
  1. That tenant's migration is rolled back (each migration has a pre-written rollback script)
  2. Other tenants continue processing
  3. Failed tenant flagged in monitoring dashboard
  4. Alert triggered to operations team
  5. Tenant X remains on previous schema version — portal continues working with previous schema
  6. Fix applied and migration retried for tenant X only
- **Pre-production validation**: All migrations tested against a staging tenant before production rollout
- **Parallel execution**: For 1,100+ tenants, migrations can be parallelised in configurable batches (e.g., 50 at a time)

---

### Q9: Async job queue — why Redis instead of Kafka?

**Answer:**
Pragmatic choice based on the workload:

- **Redis-backed queue** (via Spring's `@Async` + Redis lists or Lettuce): Simpler to operate, already deployed for caching, sufficient for our job types (bulk CSV import, screening orchestration, ERP sync)
- **Kafka**: Better for high-throughput event streaming, but adds operational complexity (Zookeeper, partitions, consumer groups). Overkill for our use case — we're processing hundreds to low-thousands of jobs/day, not millions.

If HighRadius already runs Kafka in G4 infrastructure and prefers it, we can switch. The adapter pattern means the job queue implementation is swappable without changing business logic.

---

### Q10: Rollback strategy says <5 minutes — how is this tested?

**Answer:**

- **Pre-deployment checklist** (Release Gate #12 in Doc 04): Rollback procedure is tested and documented for every release
- **Testing method**: Before each production deploy, the rollback is executed in UAT:
  1. Deploy new version to UAT
  2. Run smoke tests
  3. Execute `helm rollback` to previous version
  4. Verify application health (health endpoints, smoke tests, data integrity)
  5. Time the rollback — must complete in <5 minutes
- **Database rollback**: Pre-written Flyway rollback migration tested alongside forward migration
- **Automated**: Kubernetes liveness probes detect unhealthy pods → auto-rollback to last known good state within 10 minutes without manual intervention

---

## 3. UI / FRONTEND (Priya)

### Q1: Why 3 separate SPAs instead of 1 SPA with role-based routing?

**Answer:**
The "3 persona-specific SPAs" reference means 3 application shells that share a common component library — NOT 3 entirely separate applications. Think of it as:

- 1 shared component library (G4 DSL + custom components)
- 3 entry points / route configurations per persona (Supplier, Manager, Admin)
- Shared build pipeline, shared codebase, shared state management

The benefit: each persona's bundle only includes the routes and components they need, reducing initial load time. A Supplier never downloads Admin or Manager code.

However, if HighRadius prefers a single SPA with role-based routing (which is simpler to maintain), we can implement that instead. This is a Sprint 0 architecture decision.

---

### Q2: How much of G4 DSL are you actually using vs custom?

**Answer:**
From our component inventory analysis:

| Category                            | Count             | Examples                                                                                             |
| ----------------------------------- | ----------------- | ---------------------------------------------------------------------------------------------------- |
| G4 OOB Components (reused directly) | ~15–20           | Grids, form controls, buttons, modals, navigation, tooltips, icons                                   |
| Custom Components (G4-extended)     | ~10               | Screening progress indicator, approval chain visualisation, PO-flip line mapper, dashboard KPI cards |
| Screen-level React Components       | 39                | Mapped to 29 screens (some screens have multiple component sections)                                 |
| Layout Definitions                  | 8                 | Page templates for list views, detail views, dashboards, admin config, forms                         |
| **Total**                     | **~72–77** |                                                                                                      |

Sprint 0 G4 OOB evaluation will confirm exactly which G4 components are reusable vs. which need custom builds. This is a critical Sprint 0 deliverable — we won't know the exact split until we evaluate the G4 component library hands-on.

---

### Q3: Virtual scrolling for 1,000+ rows — what library?

**Answer:**
Approach depends on G4 DSL:

- **If G4 provides a grid component** (likely based on AG Grid or similar): We use G4's built-in virtual scrolling
- **If G4 grid doesn't support virtual scrolling**: We use AG Grid Community or react-virtualized as a fallback
- **Performance target**: Grid load < 500ms for 1,000+ rows (validated by stress test every sprint)

Virtual scrolling renders only the visible rows in the DOM (typically 20–30 rows) and swaps content on scroll. This keeps DOM node count constant regardless of data size.

---

### Q4: WCAG 2.0 AA across 29 screens — automated or manual?

**Answer:**
Both. Per Doc 04 Quality Strategy:

- **Automated**: Lighthouse accessibility audit integrated into CI/CD. Runs per sprint. Catches: missing ARIA labels, colour contrast failures, keyboard trap issues, missing alt text
- **Manual**: QA engineer performs manual audit per screen — keyboard navigation, screen reader testing (NVDA/VoiceOver), focus management, modal accessibility, dynamic content announcements
- **Design-time**: G4 DSL components are expected to be AA-compliant by default. Custom components are built with ARIA tags and keyboard navigation from the start
- **Sprint 0**: Accessibility guidelines documented as part of the component library standards. Every PR review includes accessibility check.

Estimated effort: ~29 test cases (1 per screen), ~5 adjusted QA days (Doc 04 Section 12.1).

---

### Q5: Multi-language form labels — how does the i18n system work?

**Answer:**
Technical Gap #3. Architecture:

1. **Label store**: Dedicated PostgreSQL table in the common schema: `i18n_labels(key, locale, value)`
2. **Admin UI**: Part of the Form Builder — admin can add/edit labels per language per field
3. **Caching**: Labels cached in Redis with TTL. Cache invalidated when admin updates labels
4. **Frontend**: React i18n library (react-intl or i18next) loads labels on app init. Language selection stored in user preferences
5. **Fallback**: If a label is missing for a locale, fallback to English (en-US)
6. **Tenant-specific**: Labels can be overridden per tenant (tenant schema overrides common schema labels)

---

### Q6–10: Form Builder, WebSocket, Responsive, Concurrent Edit, Session Timeout

**Form Builder**: Custom build — no off-the-shelf form builder fits the tenant-configurable, multi-language, G4-styled requirements. Built as an Admin screen using React DnD (drag-and-drop) with a JSON schema backend. Forms stored as JSON definitions in the common schema.

**WebSocket (real-time notifications)**: Spring WebSocket + SockJS fallback. Each user subscribes to a tenant-specific + user-specific channel on login. Notifications pushed on: new approval task, screening complete, PO received, invoice status change. Notification Centre (Screen #10) shows history. If G4 has its own WebSocket infrastructure, we integrate with it.

**Responsive design**: Desktop-first. Breakpoints: 1024px (tablet), 1440px (desktop), 1920px (wide). Mobile is out of scope per RFP — portal is a desktop web application. Responsive within desktop/tablet range.

**Concurrent edit conflict detection** (Validation Gap #12): Optimistic locking. Each record has a `version` field. On save, if server version > client version, save is rejected with a toast: "This record was modified by another user. Please refresh." No data loss — user sees the conflict before overwriting.

**Session timeout** (Validation Gap #11): Keycloak token expiry triggers a modal overlay: "Your session has expired. Please log in again." Modal blocks all UI interaction. Re-login redirects back to the same page. Configurable token lifetime (default: 30 minutes with silent refresh).

---

## 4. QA (Vineeth)

### Q1: 1 QA engineer for ~800-900 test cases in 20 weeks — is that realistic?

**Answer:**
Yes, with the AI multiplier and ownership split:

- **Unit tests are NOT QA's responsibility** — developers write and maintain unit tests (Jest + JUnit). The 80% coverage mandate is enforced by CI/CD and is a developer delivery criterion.
- **QA focuses on**: E2E automation, integration testing, performance, security, regression
- **AI multiplier**: 1.40x on test script authoring reduces 148 raw QA days → 116 adjusted days
- **Automation-first**: Playwright with Page Object Model. Once a journey is automated, regression runs are zero-effort
- **Parallel streams**: Backend API testing overlaps with frontend testing (Weeks 6–11)

Breakdown:

| Test Type                           | Test Cases               | Adjusted Days      |
| ----------------------------------- | ------------------------ | ------------------ |
| Backend API (66 APIs)               | ~380                     | 20                 |
| Frontend Functional (29 screens)    | ~350                     | 20                 |
| E2E Journey Automation (6 journeys) | ~60                      | 13                 |
| Performance & Load                  | ~35                      | 7                  |
| Security & Pen Test                 | ~50                      | 9                  |
| Regression (Phase 1 + 2)            | ~870 (cumulative reruns) | 16                 |
| Tenant Isolation                    | ~30                      | 5                  |
| WCAG Accessibility                  | ~29                      | 5                  |
| UAT Support                         | —                       | 9                  |
| Test Plan & Reporting               | —                       | 12                 |
| **Total**                     | **~800–900**      | **116 days** |

116 days across 20 weeks = 5.8 days/week — tight but achievable for a senior QA engineer with AI-assisted test generation.

---

### Q2: Pen test — internal or third-party?

**Answer:**
**Internal first, third-party if HighRadius requires it:**

- Our QA engineer runs OWASP SAST + DAST scans using automated tools (configured in CI/CD)
- Manual penetration testing covers: JWT tampering, tenant_id manipulation, privilege escalation, cross-tenant access, SQL injection, XSS, CSRF
- HighRadius Infosec clearance (Dependency D9) requires their own security review — this may include their own pen test or a third-party audit. We support and remediate any findings.

If HighRadius mandates a third-party pen test, that's a HighRadius-owned activity. We provide full access and remediate all findings within SLA.

---

### Q3: Why Playwright over Cypress? We use Cypress.

**Answer:**
Playwright is our proposal but we explicitly noted "subject to HighRadius approval; fallback: Cypress/Selenium" (Doc 04, Section 1.3). We're flexible:

| Feature            | Playwright                | Cypress                                 |
| ------------------ | ------------------------- | --------------------------------------- |
| Multi-browser      | Chromium, Firefox, WebKit | Chromium, Firefox (WebKit experimental) |
| API testing        | Built-in                  | Requires plugins                        |
| Parallel execution | Native (4 workers)        | Requires Cypress Cloud (paid)           |
| CI/CD integration  | Native                    | Native                                  |

If HighRadius standardises on Cypress, we switch. The Page Object Model pattern is framework-agnostic — test logic stays the same.

---

### Q4: AI multiplier 1.40x on test scripts — what's the evidence?

**Answer:**
Conservative estimate based on actual developer experience with Claude Opus AI:

- **Test script generation**: AI generates ~70% of boilerplate test code (assertions, setup/teardown, API mocking). QA engineer reviews and customises. Time savings: ~30-40%
- **API test generation**: Given an OpenAPI/Swagger spec, AI generates positive + negative + boundary test cases. QA reviews and adds edge cases.
- **Defect documentation**: AI assists in writing reproduction steps, expected vs actual, and environment details from logs

The 1.40x means: a task that would take 10 days manually takes ~7 days with AI assistance. This is the same multiplier applied to developer unit test writing.

If the multiplier doesn't hold, the risk is mitigated by the fixed-price model — Metapointer absorbs the effort, not HighRadius.

---

### Q5: How do you test multi-tenant isolation at the DB level?

**Answer:**
Automated tenant isolation tests run every sprint (Doc 04, Release Gate #4):

1. **Cross-tenant query test**: Create data in Tenant A. Attempt to read from Tenant B context. Assert: empty result set, not an error — RLS silently blocks
2. **Tenant_id injection test**: Send API request without tenant_id in JWT. Assert: 401/403 rejection at gateway
3. **Tenant_id manipulation test**: Send API request with Tenant A's JWT but modify tenant_id claim to Tenant B. Assert: JWT validation fails (signature mismatch)
4. **Direct DB test**: Connect to PostgreSQL and attempt SELECT across schemas without tenant context. Assert: RLS policy blocks
5. **Middleware bypass test**: Call service layer directly (bypassing API Gateway). Assert: service-layer tenant_id check rejects

30 test cases, 5 adjusted QA days. These run in CI/CD on every merge to QA.

---

### Q6: 3% flaky test threshold — what happens to quarantined tests?

**Answer:**

- Tests exceeding 3% flakiness (fail >3 out of 100 runs without code change) are flagged
- Quarantined tests are moved to a separate Playwright test suite tag (`@quarantine`)
- Quarantine suite does NOT block CI/CD pipeline
- QA engineer has 1 sprint to investigate and fix the root cause (usually: timing issues, test data pollution, or WebSocket race conditions)
- Fixed tests move back to the main regression suite
- Tests quarantined for >2 sprints are escalated to sprint retrospective for team review

---

### Q7: Month-end simulation — what volume? What's "peak"?

**Answer:**
Based on the RFP context (HighRadius serves 1,100+ enterprises):

- **Concurrent users**: 1,000 (Doc 03, Section 8.1)
- **Transactions per hour**: 10,000 (Doc 03, Section 8.1) — mix of PO imports, invoice submissions, approval actions
- **Simulation scenario**: 8-hour sustained load mimicking month-end close: spike in invoice submissions, bulk PO imports from ERP, approval queue backlog processing
- **Pass criteria**: All APIs < 3s (P95), grid < 500ms, no pod restarts, no memory leaks, ERP sync queue stable (not growing unbounded), dead-letter queue empty
- **Tool**: Artillery 2.0 with custom scenarios

Specific volumes should be confirmed with HighRadius during Sprint 0 — they know their actual month-end peak patterns better than we do.

---

### Q8: Synthetic ERP data — how can you claim real-ERP readiness?

**Answer:**
We can't — and we don't claim it. The approach:

- **Dev/QA phase**: Synthetic data generated by Metapointer. Covers schema variations across SAP/Oracle/NetSuite PO/invoice structures. Tests adapter logic, field mapping, and error handling.
- **UAT phase**: Switch to **real ERP data** provided by HighRadius (Dependency D5). This is when actual SAP/Oracle/NetSuite integrations are validated end-to-end.
- **Gap**: If HighRadius provides ERP sample data late (risk flagged in Doc 01, D5), we extend synthetic testing but UAT is the real validation gate.

The adapter pattern means: if a real ERP returns different field names or edge cases not in our synthetic data, the fix is localised to the ERP adapter — no business logic changes needed.

---

### Q9: Automation coverage target at go-live?

**Answer:**

> = 95% regression automation by Phase 2 go-live (Doc 04, Section 10). Breakdown:

- Sprint-by-sprint: automation backlog maintained in Jira. Any test executed manually more than once is a candidate for automation.
- Phase 1 go-live: ~70-80% automation (focus on 4 agent journeys)
- Phase 2 go-live: >= 95% (full regression suite automated)
- No manual-only regression runs at production go-live

---

### Q10: OWASP SAST+DAST — which tools?

**Answer:**
Subject to HighRadius approval:

- **SAST**: SonarQube (or HighRadius-standard static analysis tool). Integrated into CI/CD — critical/high findings block merge.
- **DAST**: OWASP ZAP (or HighRadius-standard DAST tool). Run pre-UAT and pre-production.
- **Dependency scanning**: Snyk or OWASP Dependency Check for known vulnerabilities in third-party libraries

If HighRadius has mandated security tools (e.g., Checkmarx, Veracode, Fortify), we integrate with those instead.

---

## 5. PROJECT MANAGEMENT (Abu)

### Q1: You admit a 2-3 week slip — what's the mitigation?

**Answer:**
Doc 05 "Timeline Reality Assessment" — honest disclosure. Mitigation:

1. **Overlap frontend/backend streams**: FE and BE work in parallel across phases. While BE builds Phase 2 APIs (Sprints 6–7), FE can start Phase 2 screens using API stubs.
2. **Phase 1 MVP at Week 12**: This is firm — 4 agents in production. Phase 2 completion is where the 2–3 week buffer matters.
3. **AI productivity**: If the 1.30x-1.40x multiplier holds, the effective calendar time compresses
4. **Sprint 0 design sprint**: Getting all 10 screens designed upfront prevents design-wait delays during development sprints

Worst case: Phase 2 go-live at Week 22 instead of Week 20. Hypercare start shifts accordingly but total programme duration stays at ~6 months core + 6 months hypercare.

---

### Q2: Sprint 0 — 10 screen designs + architecture + DevOps in 2 weeks — feasible?

**Answer:**
Yes, because the team is 7 people working in parallel — and it's only 10 screens (down from initial estimate) since wireframe review confirmed 19 screens are already wireframed:

| Stream                         | Owner          | Sprint 0 Deliverable                                                                         |
| ------------------------------ | -------------- | -------------------------------------------------------------------------------------------- |
| Architecture + DB schema       | Architect/TL   | System design doc, data model, Flyway setup                                                  |
| DevOps/CI-CD                   | 1 BE engineer  | Pipeline setup, Docker/Helm, environment config                                              |
| G4 OOB evaluation              | 1 FE engineer  | Evaluate G4 components, document gaps, build component map                                   |
| 10 screen designs              | 2 FE engineers | ~5 screens each in 10 days = 2 days per screen (wireframe-level, not pixel-perfect)          |
| Keycloak + Vault setup         | 1 BE engineer  | Mock IAM layer, Vault integration or env-var fallback                                        |
| QA framework                   | QA engineer    | Playwright skeleton, test plan, test data design                                             |
| Validation Error State Library | PM + QA + FE   | Catalogue all 12 validation types with UX patterns                                           |

Key point: Sprint 0 screen designs are wireframe-level mockups for HighRadius review — not final pixel-perfect designs. The 19 wireframed screens from HighRadius give us a strong UX baseline for supplier-facing journeys. Detailed visual design continues 1 sprint ahead of development.

---

### Q3: No UX designer — who designs the 10 missing screens?

**Answer:**
Our 3 Frontend Engineers are senior full-stack React developers with UX capability. In a 7-person team, we don't have the luxury of a dedicated UX designer — but:

1. **G4 DSL provides the design system**: Colour palette, typography, spacing, component library, layout patterns are all defined. We're not designing from scratch — we're composing screens from G4 components.
2. **HighRadius wireframes provide 19 of 29 screens**: We follow the established patterns for the remaining 10.
3. **Weekly design reviews**: Every screen design is reviewed with HighRadius product team before development. They catch UX issues early.
4. **Dependency D6**: If HighRadius wants to provide their own UX designs for the 10 screens, we welcome it. The RFP asks us to design screens not covered in wireframes.

If this is a concern, we can propose a UX consultant for Sprint 0 (2 weeks) at additional cost.

---

### Q4: What if Keycloak isn't ready by Sprint 1?

**Answer:**
Dependency D1. Mitigation already planned:

- **Sprint 0**: Build a mock IAM layer that simulates Keycloak behaviour — issues JWT tokens with tenant_id and role claims, supports login/logout, returns user profiles
- **Sprints 1–5**: All development and QA uses the mock IAM layer. Frontend route guards, API Gateway JWT validation, and RBAC middleware all work against mock tokens.
- **Integration**: When Keycloak becomes available, we run a parallel integration sprint to switch from mock to real Keycloak. This is a configuration change (token issuer URL, client ID, public keys) — not a code change.
- **UAT gate**: Real Keycloak integration is mandatory for UAT entry (Doc 04, Phase 1 UAT entry criteria: "Login flow works for all 4 persona roles")

Estimated delay if Keycloak is never ready: Blocks UAT and production. Cannot go live without real authentication. Escalation path defined in RACI — HighRadius Engineering is accountable for Keycloak delivery.

---

### Q5: SPOC expectation — hours per week?

**Answer:**

- **Sprint 0**: ~8–10 hours/week (heavy design review, architecture alignment, dependency coordination)
- **Sprints 1–9**: ~4–6 hours/week (weekly status call, design reviews, sign-offs, ad-hoc questions)
- **UAT**: ~8–10 hours/week (UAT coordination, defect triage, acceptance testing)
- **Hypercare**: ~2 hours/week (status review, incident response coordination)

SPOC should have authority to:

- Approve/reject UX designs within 5 business days
- Prioritise defect fixes (P1/P2 vs P3/P4)
- Escalate dependency blockers internally at HighRadius
- Make product requirement decisions without committee approval for minor items

---

### Q6: Hypercare 0.5 FTE — who specifically?

**Answer:**
Rotating across team members based on issue type:

- **Frontend issues**: 1 of 3 FE engineers on rotation (2-month shifts)
- **Backend/integration issues**: 1 of 2 BE engineers on rotation
- **QA regression**: QA engineer runs regression after hotfixes
- **Coordination**: PM handles status updates and HighRadius communication

0.5 FTE = approximately 2.5 days/week of dedicated support capacity. P1 incidents get immediate response regardless of rotation schedule.

Named individuals assigned at the start of hypercare. Handover between rotation shifts includes: open issues, monitoring dashboard walkthrough, and runbook review.

---

### Q7: Design changes after sign-off — "one revision included" — then what?

**Answer:**
Per Doc 05 Section 6.2:

- **Sprint 0 design sprint**: We design 10 screens (admin/manager). HighRadius reviews and provides feedback.
- **One revision round included**: We incorporate HighRadius feedback and produce revised designs. This revision is within the fixed price.
- **Additional revisions**: Require a Change Request. Impact assessment (scope, timeline, cost) provided within 3 business days. No work begins until written approval.
- **Post-sign-off changes**: If HighRadius approves a screen design and later wants changes after development has started, this is a formal Change Request regardless of revision count.

This protects both parties: HighRadius gets a free revision round (covers normal feedback), but scope creep through endless design iterations is managed.

---

### Q8: Weekly PVA reporting — what tool/format?

**Answer:**

- **Tool**: Jira dashboards + manual report
- **Format**: Structured report delivered every Monday via email:
  - Sprint velocity (story points completed vs planned)
  - Backlog burn-down chart
  - Sprint goal achievement %
  - Scope variance tracking (features added/removed vs baseline)
  - Dependency status (D1–D10 traffic lights)
  - Risk log updates
  - Blockers and decisions needed
- **Live dashboard**: Jira board accessible to HighRadius SPOC at all times

---

### Q9: Escalation Level 2 — 2 business days too slow?

**Answer:**
2 business days is the maximum response time, not the target:

- **Level 1** (Metapointer PM): Resolved within 1 business day — covers most issues
- **Level 2** (HighRadius SPOC): Response within 2 business days — for cross-team or dependency issues
- **Level 3** (Steering Committee): Resolution within 5 business days — strategic decisions only
- **Emergency path**: P1 production incidents bypass ALL levels — direct page to on-call engineer + immediate HighRadius notification. Response within 2 hours.

If HighRadius wants faster escalation SLAs (e.g., 1 business day for Level 2), we can accommodate — it depends on their SPOC's availability commitment.

---

### Q10: Formal handover checklist?

**Answer:**
Phase 2 Go-Live + Handover (Milestone M5) includes:

| #  | Deliverable                  | Format                                                                                  |
| -- | ---------------------------- | --------------------------------------------------------------------------------------- |
| 1  | Source code                  | GIT repository (all branches, tags, commit history)                                     |
| 2  | CI/CD pipeline configuration | Docker/Helm charts, pipeline YAML, environment configs                                  |
| 3  | API documentation            | OpenAPI/Swagger specs for all 66 APIs                                                   |
| 4  | Architecture documentation   | System design doc, data model, integration architecture                                 |
| 5  | Deployment guides            | Step-by-step production deployment runbook                                              |
| 6  | Runbooks                     | Incident response, rollback procedures, monitoring playbook                             |
| 7  | Test suite                   | Full Playwright E2E suite, API test suite, performance test scripts                     |
| 8  | Knowledge transfer sessions  | 3–5 structured sessions covering architecture, deployment, operations, troubleshooting |
| 9  | Admin guide                  | Form builder, workflow configuration, user management, audit trail                      |
| 10 | MASC evidence pack           | UAT sign-off, live customer confirmation, KPI achievement evidence                      |

HighRadius Engineering sign-off required on each deliverable. No Milestone M5 payment without signed handover acceptance.

---

## 6. SECURITY & COMPLIANCE (Priya + Vineeth)

### Q1: Infosec clearance — when do you submit? What's in the package?

**Answer:**

- **When**: Submit during QA phase (Sprint 5 for Phase 1, Sprint 9 for Phase 2) — parallel track so clearance doesn't block go-live (Dependency D9)
- **Package includes**: Architecture security review document, OWASP SAST/DAST scan reports (zero critical/high), pen test results, RBAC/ABAC matrix validation evidence, tenant isolation test results, encryption configuration (TLS 1.3, AES-256), Vault integration evidence, CSP header configuration
- **HighRadius process**: Their cybersecurity team reviews and issues Infosec certificate. Required before every production deployment. No exceptions.

---

### Q2: 5-layer enforcement chain — example request flow

**Answer:**
Example: Supplier tries to view their PO list.

1. **Frontend (Layer 1)**: Route guard checks JWT role claim = "Supplier". PO List route is visible. "Admin Settings" link is hidden.
2. **API Gateway (Layer 2)**: Request hits `/api/v1/purchase-orders`. Gateway validates JWT signature, checks expiry, extracts `role=Supplier` and `tenant_id=T42` from claims. RBAC middleware confirms Supplier role can access `/purchase-orders`. Rate limiter checks request count.
3. **Service Layer (Layer 3)**: PO Service receives request with tenant context. ABAC check confirms: this supplier (user_id=U123) can only see POs assigned to their supplier_id. Query filter: `WHERE tenant_id = 'T42' AND supplier_id = 'U123'`
4. **Database (Layer 4)**: Query executes against `tenant_t42` schema. PostgreSQL RLS policy independently enforces `tenant_id = 'T42'` — even if service layer had a bug, RLS prevents cross-tenant data.
5. **Audit (Layer 5)**: Access decision logged: `{actor: U123, action: VIEW, entity: PO_LIST, tenant: T42, outcome: ALLOW, timestamp, ip_address}`

If any layer fails, request is rejected. Layers are independent — a bug in Layer 3 doesn't compromise Layer 4.

---

### Q3: CSP headers — what policy?

**Answer:**
Content Security Policy configured to prevent XSS and data injection:

```
Content-Security-Policy:
  default-src 'self';
  script-src 'self';
  style-src 'self' 'unsafe-inline' (for G4 DSL if needed);
  img-src 'self' data: blob:;
  connect-src 'self' wss: (for WebSocket);
  frame-ancestors 'none';
  form-action 'self';
```

- No inline scripts (`'unsafe-inline'` not allowed for scripts)
- No external script loading
- WebSocket connections allowed for real-time notifications
- Frame-ancestors 'none' prevents clickjacking
- Adjusted during Sprint 0 based on G4 platform requirements (G4 may need additional sources)

---

### Q4: Virus scanning — ClamAV or S3 native?

**Answer:**
Technical Gap #2. Decision made in Sprint 0:

- **Option A**: S3-native scanning if HighRadius S3-compatible storage supports it (e.g., AWS S3 with Macie/GuardDuty)
- **Option B**: ClamAV integration — upload goes to a quarantine bucket, ClamAV scans, clean files moved to permanent storage, infected files quarantined with alert
- **Fallback**: File type whitelist (PDF, DOC, DOCX, XLS, XLSX, PNG, JPG only) + file size limit (configurable, default 10MB) as a first line of defence regardless of scanning option

---

### Q5: SOX/GDPR — what specifically do you implement?

**Answer:**

- **SOX compliance support**: Immutable audit trail (no UPDATE/DELETE on audit log), approval workflow with segregation of duties (approver != requestor), version tracking on all financial records (invoices, POs), 7-year retention for financial data
- **GDPR support**: Right to data export (supplier can download their data), data retention policies (configurable per tenant), consent tracking for data collection, no personal data in logs (masked in structured logging), data isolation via schema-per-tenant

Note: We implement the technical controls. Actual SOX/GDPR certification is HighRadius's responsibility as the data controller. We provide the tooling.

---

## 7. COMMERCIAL & LEGAL (Swetha + Abu)

### Q1: Where's the pricing? Doc 01 says "see Document 6."

**Answer:**
Document 6 (Commercial & Legal / Contract MSA) is a separate deliverable not included in the 5 proposal documents. It contains: full pricing breakdown, payment schedule, legal terms, IP ownership, liability, confidentiality, and SLA commitments.

[Abu — need to confirm if Doc 6 is ready and share it before the call or if pricing will be discussed separately]

---

### Q2: Hourly rate behind the fixed price?

**Answer:**
We don't disclose hourly rates in a fixed-price model — that's the point of fixed pricing. HighRadius pays for outcomes (7 agents, 29 screens, 66 APIs delivered to acceptance criteria), not hours.

If pressed: the fixed price is derived from bottom-up estimation (screen × complexity × days, adjusted for AI productivity), not a rate card × hours calculation.

---

### Q3: 10-15% scope variance — how do you measure %?

**Answer:**
Variance is measured by effort impact, not raw counts:

- Baseline: Agreed SOW (7 agents, 29 screens, 66 APIs, 25+ features)
- A change that adds 2 simple screens (~4 days effort) out of a 116-day QA plan = ~3.4% variance — within tolerance
- A change that adds a new agent (~3-4 weeks effort) = clearly >15% — requires CR
- Measurement: PM tracks cumulative variance in weekly PVA report. When approaching 10%, PM alerts HighRadius SPOC.

---

### Q4: IP ownership at handover?

**Answer:**
[To be confirmed in Document 6]. Standard position: all code, documentation, and deliverables created under this engagement are HighRadius property upon final payment. GIT repository with full commit history is handed over. Metapointer retains no proprietary rights to the delivered code.

---

### Q5: Penalties for missing milestones?

**Answer:**
[To be defined in Document 6]. The milestone payment structure (30-20-15-20-10-5) inherently protects HighRadius — no payment without delivery acceptance. If a milestone is late, payment is simply deferred until the milestone criteria are met.

---

*Document prepared: 13 March 2026*
*Source: Metapointer Proposals 01–05, Old Proposals Doc1–Doc4, RFP, Functional & NFR Requirements*
