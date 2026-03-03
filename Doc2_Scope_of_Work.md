# AP SUPPLIER PORTAL — SCOPE OF WORK

| Field | Detail |
|-------|--------|
| **Document** | Scope of Work (SOW) |
| **Version** | 3.3 |
| **Date** | February 28, 2026 |
| **Client** | HighRadius Corporation |
| **Project** | AP Supplier Portal Development & Deployment |
| **Service Provider** | Metapointer |
| **Classification** | PROJECT-SPECIFIC |
| **Status** | READY FOR SUBMISSION |

> **Confidentiality Notice:** This document contains proprietary and confidential information. Distribution is restricted to authorized HighRadius and Metapointer personnel only.

> **Cross-References:**
> - Executive Summary & Business Understanding → *Proposal PDF document*
> - Solution Architecture & Security → *Tech Specs document*
> - Timeline, Milestones & Delivery Approach → *Timeline document*
> - Commercial Terms & Pricing → *Commercial Agreement document*

---

## Table of Contents

1. [Scope of Work](#1-scope-of-work)
   - 1.1 [In Scope](#11-in-scope)
     - Application Development & Quantified Deliverables
     - Screen & Workflow Estimation
     - Integrations
     - Testing & Quality Assurance
     - Post-Deployment Support
     - AI Productivity Enhancements
     - Responsibility Matrix (RACI)
     - API Ownership Mapping
     - UI Gap Analysis Summary
     - Frontend Component Inventory
   - 1.2 [Out of Scope](#12-out-of-scope)
2. [Solution Overview](#2-solution-overview)
   - 2.1 [Solution Vision](#21-solution-vision)
   - 2.2 [Capability Map](#22-capability-map)
   - 2.3 [Transformation Vision — From Current State to Future State](#23-transformation-vision--from-current-state-to-future-state)
   - 2.4 [High-Level Workflow](#24-high-level-workflow)
   - 2.5 [RFP Requirement Traceability](#25-rfp-requirement-traceability)
   - 2.6 [Persona Journeys](#26-persona-journeys)
3. [Non-Functional Requirements](#3-non-functional-requirements)
   - 3.1 [Availability](#31-availability)
   - 3.2 [Performance](#32-performance)
   - 3.3 [Scalability](#33-scalability)
   - 3.4 [Security](#34-security)
   - 3.5 [Compliance](#35-compliance)
   - 3.6 [Code Quality](#36-code-quality)

---

## 1. Scope of Work

**Classification: PROJECT-SPECIFIC**

### 1.1 In Scope

#### Application Development & Quantified Deliverables

**Supplier Portal Web Application** (responsive, modern UI for three personas):

- 29 application screens across Supplier Manager, Supplier, and HighRadius Admin/Client Admin personas
- 11 popup/modals for workflows and confirmations
- 66 APIs: 58 vendor-built, 7 integrations, 1 orchestration layer
- 25+ core features including: invitation-based onboarding, dynamic multi-language forms, document upload/validation, draft save/resume, real-time screening (TIN/address/sanctions/bank), configurable approval workflows, SLA-based escalation, PO import/sync, invoice creation, master data change workflows, manager dashboards
- Responsive design with WCAG 2.0 AA accessibility standards
- Virtual scrolling for grids with 1,000+ rows
- Integration of 91-page user journey wireframes

#### Screen & Workflow Estimation

**Portal Screens Breakdown (29 Total):**

| Workflow/Feature | Screens | Complexity | Est. Days/Screen | Total Person-Days |
|-----------------|---------|------------|-----------------|-------------------|
| Supplier Onboarding | 6 | High | 5 | 30 |
| Supplier Screening | 3 | Medium | 4.5 | 13.5 |
| Bank Validation | 2 | Medium | 4 | 8 |
| Approval Workflows | 4 | High | 5.5 | 22 |
| PO Management | 5 | High | 5 | 25 |
| Invoice Management | 5 | High | 5 | 25 |
| Master Data Management | 2 | Medium | 4.5 | 9 |
| Dashboards | 2 | High | 6 | 12 |

**Popup / Modal Screens (11 Total):**

| # | Modal/Popup | Parent Screen | Trigger | Key Actions |
|---|-----------|---------------|---------|-------------|
| 1 | Send Invitation Modal | Supplier List | "Add Supplier" button | Email input, validation, template selection, send |
| 2 | Bulk Upload Modal | Supplier List | "Bulk Upload" button | CSV upload, validation results, error summary |
| 3 | Duplicate Supplier Warning | Registration / Invitation | Duplicate detection | Show existing match, allow override or cancel |
| 4 | Screening Detail Popup | Screening Dashboard | Click screening result row | Full check results, pass/fail detail per check |
| 5 | Approval Action Modal | Approval Worklist | Approve/Reject/Reassign | Comment entry, action confirmation |
| 6 | Document Preview Modal | Document tabs | Click document | PDF/image preview, download option |
| 7 | Rejection Reason Modal | PO Detail / Invoice Detail | Reject action | Reason selection/free text, confirm reject |
| 8 | Invoice Line Item Editor | PO Flip Screen | Edit line item | Quantity, price, tax, discount adjustment |
| 9 | Workflow Configuration Preview | Admin Workflow Config | Preview button | Visual approval chain diagram |
| 10 | User Role Assignment Modal | User Management | Assign/change role | Role picker, tenant scope, confirm |
| 11 | Confirmation Dialog (Generic) | Multiple screens | Destructive actions | Confirm/cancel with context message |

Estimated effort: ~3 weeks for all popup/modal UI. Each also requires API calls and E2E test cases.

- **Modals & Pop-ups:** ~5 person-weeks
- **Screen Development:** ~29 person-weeks
- **Combined Frontend (Screens + Modals): ~34 person-weeks** → ~11 calendar weeks with 3 FE devs

**Workflow/Feature Development (Backend Services):**

| Agent/Service | Workflows | Est. Days/Workflow | Total Person-Days |
|---------------|-----------|-------------------|-------------------|
| Supplier Onboarding Agent | 3 | 15 | 45 |
| Supplier Screening Agent | 2 | 12.5 | 25 |
| Bank Validation Agent | 1 | 10 | 10 |
| Supplier Approval Agent | 2 | 17.5 | 35 |
| Master Data Approval Agent | 2 | 15 | 30 |
| Purchase Order Agent | 3 | 16 | 48 |
| Portal Invoice Agent | 3 | 16 | 48 |

- **Agent/Service Development Total: ~49 person-weeks** (delivered by 2 Senior Backend Engineers + Architect/Tech Lead contributing ~40% backend effort → ~16 calendar weeks)

**Effort Reconciliation with Timeline:**

| Stream | Gross Effort | Team | AI Multiplier | Calendar Weeks |
|--------|-------------|------|--------------|----------------|
| Frontend (Screens + Modals) | ~34 person-weeks | 3 FE Devs | 1.40x | ~15 weeks |
| Backend (Agent Services) | ~49 person-weeks | 2 BE + Architect (~40%) | 1.30x | ~16 weeks |
| QA (E2E, Perf, Security, RBAC) | ~28 person-weeks | 1 QA Engineer + Automation | — | ~17 weeks (parallel streams, overlaps with dev from Week 3) |

- All estimates are gross effort before AI productivity adjustment
- Unit tests (~11 weeks) are developer responsibility and included in FE/BE capacity, not QA
- QA 17-week calendar accommodates ~28 person-weeks through overlapping test streams (backend validation + frontend E2E run concurrently Weeks 6–11; performance + security overlap Weeks 13–15)
- QA execution begins Week 1 (setup/framework) and completes Week 17 (regression + release hardening), 3 weeks before program end for handover buffer
- Calendar alignment validated in the **Timeline document** and **QA Strategy document**

#### Integrations

- Keycloak IAM for OIDC/SSO with RBAC/ABAC
- Screening APIs (address, TIN, sanctions) — parallel checks
- Bank validation API
- ERP/AP for PO/invoice sync (SAP/Oracle/NetSuite)
- Document storage (S3-compatible with virus scans)
- HashiCorp Vault for secrets management
- Notification services (email/WebSocket)
- Fault tolerance with circuit breakers, retries, and dead-letter queues

> *For detailed integration architecture, system mapping, and fault tolerance patterns, refer to the **Tech Specs document**.*

#### Testing & Quality Assurance

**Unit Testing:**

| Area | Target Coverage | Estimated Effort |
|------|----------------|-----------------|
| Frontend Unit Tests (React/Jest) | 80% coverage (RFP mandate) | ~5 weeks (Dev) |
| Backend Unit Tests (JUnit) | 80% coverage (RFP mandate) | ~6 weeks (Dev) |
| Regression Test Suite (JUnit) | Automated regression per RFP requirement | ~3 weeks (QA) |

**Functional Testing (E2E + Regression):**

| Area | Scope | Effort |
|------|-------|--------|
| Supplier Onboarding E2E | Invite → Form fill → Screening → Approval → Activation (6 features) | ~3 weeks (QA) |
| Screening & Bank Validation (Integration) | Vendor orchestration calls HR screening/bank APIs; result display and error handling | ~2 weeks (QA) |
| Approval Workflows E2E | Multi-level onboarding approval, Master data change, Payment terms (3 features) | ~2 weeks (QA) |
| PO / Invoice Flows E2E | PO import → Acknowledge → Flip to Invoice → Submit → AP Sync (7 features) | ~4 weeks (QA) |
| Document, Dashboard & Cross-cutting | Document mgmt, KPI dashboards, Keycloak SSO flow, multi-tenant isolation, session mgmt | ~3 weeks (QA) |
| Regression Suite | Automated regression across all agents per sprint | ~2 weeks (QA) |

**Performance, Security & Compliance Testing:**

| Area | Scope | Effort |
|------|-------|--------|
| API & Grid Performance | All APIs < 3s (RFP), Grid < 500ms, virtual scrolling stress | ~2 weeks (QA) |
| Load, Stress & Soak Testing | 100–500 concurrent users, ERP sync throughput, container scaling under G4 | ~3 weeks (QA) |
| Vulnerability Scanning (OWASP Top 10) | SAST + DAST scanning of all vendor-built endpoints | ~1.5 weeks (QA) |
| RBAC/ABAC & Tenant Isolation | Role matrix (4 personas × 29 screens + 11 modals), cross-tenant prevention, privilege escalation, RLS | ~3 weeks (QA) |
| SSO, CSP & Vault Validation | Keycloak token flow, session handling, CSP headers, HashiCorp Vault integration | ~1.5 weeks (QA) |
| Infosec Clearance Prep | Documentation and remediation for HighRadius cybersecurity team | ~1 week (QA) |

**QA Execution Timeline (17 Weeks):**

| QA Phase | Program Weeks | Activities |
|----------|--------------|------------|
| Setup & Framework | 1–2 | Automation framework init, CI integration, RBAC matrix prep, test data modeling |
| Backend Validation | 3–8 | 66 APIs + 7 integrations: functional, negative, tenant enforcement, failure injection |
| Frontend + E2E Automation | 6–11 | 29 screens, 11 modals, persona-based access, critical journey automation |
| Integration Hardening | 9–11 | Deep failure simulation, circuit breaker/retry validation |
| Performance Validation | 12–14 | Load, stress, 8-hour soak, month-end simulation |
| Security & Compliance | 13–15 | OWASP, JWT tampering, tenant cross-access, CSP, WCAG 2.0 AA |
| Regression & Release | 15–17 | Full regression cycles, UAT support, release hardening, go-live readiness |

> *For detailed QA strategy, tool stack, and release controls, refer to the **QA Strategy document**.*

#### Post-Deployment Support

- 6-month hypercare at 0.5 FTE
- Production monitoring and issue resolution per SLAs
- Weekly updates (email/call/PVA)
- Root cause analysis and knowledge transfer

> *For detailed hypercare SLAs, escalation matrix, and support model, refer to the **Commercial Agreement document**.*

#### AI Productivity Enhancements

All 6 engineers use Claude Opus AI subscriptions. Productivity multipliers applied:

| Activity | AI Multiplier |
|----------|--------------|
| Code Generation (Frontend) | 1.40x |
| Code Generation (Backend) | 1.30x |
| Unit Test Writing | 1.40x |
| API Documentation | 1.50x |
| Integration Code | 1.15x |
| DevOps & Config | 1.10x |

These are conservative multipliers assuming experienced developers using AI as an accelerator, not a replacement for engineering judgment.

#### Responsibility Matrix (RACI)

Clear ownership delineation between Metapointer (Vendor) and HighRadius — critical for fixed-price scoping:

| Capability | Vendor | HighRadius | Notes |
|-----------|--------|------------|-------|
| UI/UX Development (29 screens + 11 modals) | R, A | C, I | Vendor builds end-to-end; HR provides wireframes & sign-off |
| Backend Services (58 vendor-built APIs) | R, A | C | Vendor full ownership |
| Orchestration Layer (1 API) | R, A | C | Vendor builds orchestration calling HR services |
| Keycloak IAM (Auth/Login/SSO) | I | R, A | HighRadius-owned; vendor integrates only |
| Screening Services (Address/TIN/Sanctions) | C | R, A | HighRadius-owned; vendor integrates + stores results |
| Bank Validation Service | C | R, A | HighRadius-owned; vendor integrates only |
| ERP Integration (SAP/Oracle/NetSuite) | R | A, C | Vendor builds adapters; HR provides API access & samples |
| Document Storage (S3-compatible) | R | C | Vendor builds integration; HR provides infrastructure |
| G4 Platform / Deployment Environment | C | R, A | HighRadius provides; vendor deploys containers |
| Multi-Tenant Architecture | R, A | C | Vendor designs & implements isolation |
| Testing & QA | R, A | C | Vendor owns; HR provides test data & UAT sign-off |
| DevOps / CI-CD Pipeline | R | A, C | Vendor sets up per HR engineering practices |
| Product Requirements & UX Specs | C | R, A | HighRadius provides; vendor implements |
| Hypercare Support (6 months) | R | A, I | Vendor provides 0.5 FTE |
| Knowledge Transfer & Handover | R | A | Work completion requires HR engineering sign-off |

*R = Responsible (does the work) | A = Accountable (final sign-off) | C = Consulted | I = Informed*

#### API Ownership Mapping

APIs are categorized by ownership: Vendor Build (full implementation), Integrate (HR Service) (vendor only calls HR-provided API), or Vendor Build (Orchestration) (vendor builds orchestration layer calling HR services).

| Category | Count | Description |
|----------|-------|-------------|
| **Vendor Build (Full)** | 58 | End-to-end vendor ownership — design, implement, test, deploy |
| **Integrate (HR Service)** | 7 | HighRadius-owned backend services — vendor builds adapter/integration layer only |
| **Vendor Build (Orchestration)** | 1 | Vendor builds orchestration layer coordinating multiple HR services |
| **Total APIs** | **66** | |

**API Distribution by Agent:**

| Agent/Module | Vendor Build | HR Integrate | Orchestration | Total |
|-------------|-------------|-------------|---------------|-------|
| Supplier Onboarding | 12 | 0 | 0 | 12 |
| Supplier Screening | 3 | 3 | 1 | 7 |
| Bank Account Validation | 2 | 1 | 0 | 3 |
| Supplier Approval | 8 | 0 | 0 | 8 |
| Master Data Change | 6 | 0 | 0 | 6 |
| Purchase Order | 9 | 1 | 0 | 10 |
| Portal Invoice | 10 | 1 | 0 | 11 |
| Cross-cutting (Dashboard, Audit, Notifications, Admin) | 8 | 1 | 0 | 9 |
| **Total** | **58** | **7** | **1** | **66** |

*Yellow-highlighted rows in detailed appendix indicate HighRadius-owned backend services where vendor effort is limited to integration.*

#### UI Gap Analysis Summary

Analysis of the 91-page HighRadius User Journey wireframes revealed significant gaps that are accounted for in our estimation:

| Gap Category | Count | Details |
|-------------|-------|---------|
| Screens Provided by HighRadius | 13 | From User Journey wireframes |
| Missing / To-Be-Designed Screens | 16 | 55% of screens require UX design from scratch |
| Validation Gaps | 12 | Validation types specified but not illustrated in wireframes (error states, toast notifications, inline indicators) |
| Logic Complexity Gaps | 7 | Areas with significantly more implementation complexity than wireframes suggest |
| Missing API Endpoints | 3 | Required endpoints not reflected in wireframes |
| Technical Gaps | 9 | Infrastructure/integration gaps not covered in wireframes |
| Workflow Gaps | 6 | Workflow logic not fully specified in wireframes |
| **Total Gaps** | **48** | **All accounted for in estimation and delivery plan** |

**Detailed Gap Breakdown:**

**Missing / To-Be-Designed Screens (16):**

| # | Screen Name | Persona | Phase | Complexity | Notes |
|---|------------|---------|-------|------------|-------|
| 1 | Supplier Dashboard | Supplier | Phase 1 | High | Invoice pipeline, aging summary, payment status, tasks & alerts |
| 2 | Manager Dashboard | Supplier Manager | Phase 1 | High | Onboarding funnel, pending tasks, SLA metrics, quick-action panel |
| 3 | Screening Dashboard | Supplier Manager | Phase 1 | Medium | Aggregated compliance results across suppliers |
| 4 | Approval Worklist | Supplier Manager | Phase 1 | Medium | Task queue with approve/reject/reassign actions |
| 5 | Admin Settings | Admin | Phase 1 | High | Screening configuration, system parameters |
| 6 | User/Role Management | Admin | Phase 1 | High | Keycloak-integrated user creation, permission control |
| 7 | Audit Trail | Admin | Phase 1 | Medium | Filterable/exportable action log |
| 8 | Form Builder | Admin | Phase 1 | High | Drag-and-drop form configuration, multi-language labels |
| 9 | Workflow Configuration | Admin | Phase 1 | High | Approval chain builder with escalation rules |
| 10 | Notification Center | Cross-cutting | Phase 1 | Medium | Real-time alerts for all personas |
| 11 | PO List | Supplier | Phase 2 | Medium | Filterable PO grid with status indicators |
| 12 | PO Detail | Supplier | Phase 2 | Medium | PO details with acknowledge/reject actions |
| 13 | Invoice List | Supplier | Phase 2 | Medium | Invoice grid with lifecycle tracking |
| 14 | Invoice Detail | Supplier | Phase 2 | Medium | Full invoice view with status history |
| 15 | PO Flip / Invoice Creation | Supplier | Phase 2 | High | Auto-populate from PO, partial invoicing, tax/discount |
| 16 | Master Data Change Request | Supplier/Manager | Phase 2 | Medium | Data update form with approval workflow trigger |

**Validation Gap Analysis (12 types not illustrated in wireframes):**

| # | Validation Type | Affected Screens | UX Spec Required |
|---|----------------|-----------------|-----------------|
| 1 | Email format validation (registration) | Supplier Registration | Inline error states |
| 2 | TIN format/checksum validation | Registration Form | Real-time feedback indicator |
| 3 | Bank account number format validation | Bank Details Form | Field-level error + toast |
| 4 | Required field enforcement (dynamic per tenant config) | All form screens | Visual indicators + submit blocking |
| 5 | File type/size validation (document upload) | Document Upload | Error toast + supported format list |
| 6 | Duplicate supplier detection feedback | Invitation, Registration | Warning modal with existing supplier details |
| 7 | Approval chain completeness validation | Workflow Configuration | Pre-save validation + error summary |
| 8 | PO quantity bounds validation (partial invoicing) | PO Flip Screen | Inline error: "Cannot exceed PO quantity" |
| 9 | Invoice amount reconciliation validation | Invoice Creation | Warning when total deviates from PO |
| 10 | Date range validation (PO/invoice filters) | List screens | Inline date picker constraints |
| 11 | Session timeout/token expiry handling | All screens | Modal with re-login prompt |
| 12 | Concurrent edit conflict detection | Approval screens | Toast notification + refresh prompt |

**Logic Complexity Gaps (7 areas exceeding wireframe complexity):**

| # | Area | Wireframe Shows | Actual Complexity |
|---|------|----------------|------------------|
| 1 | Multi-level approval routing | Simple approve/reject | Conditional routing (spend threshold, region, category), SLA escalation, reassignment, delegation |
| 2 | Dynamic form configuration | Static form layout | Tenant-specific field ordering, validation rules, visibility conditions, multi-language labels, reusable templates |
| 3 | Bulk CSV onboarding | Single upload button | Duplicate detection, partial failure handling, progress tracking, error report download, rollback on critical failures |
| 4 | PO-to-Invoice flip | Simple mapping | Partial invoicing, line-item selection, tax/discount calculation, multi-currency, attachment inheritance |
| 5 | Screening orchestration | Sequential checks | 4 parallel checks with independent pass/fail, retry on timeout, partial result display, blocking vs. warning logic |
| 6 | Multi-tenant data isolation | Not shown | Schema-per-tenant resolution, JWT claim extraction, middleware enforcement, cross-tenant query prevention |
| 7 | ERP sync conflict resolution | Simple sync icon | Bi-directional sync handling, conflict detection (stale PO data), retry queues, dead-letter handling |

**Missing API Endpoints (3):**

| # | Endpoint | Purpose | Why Missing |
|---|----------|---------|-------------|
| 1 | Bulk invitation status tracking API | Track progress of CSV bulk imports | Wireframes show upload but not progress tracking |
| 2 | Screening retry/re-trigger API | Allow manual re-trigger of failed screening checks | Wireframes show results but not retry flow |
| 3 | Audit trail export API | Export filtered audit logs to CSV/PDF | Wireframes show audit screen but not export |

**Technical Gaps (9):**

| # | Gap | Impact | Mitigation |
|---|-----|--------|------------|
| 1 | WebSocket infrastructure for real-time notifications | Required for live status updates and alerts | Design in Sprint 0; implement in Sprint 1 |
| 2 | File virus scanning integration | Required for secure document uploads | Integrate with ClamAV or S3 scanning in Sprint 0 |
| 3 | Multi-language label management system | Required for i18n form configuration | Design label store schema in Sprint 0 |
| 4 | Tenant provisioning automation | Required for admin tenant setup | Admin API + seed data scripts in Sprint 1 |
| 5 | Rate limiting and throttling configuration | Required for API security | API Gateway configuration in Sprint 0 |
| 6 | Health check and readiness probes | Required for Kubernetes deployment | Standard Spring Boot Actuator + custom checks |
| 7 | Database migration tooling (schema versioning) | Required for multi-tenant schema management | Flyway with tenant-aware migration strategy |
| 8 | Async job queue for long-running operations | Required for bulk imports, screening orchestration | Redis-backed job queue with status polling |
| 9 | Caching strategy for static/config data | Required for performance | Redis cache for form templates, workflow defs, i18n labels |

**Workflow Gaps (6):**

| # | Workflow | Gap Description |
|---|---------|----------------|
| 1 | Invitation expiry and re-invite | Wireframes don't specify: expiry period, re-invite flow, expired link handling |
| 2 | Draft save/resume lifecycle | Wireframes show save button but not: auto-save interval, draft expiry, resume from last step |
| 3 | Approval SLA escalation | Wireframes show approval but not: escalation triggers, notification chain, auto-approve on SLA breach |
| 4 | Supplier deactivation/reactivation | Not shown in wireframes — required for compliance (e.g., sanctions match after activation) |
| 5 | Master data change impact assessment | Wireframes show change form but not: which changes trigger re-screening, which require approval |
| 6 | Invoice rejection and resubmission | Wireframes show status but not: rejection reason capture, resubmission flow, version tracking |

**Mitigation:** Validation Error State Library to be created in Sprint 0. All error messages, toast notifications, and inline validation indicators documented before Sprint 1 development begins. Sprint 0 design sprint addresses missing screens, with UX running 1 sprint ahead of development throughout.

#### Frontend Component Inventory

| Category | Count | Details |
|----------|-------|---------|
| G4 OOB Components (Reused) | ~15–20 | Grids, form controls, buttons, modals, navigation — leveraged directly from G4 DSL library |
| Custom Components (G4-Extended) | ~10 | Portal-specific components not covered by G4 OOB (e.g., screening progress, approval chain visualization, PO-flip mapper) |
| Screen-Level React Components | 39 | Across 19 screens, mapping directly to dev tasks and Jira tickets |
| Layout Definitions | 8 | Page templates for different screen types |
| Total Components | ~72–77 | G4-first approach reduces custom build effort |

G4 OOB component evaluation completed in Sprint 0. Custom components built only where G4 library gaps exist. Component-per-screen mapping drives sprint planning and task allocation.

### 1.2 Out of Scope

- **HighRadius-Owned Services Build:** Development or modification of Keycloak authentication/login/signup, bank validation service, screening services (address/TIN/sanctions), or G4 OOB components — vendor scope limited to integration effort only
- **Additional ERP Integrations:** ERP types beyond SAP/Oracle/NetSuite or custom multi-customer mappings exceeding RFP specs
- **Data Migration:** Migration of existing supplier data from ERPs, spreadsheets, or other legacy systems
- **Infrastructure Provisioning:** Hardware, cloud resources, or environment setup beyond containerized G4 deployment
- **Testing Exclusions:** Real-world production data testing (vendor uses mocks/samples); compliance certifications beyond SOX/GDPR support
- **Scope Changes:** Requirements exceeding defined scope without approved change requests, including major wireframe revisions after design sign-off

---

## 2. Solution Overview

**Classification: PROJECT-SPECIFIC**

### 2.1 Solution Vision

The Supplier Portal is a secure, scalable, self-service web application designed to digitize and streamline supplier onboarding, compliance validation, purchase order management, and invoice processing for HighRadius's AP automation platform.

**The solution aims to:**
- Eliminate manual, email-driven supplier interactions by providing a single system of engagement
- Enforce compliance and validation at the point of data entry through automated real-time checks
- Improve operational efficiency through automation, reducing onboarding cycles from 15–20 days to 3–5 days and invoice SLAs from ~60% to >90%
- Provide real-time visibility to suppliers and internal stakeholders via dashboards
- Support multi-tenant, enterprise-grade scalability with 100% data isolation

### 2.2 Capability Map

| Agent | Type | Key Features |
|-------|------|-------------|
| Supplier Onboarding | Automated | Individual/bulk (CSV) invitations, dynamic multi-language forms, document upload/validation, draft save/resume, duplicate checking |
| Supplier Screening | Automated | Parallel real-time checks: address verification, TIN validation, sanctions screening (OFAC), with progress indicators and actionable error feedback |
| Bank Account Validation | Automated | Real-time bank detail verification, ownership validation, fraud prevention |
| Supplier Approval | Assisted | Multi-level configurable workflows, conditional routing (e.g., spend threshold), SLA auto-escalation, approve/reject/reassign |
| Master Data Change Approval | Assisted | Approval workflows for supplier data updates, payment terms changes, configurable chains |
| Purchase Order | Automated | Multi-ERP PO import/sync, acknowledgment/reject by supplier, real-time status tracking |
| Portal Invoice Creation | Assisted | Manual entry + one-click PO-flip, partial invoicing, tax/discount lines, attachments, AP sync |

**Additional Self-Service Capabilities:**
- Supplier Dashboard: invoice status pipeline, aging summary, payment status, tasks & alerts
- Manager Dashboard: onboarding funnel, pending tasks, SLA compliance, KPI tracking (pass/fail rates, coverage %)
- In-app/email notifications and document management with versioning
- Notification Center with real-time alerts for PO receipts, invoice status changes, and approval decisions

### 2.3 Transformation Vision — From Current State to Future State

**Automated Onboarding Workflows:**
- **Digital Invitation:** Individual or bulk (CSV) from portal. Validates emails, checks duplicates, dispatches secure time-limited links
- **Dynamic Self-Registration:** Multi-step form per tenant configuration, real-time validation, save draft/resume capability
- **Real-Time Screening:** Address, TIN, Sanctions, Bank — four parallel checks on submission. Failures block with actionable errors and retry options
- **Multi-Level Approval:** Configurable chains with conditional routing (e.g., spend threshold, region, category), SLA auto-escalation, delegation
- **Auto-Activation:** On final approval, supplier activated + notified, full portal access granted via Keycloak SSO
- **Impact:** 15–20 days → 3–5 days onboarding. 100% screening coverage. 80%+ touchpoint reduction

**Real-Time PO to Invoice Conversion:**
- **PO Import & Sync** from buyer ERP (multi-customer), real-time on PO List with notifications
- **Self-service Acknowledge/Reject** in portal with auto-sync to ERP
- **One-Click PO Flip:** auto-populate invoice from PO, partial invoicing, tax/discount lines, attachments
- **Validated Submission** with field-level validation, auto-sync to AP, real-time status tracking
- **Impact:** SLA compliance ~60% → >90%. First-pass accuracy ~65% → >95%

**Self-Service Dashboards & Analytics:**
- Supplier Dashboard: invoice status pipeline (Draft, Submitted, Approved, Paid), aging summary, payment status, tasks & alerts
- Manager Dashboard: onboarding funnel metrics, pending tasks, SLA compliance, KPI tracking
- Admin Audit Trail: complete filterable record of all portal actions, exportable for compliance

### 2.4 High-Level Workflow

1. Supplier Manager sends onboarding invitation (individual or bulk via CSV)
2. Supplier completes self-registration: multi-step dynamic form, document upload, real-time validation, with draft save/resume and multi-language support
3. Automated compliance screening triggered: address, TIN, sanctions, and bank validation run in parallel with progress indicators
4. Submission enters approval workflow: multi-level, configurable routing with SLA-based escalation
5. Upon approval, supplier is activated, notified, and granted full portal access via Keycloak SSO
6. Supplier views/acknowledges/rejects POs (imported from ERPs), creates/submits invoices (manual or PO-flip)
7. Invoice and PO data syncs with ERP/AP systems with pre-submission field-level validation
8. Stakeholders track progress via real-time dashboards, notification center, and exportable reports

### 2.5 RFP Requirement Traceability

Direct mapping from RFP requirements to proposed solution modules, confirming full coverage:

| RFP Requirement Area | Solution Module | Screens | Phase | Coverage |
|---------------------|----------------|---------|-------|----------|
| Supplier Onboarding (invitations, forms, documents) | Supplier Onboarding Agent | 6 screens + 3 modals | Phase 1 | Full |
| Compliance Screening (address, TIN, sanctions) | Supplier Screening Agent | 3 screens + 1 modal | Phase 1 | Full |
| Bank Account Validation | Bank Account Validation Agent | 2 screens | Phase 1 | Full |
| Multi-Level Approval Workflows | Supplier Approval Agent | 4 screens + 2 modals | Phase 1 | Full |
| Master Data Change Management | Master Data Change Approval Agent | 2 screens + 1 modal | Phase 2 | Full |
| PO Import/Acknowledgment (multi-ERP) | Purchase Order Agent | 5 screens + 2 modals | Phase 2 | Full |
| Invoice Creation (manual + PO-flip) | Portal Invoice Creation Agent | 5 screens + 2 modals | Phase 2 | Full |
| Dashboards (Supplier + Manager) | Cross-cutting | 2 screens | Phase 1 | Full |
| Keycloak IAM / SSO / RBAC | Integration (HR-owned) | Login/Auth | Phase 1 | Integration only |
| Multi-Tenancy & Data Isolation | Architecture (schema-per-tenant) | All screens | Phase 1 | Full |
| WCAG 2.0 AA Accessibility | Frontend architecture | All screens | Both | Full |
| 80% Code Coverage | QA framework | — | Both | Full |
| <3s API Response | Backend architecture | — | Both | Full |
| Containerized G4 Deployment | DevOps/CI-CD | — | Phase 1 | Full |
| Hypercare (6 months) | Support model | — | Post-deployment | Full |
| Handover (GIT, docs, KT) | Delivery governance | — | Phase 2 end | Full |

**Result: 100% RFP requirement coverage** across all 7 agents, NFRs, engagement expectations, and success criteria.

### 2.6 Persona Journeys

**Supplier Journey:**
- Receives email invitation with secure, time-limited link → completes multi-step registration → automated screening → approval workflow → dashboard access → PO management → invoice creation via PO-flip → status tracking

**Supplier Manager Journey:**
- SSO login → Manager Dashboard with pipeline metrics → send invitations (individual/bulk) → monitor worklist with status filters → review screening results → process approval tasks → track SLA compliance

**Admin Journey:**
- Configure onboarding forms (drag-and-drop builder, multi-language labels, reusable templates) → define approval workflows (chains, escalation rules, conditional routing) → manage users/roles via Keycloak → view audit trail (filterable, exportable)

---

## 3. Non-Functional Requirements

**Classification: PROJECT-SPECIFIC**

### 3.1 Availability

- 99.5% system availability target
- Redundant components to minimize single points of failure
- Health checks and auto-restart policies
- Planned maintenance windows with minimal disruption

### 3.2 Performance

| Metric | Target |
|--------|--------|
| API Response Time (P95) | < 3 seconds |
| API Response Time (P99) | < 3 seconds |
| Grid Load (1,000+ rows) | < 500 milliseconds |
| Page Load Time | < 2 seconds |
| Screening Execution | Real-time with progress indicators |
| File Upload/Download | < 5 seconds for typical documents |

- Asynchronous processing for long-running operations (screening, bulk imports)
- Efficient pagination and filtering for large datasets

### 3.3 Scalability

- 1,000 concurrent users / 10,000 transactions per hour
- Horizontal scalability — frontend, backend, and integration layers scale independently
- Architecture supports onboarding additional tenants without impacting existing users
- Multi-tenant automation absorbs acquisitions without proportional headcount

### 3.4 Security

- Keycloak-based SSO with OIDC/JWT authentication
- RBAC/ABAC enforcement at every layer (zero-trust)
- TLS 1.3 for data in transit, AES-256 for data at rest
- HashiCorp Vault for secrets management
- OWASP Top 10 compliance
- Secure file handling with virus scanning for document uploads
- CSP headers and XSS protection

> *For detailed security architecture, permission matrices, and enforcement model, refer to the **Tech Specs document**.*

### 3.5 Compliance

- Full immutable audit trail for all onboarding, approval, and invoice actions
- 2-year audit log retention, filterable and exportable
- SOX/GDPR support alignment
- 100% screening coverage eliminating non-compliant supplier risk
- Data retention and traceability aligned with enterprise audit standards

### 3.6 Code Quality

- 80% minimum test code coverage (backend — JUnit, frontend — Jest)
- Static code analysis with no critical/high findings
- PR review policy: every merge requires at least 1 peer review
- Definition of Done includes: code complete, tests passing, reviewed, integration tested, security scanned, documented

---

*Prepared By: Metapointer | For: HighRadius Corporation | Date: February 28, 2026*
