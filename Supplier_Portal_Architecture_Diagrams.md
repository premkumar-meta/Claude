# SUPPLIER PORTAL — ENTERPRISE ARCHITECTURE & FLOW DOCUMENTATION

| Field | Detail |
|-------|--------|
| Document Type | Architecture & Flow Documentation |
| Version | 2.0 |
| Date | February 28, 2026 |
| Client | HighRadius Corporation |
| Project | AP Supplier Portal |
| Classification | PROPOSAL-READY / ARCHITECTURE-REVIEW READY |

> **Source Context:** RFP (2 pages), Enterprise Proposal v3.3 (1341 lines), 10 Batches of Wireframe Analysis (51 screens, 66 observations), 7 Agents, 3 Personas, 29 Screens + 11 Modals, 66 APIs

> **Mermaid Source Files:** All diagrams are stored as `.mmd` files in the `mermaid/` folder for rendering via Mermaid Live Editor, CLI, or any compatible tool. The E2E Process Flow has been exported to image.

---

## TABLE OF CONTENTS

1. End-to-End Process Flow (Mermaid — exported to image)
2. System Architecture (5-Layer Stack)
3. Microservice Interaction — Onboarding Sequence
4. Microservice Interaction — PO-to-Invoice Sequence
5. Agent Automation Trigger Map
6. Event-Driven Integration Mapping
7. Security & IAM Flow (5-Layer Enforcement)
8. Multi-Tenant Data Isolation
9. Phase-Based Delivery Roadmap
10. Error Handling & Rejection Loops
11. Decision Point Matrix
12. Status Lifecycle State Machines
13. Screen-to-Agent-to-API Mapping

---

## 1. END-TO-END PROCESS FLOW

**Mermaid file:** `mermaid/01_e2e_process_flow.mmd` (exported to image)

This is the master lifecycle diagram covering the complete supplier journey from invitation through payment, grouped into Phase 1 (Onboarding & Compliance) and Phase 2 (Transactional Enablement). All 7 agents, 6 decision points, and both invoice creation paths (PO-flip + manual) are represented.

See exported image for the rendered flow.

---

## 2. SYSTEM ARCHITECTURE (5-Layer Stack)

**Mermaid file:** `mermaid/02_system_architecture.mmd`

### Architecture Overview

The system follows a modular, layered architecture designed for HighRadius's NFRs: sub-3s API responses, 100% multi-tenant data isolation, containerized G4 deployment, and Keycloak-based authentication.

### Layer Breakdown

| Layer | Technology | Components | Responsibility |
|-------|-----------|------------|----------------|
| **Presentation** | React 18.x + G4 DSL | 3 persona-specific SPAs sharing a common component library | Responsive UI, WCAG 2.0 AA, virtual scrolling (1000+ rows), role-based route guards |
| **API Gateway** | Spring Cloud Gateway | JWT Validator, Rate Limiter, Tenant Injector, RBAC Middleware | Every request passes 4 sequential gates. No request reaches business logic without valid JWT + tenant context + role match |
| **Service** | Spring Boot 3.x | 12 microservices across 4 domains | Stateless, horizontally scalable, independently deployable. 66 APIs total |
| **Integration** | Adapter Pattern + Resilience4j | 6 adapters wrapping external systems | Circuit breaker, exponential retry, dead-letter queue per integration |
| **Data** | PostgreSQL OLAP + Redis | Schema-per-tenant DB, Redis cache + job queue | 100% tenant isolation via RLS, 2-year immutable audit logs |

### Service Domain Organization (12 Microservices, 66 APIs)

**Onboarding Domain (3 services)**
| Service | APIs | Key Responsibilities |
|---------|------|---------------------|
| Invitation Service | 12 | Generate secure links, send invitations (individual + bulk CSV), duplicate detection, tenant-scoped invitation records |
| Registration Service | (shared with above) | Dynamic form config per tenant, 5-step wizard, auto-save draft/resume, field validation, multi-language labels |
| Document Service | (shared) | Upload to S3, virus scanning (ClamAV), file metadata, auto-conversion (.xlsx → .pdf), auto-classification (Generated vs Supporting) |

**Compliance Domain (2 services)**
| Service | APIs | Key Responsibilities |
|---------|------|---------------------|
| Screening Orchestrator | 7 (3 HR + 1 orch) | Fan out 4 parallel checks (address, TIN, sanctions, bank), aggregate pass/fail, retry on timeout, circuit breaker per check |
| Approval Engine | 8 | Multi-level configurable workflows, conditional routing (spend/region/category), SLA tracking + auto-escalation, Keycloak user creation on final approval |

**Transactional Domain (3 services)**
| Service | APIs | Key Responsibilities |
|---------|------|---------------------|
| PO Service | 10 (1 HR) | ERP PO import (batch), line item parsing, acknowledge/reject processing, bidirectional ERP sync, bulk acknowledgment |
| Invoice Service | 11 (1 HR) | PO-flip auto-population, manual blank draft, partial invoicing (line selection), field validation, invoice PDF generation, AP sync |
| Master Data Service | 6 | Detect changed fields, determine approval requirement, route to workflow, apply changes on approval, trigger re-screening if needed |

**Cross-Cutting Services (4 services)**
| Service | APIs | Key Responsibilities |
|---------|------|---------------------|
| Notification Service | (part of 9) | Email dispatch via Redis job queue, WebSocket real-time push, invitation/confirmation/alert emails |
| Audit Service | (part of 9) | Immutable append-only log, every allow/deny decision, 2-year retention, CSV/PDF export for compliance |
| Dashboard Service | (part of 9) | KPI aggregation for supplier + manager dashboards, invoice pipeline metrics, financial summary |
| Admin Config Service | (part of 9) | Form builder config, workflow definition management, screening settings, tenant settings, i18n labels |

### API Ownership Summary

| Category | Count | Description |
|----------|-------|-------------|
| Vendor Build (Full) | 58 | End-to-end vendor ownership — design, implement, test, deploy |
| Integrate (HR Service) | 7 | HighRadius-owned backend services — vendor builds adapter only |
| Vendor Build (Orchestration) | 1 | Screening Orchestrator coordinating 3 HR services + bank validation |
| **Total** | **66** | |

---

## 3. MICROSERVICE INTERACTION — ONBOARDING SEQUENCE

**Mermaid file:** `mermaid/03_onboarding_sequence.mmd`

The onboarding flow executes in 4 sequential phases, each with distinct service ownership:

### Phase 1: Invitation (Supplier Manager → System)

| Step | Actor | Service | API | Action |
|------|-------|---------|-----|--------|
| 1 | Supplier Manager | UI | — | Click "+ Add Supplier" on Supplier List |
| 2 | Supplier Manager | UI | — | Fill Invitation E-Form: Name, Email, ERP/Company (AOPS001), Category (C-Supplier) |
| 3 | System | API Gateway | — | Validate JWT + RBAC (SupplierManager role) + inject tenant_id |
| 4 | System | Invitation Service | `POST /api/v1/invitations` | Check duplicate (email + tenant). If found → 409 Conflict + Warning Modal |
| 5 | System | Invitation Service | — | INSERT invitation record (status: PENDING) |
| 6 | System | Notification Service | — | Queue email job in Redis → dispatch invitation email with secure time-limited link |
| 7 | Supplier | Email | — | Receives email from noreply@qas.com with "Proceed To Complete Vendor Registration" link |

### Phase 2: Registration (Supplier → System)

| Step | Actor | Service | API | Action |
|------|-------|---------|-----|--------|
| 8 | Supplier | UI | — | Click email link → load registration form |
| 9 | System | Registration Service | `GET /api/v1/registration/{token}` | Validate token (not expired, not used), load invitation data + tenant form config |
| 10 | Supplier | UI | — | Form pre-filled: Name (James Doe), Email (james.doe@nike.com), Operating Unit (AOPS001) |
| 11 | Supplier | Registration Service | `PUT /api/v1/registration/{id}/step/{n}` | Fill each of 5 steps — auto-save via UPSERT on each step ("Last auto-saved at 10:42 AM") |
| 12 | Supplier | Document Service | `POST /api/v1/documents/upload` | Upload documents (drag-drop/browse) → S3 storage + virus scan |
| 13 | Supplier | Registration Service | `POST /api/v1/registration/{id}/submit` | Check certification checkbox → submit → validate all 5 steps → UPDATE status → SUBMITTED |
| 14 | System | Notification Service | — | Send confirmation email ("Application Submitted Successfully") |

### Phase 3: Automated Screening (System — No Human Involvement)

| Step | Service | External API | Action |
|------|---------|-------------|--------|
| 15 | Screening Orchestrator | — | Receive REGISTRATION_SUBMITTED event, create screening record (IN_PROGRESS) |
| 16 | Screening Orchestrator | Address API (HR) | `POST /screen/address` — verify billing + remittance addresses |
| 17 | Screening Orchestrator | TIN API (HR) | `POST /screen/tin` — validate TIN (21-GHTDRT, Corporation) |
| 18 | Screening Orchestrator | Sanctions API (HR) | `POST /screen/sanctions` — check OFAC/EU/UN lists |
| 19 | Screening Orchestrator | Bank API (HR) | `POST /validate/bank` — validate account (HP-347598, HSBC) |

Steps 16-19 execute **in parallel**. Each has an independent circuit breaker. Results:
- **All 4 pass** → status: PASSED → emit SCREENING_PASSED event → trigger approval
- **Any data error** → status: FAILED → notify supplier with actionable error → supplier corrects + resubmits
- **Sanctions match** → BLOCKED → requires manual manager review
- **Service timeout** → circuit breaker opens → retry queue (1s, 5s, 30s) → DLQ after 3 failures

### Phase 4: Approval & Activation (System + Supplier Manager)

| Step | Actor | Service | Action |
|------|-------|---------|--------|
| 20 | System | Approval Engine | Load workflow config (levels, routing rules, SLA), create level-1 approval request |
| 21 | System | Notification Service | Notify Level 1 Approver |
| 22 | Supplier Manager | Approval Engine | `GET /api/v1/approvals/pending` — view approval worklist |
| 23 | Supplier Manager | Approval Engine | `POST /api/v1/approvals/{id}/approve` — approve with comment |
| 24 | System | Approval Engine | Check if final level. If more levels → create next-level request + notify |
| 25 | System | Approval Engine | On final approval → UPDATE supplier status → ACTIVE |
| 26 | System | Keycloak IAM | Create Keycloak user with Supplier role + tenant scope |
| 27 | System | Notification Service | Send activation email with portal access link |

**Alternative flows at step 23:**
- **Reject** → capture reason in modal → notify supplier → supplier can correct + resubmit (re-enters screening)
- **Reassign** → route to different approver at same level
- **SLA breach** (no action within configured time) → auto-escalate to next approval level

---

## 4. MICROSERVICE INTERACTION — PO-TO-INVOICE SEQUENCE

**Mermaid file:** `mermaid/04_po_to_invoice_sequence.mmd`

### PO Import & Acknowledgment

| Step | Actor | Service | Action |
|------|-------|---------|--------|
| 1 | ERP (SAP/Oracle/NetSuite) | ERP Adapter → PO Service | Push PO data (scheduled batch). `POST /api/v1/po/import` |
| 2 | System | PO Service | UPSERT POs (status: ACK_PENDING), notify supplier ("3 New POs") |
| 3 | Supplier | PO Service | `GET /api/v1/po?status=all` — view PO List (8 POs: 5 pending, 3 acknowledged) |
| 4 | Supplier | PO Service | `GET /api/v1/po/PO-00181` — view PO Detail (Laptop $1,200 + Keyboard $150) |
| 5a | Supplier | PO Service | `POST /api/v1/po/PO-00181/acknowledge` — single acknowledge |
| 5b | Supplier | PO Service | `POST /api/v1/po/bulk-acknowledge` — bulk acknowledge (select 2+ POs → Actions → "Acknowledge Orders") |
| 6 | System | ERP Adapter | `POST /erp/po/{id}/ack-status` — sync acknowledgment back to ERP |
| 7 | System | Audit Service | Log acknowledgment action |

### PO-Flip: Create Invoice from Acknowledged PO

| Step | Actor | Service | Action |
|------|-------|---------|--------|
| 8 | Supplier | UI | Open Acknowledged PO (PO-00170) → click "Create Invoice" button |
| 9 | System | UI | Render "Select Lines to Create Invoice" modal with PO line items + checkboxes |
| 10 | Supplier | UI | Select Line 1 (Laptop Pro 15) → click "Create Invoice" |
| 11 | System | Invoice Service | `POST /api/v1/invoices/from-po` — pull PO billing, supplier, line data → INSERT invoice (DRAFT, auto-populated) |
| 12 | System | UI | Toast: "Invoice draft created" — render invoice detail with auto-filled fields |
| 13 | Supplier (optional) | Invoice Service | `POST /api/v1/invoices/{id}/add-po-lines` — add more PO lines via "Select PO Lines to add to Invoice" modal |
| 14 | Supplier | Invoice Service | `PUT /api/v1/invoices/{id}` — edit mode: fill Invoice No (INV-2025-003), adjust dates → save |

### File Attachment (Files Tab)

| Step | Actor | Service | Action |
|------|-------|---------|--------|
| 15 | Supplier | UI | Switch to Files Tab → click Upload |
| 16 | Supplier | Document Service | `POST /api/v1/invoices/{id}/files` — upload 3 files (browse/drag-drop) |
| 17 | System | Document Service | Store in S3 + virus scan, auto-classify (Generated vs Supporting), auto-convert .xlsx → .pdf for Invoice type |
| 18 | System | UI | Toast: "Files Uploaded Successfully" — grid shows files with tags, view/edit/download/delete actions |

**File classification rules:**
- **Generated** (cyan tag) = system auto-generated invoice PDF from invoice data
- **Supporting** (orange tag) = user-uploaded document
- **Type taxonomy:** Invoice, GRN (Goods Receipt Note), Others — editable via "Edit Description and Type" modal

### Submission & AP Sync

| Step | Actor | Service | Action |
|------|-------|---------|--------|
| 19 | Supplier | Invoice Service | `POST /api/v1/invoices/{id}/submit` — validate all required fields |
| 20 | System | Invoice Service | UPDATE status → SUBMITTED, generate invoice PDF (tag: Generated), sync to AP via ERP Adapter |
| 21 | System | Notification Service | Notify AP team of new invoice |
| 22 | System | UI | Toast: "Invoice Created Successfully" — status badge changes to SUBMITTED, all buttons removed (read-only) |

### Manual Invoice Path (Alternative to PO-Flip)

| Step | Actor | Action |
|------|-------|--------|
| 1 | Supplier | Click "+ Add Invoice" on Invoice List → blank draft created |
| 2 | Supplier | Edit mode: fill ALL fields (Bill-to, Ship-to, Invoice No, dates, Type, PO Number, etc.) |
| 3 | Supplier | Only Supplier section auto-populated from profile (Apex Systems, S-4321, TIN: 27-3216794) |
| 4 | Supplier | Can link to PO via Type=PO + PO Number dropdown (hybrid approach) |
| 5+ | Same | Save → attach files → submit (same flow as steps 15-22 above) |

**Both paths converge:** Draft → Edit → Save → Attach Files → Submit → Submitted (read-only)

---

## 5. AGENT AUTOMATION TRIGGER MAP

**Mermaid file:** `mermaid/05_agent_trigger_map.mmd`

### 7 Agents: Triggers, Execution, and Outputs

| # | Agent | Type | Trigger Event | What It Executes | Output / State Change | APIs | Phase |
|---|-------|------|---------------|-----------------|----------------------|------|-------|
| 1 | **Supplier Onboarding** | Automated | Manager clicks "Send Invitation" or uploads Bulk CSV | Generate secure link, load tenant form config, auto-save drafts per step, validate 5-step wizard, send confirmation email | Invitation sent, Supplier record SUBMITTED | 12 | 1 |
| 2 | **Supplier Screening** | Automated | Supplier clicks "Submit Registration" | Orchestrate 4 parallel checks: address (HR API), TIN (HR API), sanctions/OFAC (HR API). Aggregate pass/fail. Retry on timeout | Screening PASSED or FAILED | 7 (3 HR + 1 orch) | 1 |
| 3 | **Bank Account Validation** | Automated | Supplier clicks "Submit Registration" (runs parallel with Agent 2) | Validate bank ownership (HR API), verify account format, check ABA/routing, fraud scoring | Bank validation PASSED or FAILED | 3 (1 HR) | 1 |
| 4 | **Supplier Approval** | Assisted | All screening checks pass (SCREENING_PASSED event) | Load workflow config per tenant, route to correct level, conditional routing (spend/region/category), SLA tracking + auto-escalation, approve/reject/reassign. Create Keycloak user on final approval | Supplier ACTIVE or REJECTED | 8 | 1 |
| 5 | **Master Data Change** | Assisted | Supplier edits profile data | Detect changed fields, determine if approval required, route to workflow, apply on approval, trigger re-screening if bank/address changed | Master record updated or unchanged | 6 | 2 |
| 6 | **Purchase Order** | Automated | ERP pushes new PO data (scheduled); Supplier clicks Acknowledge/Reject | Ingest POs from multi-ERPs, parse line items + metadata, process ack/reject, sync status back to ERP, bulk acknowledgment | PO ACKNOWLEDGED or REJECTED | 10 (1 HR) | 2 |
| 7 | **Portal Invoice Creation** | Assisted | Supplier clicks "Create Invoice" (PO-flip) or "+ Add Invoice" (manual); then "Submit" | PO-flip: auto-populate from PO. Manual: blank draft. Partial invoicing via line selection. Field validation, file attachment + auto-classify, generate invoice PDF, sync to AP/ERP | Invoice DRAFT → SUBMITTED → AP Sync | 11 (1 HR) | 2 |

### Agent Chaining Pattern

```
Invitation (Agent 1)
  → Registration SUBMITTED
    → Screening (Agent 2) + Bank Validation (Agent 3) [parallel]
      → SCREENING_PASSED
        → Approval (Agent 4)
          → ACTIVE
            → PO Import (Agent 6) → Acknowledge → Invoice (Agent 7)
            → Profile Edit → Master Data Change (Agent 5)
```

Agents are decoupled via events — each can evolve independently. Automated agents (1, 2, 3, 6) run without human intervention. Assisted agents (4, 5, 7) automate the workflow around human decisions.

---

## 6. EVENT-DRIVEN INTEGRATION MAPPING

**Mermaid file:** (included in `02_system_architecture.mmd`)

### External System Integrations (7 HighRadius-Owned + 4 Infrastructure)

| External System | Protocol | Data Flow | Direction | Trigger | Fault Tolerance |
|----------------|----------|-----------|-----------|---------|-----------------|
| **Keycloak IAM** | OIDC/OAuth 2.0 | JWT tokens, user roles, tenant claims, SSO sessions | Bidirectional | Every request (JWT validation); on activation (user creation) | N/A — hard dependency, fail = 401 |
| **Address Screening API** | REST/HTTPS | Billing + remittance addresses → Pass/Fail + confidence | Request-Response | Registration submit | Circuit breaker (5 failures/60s), retry (1s, 5s, 30s), DLQ |
| **TIN Validation API** | REST/HTTPS | TIN (21-GHTDRT), classification type → Valid/Invalid | Request-Response | Registration submit | Same as above |
| **Sanctions Screening API** | REST/HTTPS | Supplier name + aliases → Match/No-Match + score (OFAC/EU/UN) | Request-Response | Registration submit | Same as above |
| **Bank Validation API** | REST/HTTPS | Account (HP-347598), Bank (HSBC), ABA, type → Validated/Failed | Request-Response | Registration submit | Same as above |
| **ERP Systems** (SAP/Oracle/NetSuite) | REST API | POs IN (batch import), Ack status OUT, Invoices OUT | Bidirectional | Scheduled (PO import) + Event-driven (ack sync, invoice submit) | Circuit breaker, retry, DLQ |
| **S3-Compatible Storage** | S3 API | Documents, generated PDFs | Read/Write | Upload, auto-generate PDF, download | Standard S3 resilience |
| **HashiCorp Vault** | Vault API | API keys, DB credentials, certificates, encryption keys | Read-only (runtime) | Application startup + credential rotation | HA Vault config |
| **Email Service** | SMTP/API | Invitation, confirmation, notification, alert emails | Outbound only | Event-driven via Redis job queue | Redis persistence, retry |
| **WebSocket Service** | WS/WSS | Real-time status updates, PO notifications, approval alerts | Push to client | Status changes, new PO arrival, approval decisions | Reconnection logic |

### Fault Tolerance Pattern (Applied to All External Integrations)

| Layer | Technology | Configuration | Behavior |
|-------|-----------|---------------|----------|
| Circuit Breaker | Resilience4j | Threshold: 5 failures in 60s, timeout: 10s per call | States: Closed → Open (reject all) → Half-Open (test single request) |
| Retry Queue | Redis-backed | Strategy: Exponential backoff. Max: 3 retries. Intervals: 1s, 5s, 30s | Failed calls requeued with increasing delay |
| Dead Letter Queue | Redis | After 3 retry failures | Alert ops team + notify affected user. Manual review required |

### Screening Orchestration Detail

The Screening Orchestrator is the **single orchestration API** in the system. On REGISTRATION_SUBMITTED:

1. Create screening record (status: IN_PROGRESS)
2. Fan out 4 parallel HTTP calls to HR-owned services
3. Each call has its own circuit breaker instance
4. Results collected asynchronously — partial results displayed as they arrive
5. Final aggregation: ALL 4 must pass → SCREENING_PASSED
6. Any failure → SCREENING_FAILED with per-check error details

---

## 7. SECURITY & IAM FLOW (5-Layer Enforcement)

**Mermaid file:** `mermaid/06_security_iam_flow.mmd`

### Defense-in-Depth: 5 Enforcement Layers

No single layer is trusted as the sole security boundary. Each layer adds independent verification.

| Layer | Enforcement Point | What It Checks | Failure Action |
|-------|-------------------|----------------|---------------|
| **1. Frontend** | React route guards + component visibility | Role → show/hide routes, buttons, tabs | Hidden UI elements; redirect to dashboard. **Not a security boundary** — UX optimization only |
| **2. API Gateway** | JWT validation + RBAC middleware | Token signature + expiry, tenant_id presence, role claim match | 401 Unauthorized (invalid token) or 403 Forbidden (missing role) |
| **3. Service Layer** | ABAC (Attribute-Based Access Control) engine | Ownership (resource.owner == user_id), status (action allowed in this state?), tenant (double-check scope) | 403 Forbidden with specific reason code |
| **4. Database** | PostgreSQL Row-Level Security (RLS) | `tenant_id = current_setting('app.tenant_id')` on every query | Query returns empty set — zero cross-tenant leakage even if middleware bypassed |
| **5. Audit** | Immutable append-only logging | Every allow/deny decision recorded | Audit trail for compliance. Fields: timestamp, user_id, tenant_id, action, resource, result, IP, user_agent |

### Persona-to-Screen Access Matrix

| Screen / Area | Supplier | Supplier Manager | Approver | Admin |
|--------------|----------|-----------------|----------|-------|
| Supplier Dashboard | Full (Own) | None | None | None |
| Manager Dashboard | None | Full | View | View |
| Supplier Registration Form | Full (Own) | None | None | None |
| Supplier List / Worklist | Own | Full | View | View |
| Screening Dashboard | None | Full | View | View |
| Approval Worklist | None | View | Full | View |
| PO List / PO Detail | Full (Own) | View | None | None |
| Invoice List / Invoice Detail | Full (Own) | View | None | None |
| Invoice Creation / PO Flip | Full (Own) | None | None | None |
| Supplier Profile | Full (Own) | View | None | View |
| Form Builder | None | None | None | Config |
| Workflow Configuration | None | None | None | Config |
| User/Role Management | None | None | None | Full |
| Audit Trail | None | View | None | Full |
| Notification Center | Full (Own) | Full (Own) | Full (Own) | Full |

### Button-Level Visibility Rules

| Button / Action | Supplier | Supplier Manager | Approver | Admin |
|----------------|----------|-----------------|----------|-------|
| Send Invitation | Hidden | Visible | Hidden | Visible |
| Bulk Upload (CSV) | Hidden | Visible | Hidden | Visible |
| Approve / Reject | Hidden | Hidden | Visible | Hidden |
| Reassign Approval | Hidden | Hidden | Visible | Visible |
| Create Invoice | Visible | Hidden | Hidden | Hidden |
| Acknowledge PO | Visible | Hidden | Hidden | Hidden |
| + Add Invoice | Visible | Hidden | Hidden | Hidden |
| Submit / Delete Invoice | Visible (Draft only) | Hidden | Hidden | Hidden |
| Configure Form Fields | Hidden | Hidden | Hidden | Visible |
| Export Audit Trail | Hidden | Visible | Hidden | Visible |
| Edit Profile | Visible | Hidden | Hidden | Hidden |

### ABAC Runtime Check Examples

| Scenario | Check | Result |
|----------|-------|--------|
| Supplier A tries to view Supplier B's invoices | Ownership: resource.supplier_id != ctx.user_supplier_id | 403 — Not resource owner |
| Supplier tries to delete a Submitted invoice | Status: DELETE not allowed when status != DRAFT | 403 — Action not allowed in this status |
| Tenant A user sends request with Tenant B resource ID | Tenant: resource.tenant_id != ctx.tenant_id | 403 — Cross-tenant access blocked |
| Manager tries to create an invoice | RBAC: /invoices/create requires SUPPLIER role | 403 — Insufficient permissions |

---

## 8. MULTI-TENANT DATA ISOLATION

**Mermaid file:** `mermaid/07_multitenant_isolation.mmd`

### 4-Mechanism Isolation (100% Data Isolation per RFP)

| Mechanism | Layer | How It Works |
|-----------|-------|-------------|
| **JWT Tenant Resolution** | API Gateway | Every request carries Keycloak-issued JWT with `tenant_id` claim. Gateway extracts before any business logic. No request proceeds without valid tenant context |
| **Schema-Per-Tenant** | Database | Each HighRadius customer gets isolated PostgreSQL schema (`tenant_a_schema`, `tenant_b_schema`). No shared tables for tenant-specific data |
| **Middleware Enforcement** | Service Layer | `TenantContextFilter` sets `SET LOCAL app.tenant_id = '{id}'` as PostgreSQL session variable + selects correct schema before every query |
| **Row-Level Security** | Database (Safety Net) | RLS policy: `USING (tenant_id = current_setting('app.tenant_id')::uuid)` + `WITH CHECK` for writes. Enforced even if middleware bypassed |

### Tenant-Scoped Resources

| Resource | Isolation Pattern |
|----------|------------------|
| PostgreSQL tables | Schema-per-tenant: `tenant_a_schema.suppliers`, `tenant_b_schema.suppliers` |
| Redis sessions | Key prefix: `session:{tenant_id}:{user_id}` |
| Redis config cache | Key prefix: `config:{tenant_id}:forms` |
| Redis job queue | Key prefix: `queue:{tenant_id}:screening` |
| S3 documents | Path prefix: `/{tenant_id}/suppliers/{supplier_id}/...` |
| Audit logs | Scoped per tenant schema, plus tenant_id column with RLS |

### Shared (Non-Tenant) Resources

| Resource | Location | Contents |
|----------|----------|----------|
| Form templates | `common_schema.form_templates` | Dynamic form field configurations (shared base, tenant overrides) |
| Workflow definitions | `common_schema.workflow_definitions` | Approval chain templates |
| i18n labels | `common_schema.i18n_labels` | Multi-language label translations |
| Tenant config | `common_schema.tenant_config` | Tenant metadata, feature flags |

### JWT Payload Structure (from Keycloak)

```json
{
  "sub": "user-uuid-123",
  "tenant_id": "TENANT-A",
  "roles": ["SUPPLIER"],
  "org": "AOPS001",
  "email": "james.doe@nike.com",
  "exp": 1740000000
}
```

---

## 9. PHASE-BASED DELIVERY ROADMAP

**Mermaid file:** `mermaid/09_delivery_gantt.mmd`

### Sprint-to-Agent Mapping

| Sprint | Weeks | Calendar Window | Agents | Screens | APIs | Key Milestones |
|--------|-------|----------------|--------|---------|------|----------------|
| Sprint 0 | 1-2 | Mar 2-13, 2026 | — | — | — | Architecture sign-off, CI/CD setup, G4 OOB eval, design sprint for 16 undesigned screens, DB schema v1, validation library |
| Sprint 1-2 | 3-6 | Mar 16 - Apr 10 | Onboarding + Screening | 6 + 3 | 12 + 7 | Invitation flow, 5-step registration, parallel screening checks |
| Sprint 3-4 | 7-10 | Apr 13 - May 8 | Bank Validation + Approval + Dashboards | 2 + 4 + 2 | 3 + 8 | Approval engine, SLA escalation, supplier + manager dashboards |
| Sprint 5 | 11-12 | May 11-22 | — | — | — | Integration testing, E2E: Invite → Register → Screen → Approve → Activate |
| UAT | 12-14 | May 22 - Jun 5 | — | — | — | Performance validation (API<3s, Grid<500ms), WCAG audit, UAT sign-off |
| **MVP Go-Live** | ~14 | **Mid-May 2026** | **4 agents live** | **17 screens** | **~40 APIs** | **1 live customer in production** |
| Sprint 6-7 | 13-16 | Jun 8 - Jul 3 | PO + Invoice | 5 + 5 | 10 + 11 | PO import/ack, PO-flip, manual invoice, file attachment, AP sync |
| Sprint 8-9 | 17-20 | Jul 6-31 | Master Data Change | 2 | 6 | Profile edit workflow, re-screening trigger, full regression, pen test |
| UAT 2 | 19-20 | Jul 20-31 | — | — | — | Full regression, virtual scrolling stress test, UAT feedback |
| **Full Go-Live** | ~20 | **Early July 2026** | **All 7 agents** | **29 + 11 screens** | **66 APIs** | **Full delivery + GIT handover + KT** |
| Hypercare | — | Jul 2026 - Jan 2027 | — | — | — | 0.5 FTE, production support, weekly updates |

### Team Allocation (7 FTE)

| Role | Count | Focus |
|------|-------|-------|
| Architect / Tech Lead | 1 | System design, G4 integration, code quality |
| Senior Backend Engineers | 2 | Microservices, APIs, database, DevOps |
| Frontend Engineers | 2 | UI with G4 DSL, responsive design, WCAG |
| QA Engineer | 1 | E2E automation, performance, security, WCAG testing |
| Project Manager | 1 | Timeline, stakeholder communication, PVA reporting |

Frontend and backend streams run in parallel. QA overlaps ~40% with active development sprints.

---

## 10. ERROR HANDLING & REJECTION LOOPS

**Mermaid file:** `mermaid/08_error_handling.mmd`

### Screening Failure Types

| Failure Type | Check | Behavior | Recovery Path |
|-------------|-------|----------|---------------|
| Address invalid | Address Verification | Block with actionable error — fields highlighted | Supplier corrects address → resubmit |
| TIN invalid | TIN Validation | Format/checksum error — correct format shown (XX-XXXXXX) | Supplier corrects TIN → resubmit |
| Sanctions match | Sanctions Screening | BLOCKED — manual review required | Manager reviews manually via Screening Dashboard |
| Bank invalid | Bank Validation | Ownership/format error | Supplier corrects bank details → resubmit |
| Service timeout | Any check | Circuit breaker opens → retry queued (1s, 5s, 30s) | After 3 failures → DLQ → ops alert + supplier notification |

### Approval Rejection Loop

| Action | Outcome | Next Step |
|--------|---------|-----------|
| Approve | Advance to next level (or activate if final) | Next approver notified; or Keycloak user created + supplier activated |
| Reject | Mandatory reason captured in modal | Supplier notified with reason — can correct data + resubmit (re-enters screening) |
| Reassign | Route to different approver at same level | New approver notified |
| No action (SLA breach) | Auto-escalate to next level | Next-level manager notified with escalation flag |

### Invoice Rejection Recovery

| Status | Supplier Actions Available | Recovery |
|--------|---------------------------|----------|
| Draft | Submit, Delete, Edit, Add Line Items, Upload Files | Full CRUD |
| Submitted | None (read-only) | Wait for AP processing |
| In Progress | None (read-only) | Wait for AP decision |
| **Rejected** | **None (read-only) — WORKFLOW GAP IDENTIFIED** | **Supplier must create NEW invoice (PO-flip or manual) referencing same PO** |
| Paid | None (terminal) | Lifecycle complete |
| Void | None (terminal) | Invoice cancelled |

> **Workflow Gap #6:** Wireframes confirm no "Resubmit" or "Edit" button on rejected invoices. This is documented in the proposal's 48-gap analysis. Recovery requires creating an entirely new invoice.

### Field-Level Validation (Two-Tier)

| Tier | Location | Checks | Failure UX |
|------|----------|--------|-----------|
| Client-side | React SPA | Required fields, format masks (TIN: XX-XXXXXX, phone: +1 (XXX) XXX-XXXX), date ranges | Inline error indicators + submit blocked |
| Server-side | Service Layer | Business rules, duplicate detection, amount reconciliation, cross-field validation | 422 response with field-level errors + toast notification |

---

## 11. DECISION POINT MATRIX

### All Decision Points Across the Portal

| ID | Decision | Actor | Location | Options | Outcome |
|----|----------|-------|----------|---------|---------|
| DP-1 | Invitation method | Supplier Manager | Supplier List | Individual / Bulk CSV | E-Form Modal or CSV upload + batch validation |
| DP-2 | Duplicate supplier? | System (auto) | Invitation Service | Duplicate found / No duplicate | Warning modal (override or cancel) / Proceed |
| DP-3 | Registration: save or submit? | Supplier | Registration Form | Auto-save draft / Submit | Persist draft (resume later) / Trigger screening |
| DP-4 | Screening result (per check x4) | System (auto) | Screening Orchestrator | All pass / Data error / Sanctions match / Timeout | Proceed to approval / Block + retry / Manual review / Circuit breaker |
| DP-5 | Approval decision (per level) | Approver (human) | Approval Worklist | Approve / Reject / Reassign | Next level or activate / Notify with reason / Route to other |
| DP-6 | Approval routing condition | System (auto) | Approval Engine | Spend > threshold / Region / Category | Senior approver / Regional manager / VP level |
| DP-7 | PO action | Supplier | PO Detail | Acknowledge / Reject / Bulk select | Status → Acknowledged (Create Invoice enabled) / Rejected (terminal) |
| DP-8 | Invoice creation method | Supplier | PO Detail or Invoice List | PO-flip / Manual / Hybrid | Auto-populate from PO / Blank draft / Manual + link to PO |
| DP-9 | Invoice line selection (PO-flip) | Supplier | Select Lines Modal | Partial (1 of N) / Full (all lines) | Partial invoicing / Full PO invoice |
| DP-10 | Profile change triggers re-approval? | System (auto) | Master Data Service | Bank changed / Address changed / Minor change | Re-screening + approval / Address re-verification / Auto-approve |

---

## 12. STATUS LIFECYCLE STATE MACHINES

### PO Status Lifecycle (4 states)

```
[ERP Import] → ACK_PENDING
                  ├── Supplier acknowledges → ACKNOWLEDGED → (all lines invoiced) → CLOSED
                  └── Supplier rejects    → REJECTED (terminal, read-only)
```

**CTA by status:** Ack Pending → "Acknowledge" button | Acknowledged → "Create Invoice" button | Rejected/Closed → no buttons

**Badge colors:** Ack Pending = orange | Acknowledged = green | Rejected = red | Closed = green

### Invoice Status Lifecycle (6 states)

```
[Created via PO-flip or Manual] → DRAFT
                                    ├── Supplier submits → SUBMITTED
                                    │                        └── AP processes → IN_PROGRESS
                                    │                                           ├── AP approves → PAID (terminal)
                                    │                                           ├── AP rejects  → REJECTED (read-only)
                                    │                                           └── AP voids    → VOID (terminal)
                                    └── Supplier deletes → (removed)
```

**CTA by status:** Draft → "Submit" + "Delete" | All others → no buttons (read-only)

**Badge colors:** Draft = orange | Submitted = orange | In Progress = green | Rejected = red | Paid = green | Void = grey

### Supplier Status Lifecycle (7 states)

```
[Invitation Sent] → INVITED → (supplier clicks link) → REGISTRATION_DRAFT
                                                          └── (submit) → SUBMITTED
                                                                          └── SCREENING_IN_PROGRESS
                                                                                ├── All pass → SCREENING_PASSED → APPROVAL_PENDING
                                                                                │                                    ├── Approved → ACTIVE
                                                                                │                                    └── Rejected → REJECTED
                                                                                └── Any fail → SCREENING_FAILED → (correct + retry) → SUBMITTED
```

**Supplier List badge colors:** Onboarded (green) | Invited (blue) | Inactive (grey)

**Left nav sub-statuses for Invited:** TIN Check, Bank Account Validation, Sanctions Screening, Need Review

---

## 13. SCREEN-TO-AGENT-TO-API MAPPING

| Agent | Phase | Type | Screens (from wireframes) | APIs | Wireframe Batches |
|-------|-------|------|--------------------------|------|-------------------|
| Supplier Onboarding | 1 | Automated | Supplier List, Invitation Modal, Email, Registration 5-Step, Success Toast | 12 | Batches 1-2 (Screens 1-10) |
| Supplier Screening | 1 | Automated | Screening Dashboard, Detail Popup (not in wireframes — to be designed) | 7 (3 HR + 1 orch) | Post-registration trigger |
| Bank Account Validation | 1 | Automated | Integrated with Screening flow | 3 (1 HR) | Registration Step 4 data |
| Supplier Approval | 1 | Assisted | Approval Worklist, Action Modal (not in wireframes — to be designed) | 8 | Post-screening trigger |
| Master Data Change | 2 | Assisted | Supplier Profile 5-tab view (Batch 9) | 6 | Batch 9 (Screen 39) |
| Purchase Order | 2 | Automated | PO List, PO Detail x4 statuses, Bulk Ack | 10 (1 HR) | Batches 4, 6, 8 (Screens 13-14, 19, 29-32) |
| Portal Invoice Creation | 2 | Assisted | Invoice List, Invoice Detail x6 statuses, PO-Flip flow, Manual flow, Files Tab | 11 (1 HR) | Batches 4-8, 10 (Screens 12, 16-28, 33-38, 40-51) |
| Cross-Cutting | Both | — | Dashboards (2), Notification Center, Audit Trail, Admin Config | 9 (1 HR) | Batch 3 (Screen 11) |
| **TOTAL** | | | **29 Screens + 11 Modals** | **66 APIs** | **51 wireframe screens captured across 10 batches** |

---

## MERMAID SOURCE FILES

All Mermaid diagrams are stored separately for rendering:

| File | Diagram | Best Rendered As |
|------|---------|------------------|
| `mermaid/01_e2e_process_flow.mmd` | End-to-End Process Flow | Flowchart (exported to image) |
| `mermaid/02_system_architecture.mmd` | System Architecture (5-Layer) | Flowchart |
| `mermaid/03_onboarding_sequence.mmd` | Onboarding Microservice Interaction | Sequence Diagram |
| `mermaid/04_po_to_invoice_sequence.mmd` | PO-to-Invoice Microservice Interaction | Sequence Diagram |
| `mermaid/05_agent_trigger_map.mmd` | Agent Automation Trigger Map | Flowchart |
| `mermaid/06_security_iam_flow.mmd` | Security & IAM (5-Layer Enforcement) | Flowchart |
| `mermaid/07_multitenant_isolation.mmd` | Multi-Tenant Data Isolation | Flowchart |
| `mermaid/08_error_handling.mmd` | Error Handling & Rejection Loops | Flowchart |
| `mermaid/09_delivery_gantt.mmd` | Delivery Roadmap | Gantt Chart |

> Render using: [Mermaid Live Editor](https://mermaid.live), `mmdc` CLI, or any Mermaid-compatible tool.

---

**Document End**

*Generated from: RFP (2 pages), Enterprise Proposal v3.3 (22 sections, 1341 lines), 10 Wireframe Batches (51 screens, 66 observations across 7 modules)*
