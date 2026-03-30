Product Scope & Gap Analysis

AP Supplier Portal

Prepared for:  HighRadius Corporation

Prepared by:  Metapointer Labs Pvt. Ltd.

Date:  March 2026

Version:  3.3

Table of Contents

1.  Scope Overview	3

1.1  In Scope	3

1.2  Out of Scope	4

1.3  Assumptions	4

1.4  Dependencies	4

2.  User Roles & Access	6

3.  Functional Scope	7

3.1  Capability Map	7

3.2  Functional Requirements	7

3.3  Screen Inventory	8

3.4  High-Level Workflow	8

4.  MVP & Phasing	10

5.  Acceptance Criteria	11

6.  Requirements Traceability	12

7.  Wireframe Gap Analysis	14

7.1  Missing / To-Be-Designed Screens (16)	14

7.2  Validation Gap Analysis (12)	15

7.3  Logic Complexity Gaps (7)	16

7.4  Missing API Endpoints (3)	16

7.5  Technical Gaps (9)	16

7.6  Workflow Gaps (6)	17


# 1.  Scope Overview



## 1.1  In Scope


The following deliverables are fully in scope and accounted for within the fixed-price engagement. All estimates are based on a bottom-up analysis of the HighRadius Product Backlog Requirements (PBR) spreadsheet, the 91-page User Journey wireframes, RFP requirements, and gap analysis:


| Deliverable Category | Count | Description |
| --- | --- | --- |
| Application Screens | 29 | Responsive web application screens across all three personas |
| Modal / Popup Workflows | 11 | Workflow confirmation, document preview, action, and configuration modals |
| Intelligent Agents | 7 | 4 automated + 3 assisted agents covering the full supplier lifecycle |
| Vendor-Built APIs | 58 | Full ownership: design, implement, unit-test, deploy, document |
| Integration APIs (HR-owned) | 7 | HighRadius-owned services; vendor builds adapter and integration layer only |
| Orchestration API | 1 | Vendor-built orchestration coordinating multiple HR-owned services |
| Total APIs | 66 | Complete API surface area across all agents and cross-cutting services |
| Core Features | 25+ | Onboarding, screening, approval, PO management, invoice, dashboards, admin config |
| Integrations | 8 | Keycloak IAM, screening APIs, bank validation, ERP (SAP/Oracle/NetSuite), S3, Vault, WebSocket, notifications |
| Post-Deployment Hypercare | 6 months | 0.5 FTE production support, SLA monitoring, and knowledge transfer |


Additional in-scope items:

•  Responsive design with WCAG 2.0 AA accessibility compliance across all 29 screens

•  Virtual scrolling for grids handling 1,000+ rows without performance degradation

•  Multi-tenant architecture with 100% schema-per-tenant data isolation and row-level security

•  HighRadius Product Backlog Requirements (PBR) spreadsheet reviewed as the primary requirements source alongside the 91-page User Journey wireframes — all 48 identified gaps addressed

•  Sprint 0 design sprint covering 16 undesigned screens (55% of total screens)

•  Validation Error State Library — all error messages, toast notifications, and inline states documented before Sprint 1

•  CI/CD pipeline following HighRadius engineering practices (RFP Section 5 mandate)

•  OpenAPI/Swagger documentation for all 66 APIs

•  Feature-level technical design documentation, deployment guides, and runbooks

•  GIT handover with all source code, documentation, and knowledge transfer sessions


## 1.2  Out of Scope


The following items are explicitly excluded from this engagement. Any change request to include these will require formal impact assessment on cost and timeline:

•  Development or modification of HighRadius-owned services: Keycloak authentication/login/signup, bank validation service, screening services (address, TIN, sanctions), or G4 OOB components

•  ERP types beyond SAP, Oracle, and NetSuite, or custom multi-customer mappings exceeding RFP specifications

•  Migration of existing supplier data from ERPs, spreadsheets, or other legacy systems

•  Hardware, cloud resource, or environment provisioning beyond containerised G4 deployment

•  Real-world production data testing during development — vendor uses mocks and synthetic samples

•  Compliance certifications beyond SOX/GDPR support (e.g., ISO 27001, PCI-DSS)

•  Requirements exceeding the defined scope without an approved change request, including major wireframe revisions after design sign-off


## 1.3  Assumptions


•  Platform Availability: HighRadius will provide timely access to Keycloak IAM, screening APIs, bank validation API, G4 platform, and ERP sample data for UAT.

•  Scope Stability: RFP-defined scope (7 agents, 29 screens, specified NFRs) is frozen post-Sprint 0. Changes managed through formal CR process.

•  Design Sign-off Speed: Weekly UX/UI sign-offs and stakeholder feedback will be provided by HighRadius within 5 business days to prevent design iteration delays.

•  March 2026 Kickoff: Project kickoff assumes March 2026 start. Any delay shifts all downstream milestones proportionally.

•  Test Data: Performance testing will use production-scale datasets provided by HighRadius.

•  Product Requirements: UX specifications and product requirements will be provided by HighRadius per RFP Section 5 for all agent workflows.


## 1.4  Dependencies


Full dependency register with ownership, impact, and mitigation is provided in the Executive Overview document (Document 1). Key dependencies:

•  Keycloak IAM environment — HighRadius (D1)

•  G4 DSL component library — HighRadius (D2)

•  Screening and bank validation APIs — HighRadius (D3, D4)

•  ERP sample data for PO and invoice flows — HighRadius (D5)

•  UX wireframes for 16 undesigned screens — HighRadius (D6)

•  QA/UAT environment provisioned — HighRadius (D7)

•  HashiCorp Vault access — HighRadius (D10)


# 2.  User Roles & Access


The portal supports four distinct personas with clearly defined access boundaries. Role assignment is managed through Keycloak IAM. The permission model uses a hybrid RBAC + ABAC enforcement chain across all 29 screens and 11 modals:


| Persona | Primary Responsibilities | Key Screens | Access Level |
| --- | --- | --- | --- |
| Supplier | Complete self-registration; upload documents; view and acknowledge POs; create and submit invoices; track payment status | Registration form, Supplier Dashboard, PO List, PO Detail, Invoice List, Invoice Creation, Master Data Change | Own records only — full access to own data; no access to other suppliers or manager views |
| Supplier Manager | Send invitations (individual and bulk CSV); monitor onboarding pipeline; review screening results; process approval worklist; track SLA compliance | Manager Dashboard, Supplier List, Screening Dashboard, Approval Worklist, Document Management | Full access to all supplier records within their tenant; view-only on approvals and admin |
| Approver | Review and process approval tasks for supplier onboarding and master data changes; approve, reject, or reassign within configured SLA | Approval Worklist, Approval Action Modal, Master Data Change | Full access to approval tasks assigned to their role; view-only on supplier and manager screens |
| HighRadius / Client Admin | Configure onboarding forms; define approval workflows; manage users and roles; view audit trail; configure system parameters | Form Builder, Workflow Configuration, User/Role Management, Admin Settings, Audit Trail, Notification Centre | Full configuration access; view-only on operational screens |


Security Enforcement
Access is enforced at 5 layers: (1) Frontend route guards and component visibility, (2) API Gateway JWT validation and RBAC middleware, (3) Service layer ABAC checks, (4) Database tenant_id scoping and row-level security, (5) Immutable audit logging of every access decision. No request reaches business logic without valid JWT + tenant context + role match.


# 3.  Functional Scope



## 3.1  Capability Map


The portal is structured around 7 intelligent agents covering the complete supplier lifecycle from onboarding through invoice processing:


| Agent | Type | Core Features |
| --- | --- | --- |
| Supplier Onboarding | Automated | Individual email invitations; bulk CSV onboarding; dynamic multi-language registration forms (tenant-configured); document upload and validation; draft save and resume; duplicate supplier detection; auto-activation on approval |
| Supplier Screening | Automated | Four parallel real-time checks: address verification, TIN/EIN validation, OFAC sanctions screening, bank account pre-validation; progress indicators; actionable error feedback; retry capability; 100% coverage guarantee |
| Bank Account Validation | Automated | Real-time bank detail verification via HighRadius-owned API; ownership validation; fraud prevention against Business Email Compromise (BEC) attacks; change triggers re-validation workflow |
| Supplier Approval | Assisted | Multi-level configurable approval chains; conditional routing by spend threshold, region, and category; SLA-based auto-escalation; approve, reject, and reassign actions; delegation support; KPI tracking |
| Master Data Change Approval | Assisted | Structured change request form for supplier data updates and payment term modifications; configurable approval chains; determines which changes trigger re-screening; version tracking |
| Purchase Order | Automated | Multi-ERP PO import and synchronisation (SAP, Oracle, NetSuite); real-time status display; supplier acknowledgement and rejection with auto-sync to ERP; notifications on PO receipt |
| Portal Invoice Creation | Assisted | Manual invoice creation with field-level validation; one-click PO-flip with auto-population; partial invoicing; tax and discount line items; attachment support; AP synchronisation; rejection and resubmission flow |



## 3.2  Functional Requirements


The following diagram illustrates the complete functional requirements coverage across all portal modules and personas:

Figure 2: AP Supplier Portal — Functional Requirements Overview


## 3.3  Screen Inventory


Portal screens breakdown across all workflows (29 screens total):


| Workflow / Feature | Screens | Complexity | Phase |
| --- | --- | --- | --- |
| Supplier Onboarding | 6 | High | Phase 1 |
| Supplier Screening | 3 | Medium | Phase 1 |
| Bank Account Validation | 2 | Medium | Phase 1 |
| Approval Workflows | 4 | High | Phase 1 |
| Dashboards (Supplier + Manager) | 2 | High | Phase 1 |
| Admin (Form Builder, Workflow Config, User Mgmt, Settings, Audit) | 5 | High | Phase 1 |
| PO Management | 5 | High | Phase 2 |
| Invoice Management | 5 | High | Phase 2 |
| Master Data Management | 2 | Medium | Phase 2 |
| Notification Centre | 1 | Medium | Phase 1 |
| Total | 29 | — | — |



## 3.4  High-Level Workflow


The end-to-end supplier lifecycle follows this workflow:

•  Step 1 — Invitation: Supplier Manager sends individual or bulk CSV invitation from portal. System validates email, checks for duplicates, and dispatches a secure time-limited link.

•  Step 2 — Registration: Supplier completes multi-step dynamic registration form per tenant configuration, uploads required documents, with real-time validation, draft save, and multi-language support.

•  Step 3 — Screening: Automated compliance screening triggered on submission: address, TIN, OFAC sanctions, and bank validation run in parallel with progress indicators. Failures block with actionable errors and retry options.

•  Step 4 — Approval: Submission enters configurable multi-level approval workflow with SLA-based auto-escalation and conditional routing. Approvers receive notifications and can approve, reject, or reassign.

•  Step 5 — Activation: On final approval, supplier is automatically activated and notified. Full portal access granted via Keycloak SSO. Supplier data synchronised to master data store.

•  Step 6 — PO Management: Supplier views purchase orders imported from buyer ERPs. Acknowledges or rejects POs directly in the portal. Status auto-syncs back to ERP in real time.

•  Step 7 — Invoicing: Supplier creates invoices manually or via one-click PO-flip. Field-level validation enforced before submission. Invoice syncs to AP system with real-time status tracking.

•  Step 8 — Visibility: All stakeholders track progress via real-time dashboards, notification centre, and exportable audit trail. KPI metrics visible to Supplier Manager. Admin has full audit log access.


# 4.  MVP & Phasing


The programme is structured in two delivery phases aligned to the HighRadius RFP agent groupings, with Sprint 0 providing the technical foundation for both. Per this proposal, “MVP” and “Phase 1” refer to the same 4-agent delivery gate — the first production release comprising Supplier Onboarding, Screening, Bank Account Validation, and Supplier Approval:


| Phase | Agents | Weeks | Go-Live Target | Key Deliverables |
| --- | --- | --- | --- | --- |
| Sprint 0 — Foundation | N/A | 1–2 | N/A | Architecture, DevOps/CI-CD, G4 OOB evaluation, Keycloak setup, design sprint (16 screens), Validation Error State Library, DB schema v1 |
| Phase 1 (MVP) | Supplier Onboarding, Supplier Screening, Bank Account Validation, Supplier Approval | 3–12 | ~Week 12 from Kickoff | 17 screens, ~40 APIs, core dashboards, Keycloak + screening + bank validation integrations, UAT sign-off, 1 live customer in production |
| Phase 2 — Full Delivery | Purchase Order, Portal Invoice Creation, Master Data Change Approval | 13–20 | ~Week 20 from Kickoff | 12 additional screens, ~27 APIs, full ERP sync (SAP/Oracle/NetSuite), complete portal in production, GIT handover, KT sessions |
| Hypercare | All agents (support) | Months 5–11 from Kickoff (6-month Hypercare) | Continuous | 0.5 FTE production support, SLA monitoring, performance tuning, knowledge transfer to HighRadius operations team |


Phase 1 (MVP) Commitment
Phase 1 targets production with 1 live customer at ~Week 12 from Kickoff — delivering the four highest-value agents (Onboarding, Screening, Bank Validation, Approval). This enables HighRadius to demonstrate immediate value to clients while Phase 2 transactional capabilities are completed in parallel.


# 5.  Acceptance Criteria


Acceptance is measured at two levels: (a) feature-level Definition of Done enforced at every sprint, and (b) agent-level KPI achievement required for MASC Milestone (c). All 90%+ KPI targets must be met before final handover acceptance:


| Agent | KPI Metric | Target |
| --- | --- | --- |
| Supplier Onboarding | % of invitations resulting in completed registrations | >90% |
| Supplier Onboarding | Average onboarding cycle time (invitation to activation) | < 5 business days |
| Supplier Screening | % of submissions auto-screened without manual intervention | >95% |
| Supplier Screening | Average screening execution time (all 4 checks) | < 30 seconds |
| Bank Account Validation | % of bank details validated on first submission | >90% |
| Supplier Approval | % of approvals completed within SLA | >90% |
| Supplier Approval | Average approval cycle time | < 2 business days |
| Purchase Order | % of POs successfully imported from ERP | >95% |
| Purchase Order | PO acknowledgement sync accuracy | >99% |
| Portal Invoice Creation | Invoice first-pass accuracy rate | >95% |
| Portal Invoice Creation | Average invoice creation time via PO-flip | < 5 minutes |
| Master Data Change | % of changes processed through workflow without error | >90% |
| Master Data Change | Average change approval cycle time | < 3 business days |


Feature-level Definition of Done — a story is not complete until ALL criteria are met:

•  Code complete, clean, follows coding standards, self-reviewed

•  Unit tests written and passing: minimum 80% coverage (Jest for frontend, JUnit for backend)

•  PR reviewed and approved by at least 1 peer (logic, security, performance, architecture)

•  Feature works end-to-end across frontend and backend; API contracts validated

•  No open critical or high-severity bugs; medium/low documented and triaged

•  API documentation (Swagger), technical design doc, and runbooks updated

•  SAST passed with no critical/high findings; RBAC/ABAC validated; CSP verified

•  Feature deployed via CI/CD to QA environment and smoke-tested

•  All acceptance criteria verified and demonstrated to HighRadius stakeholder


# 6.  Requirements Traceability


Direct mapping from all RFP requirements to proposed solution modules confirms 100% coverage. No requirements are unaddressed or deferred:


| RFP Requirement Area | Solution Module | Screens | Phase | Coverage |
| --- | --- | --- | --- | --- |
| Supplier Onboarding (invitations, forms, documents) | Supplier Onboarding Agent | 6 screens + 3 modals | Phase 1 | Full |
| Compliance Screening (address, TIN, sanctions) | Supplier Screening Agent | 3 screens + 1 modal | Phase 1 | Full |
| Bank Account Validation | Bank Account Validation Agent | 2 screens | Phase 1 | Full |
| Multi-Level Approval Workflows | Supplier Approval Agent | 4 screens + 2 modals | Phase 1 | Full |
| Master Data Change Management | Master Data Change Approval Agent | 2 screens + 1 modal | Phase 2 | Full |
| PO Import and Acknowledgement (multi-ERP) | Purchase Order Agent | 5 screens + 2 modals | Phase 2 | Full |
| Invoice Creation (manual + PO-flip) | Portal Invoice Creation Agent | 5 screens + 2 modals | Phase 2 | Full |
| Dashboards (Supplier + Manager) | Cross-cutting | 2 screens | Phase 1 | Full |
| Keycloak IAM / SSO / RBAC | Integration (HR-owned) | Login/Auth | Phase 1 | Integration only |
| Multi-Tenancy & Data Isolation | Architecture (schema-per-tenant) | All screens | Phase 1 | Full |
| WCAG 2.0 AA Accessibility | Frontend architecture | All screens | Both | Full |
| 80% Code Coverage | QA framework | — | Both | Full |
| <3s API Response | Backend architecture | — | Both | Full |
| Containerised G4 Deployment | DevOps/CI-CD | — | Phase 1 | Full |
| Hypercare (6 months) | Support model | — | Post-deploy | Full |
| Handover (GIT, docs, KT) | Delivery governance | — | Phase 2 end | Full |


100% RFP Coverage
All 7 agents, all non-functional requirements (NFRs), all engagement expectations, and all success criteria defined in the HighRadius RFP are fully covered within this proposal. No gaps, no deferred items, no scope ambiguity.

Non-Functional Requirements coverage:

Figure 3: AP Supplier Portal — Non-Functional Requirements Coverage


# 7.  Wireframe Gap Analysis


A detailed analysis of the 91-page HighRadius User Journey wireframes identified 48 gaps across 6 categories. All gaps are fully accounted for in our estimation and delivery plan — no hidden scope, no surprise change requests.


| Gap Category | Count | Details |
| --- | --- | --- |
| Screens Provided by HighRadius | 13 | From User Journey wireframes |
| Missing / To-Be-Designed Screens | 16 | 55% of screens require UX design from scratch |
| Validation Gaps | 12 | Validation types specified but not illustrated in wireframes (error states, toast notifications, inline indicators) |
| Logic Complexity Gaps | 7 | Areas with significantly more implementation complexity than wireframes suggest |
| Missing API Endpoints | 3 | Required endpoints not reflected in wireframes |
| Technical Gaps | 9 | Infrastructure/integration gaps not covered in wireframes |
| Workflow Gaps | 6 | Workflow logic not fully specified in wireframes |
| Total Gaps | 48 | All accounted for in estimation and delivery plan |



## 7.1  Missing / To-Be-Designed Screens (16)


55% of the 29 total screens are absent from the HighRadius wireframes and will be designed from scratch during the Sprint 0 design sprint:


| # | Screen Name | Persona | Phase | Complexity | Notes |
| --- | --- | --- | --- | --- | --- |
| 1 | Supplier Dashboard | Supplier | Phase 1 | High | Invoice pipeline, aging summary, payment status, tasks & alerts |
| 2 | Manager Dashboard | Supplier Manager | Phase 1 | High | Onboarding funnel, pending tasks, SLA metrics, quick-action panel |
| 3 | Screening Dashboard | Supplier Manager | Phase 1 | Medium | Aggregated compliance results across suppliers |
| 4 | Approval Worklist | Supplier Manager | Phase 1 | Medium | Task queue with approve/reject/reassign actions |
| 5 | Admin Settings | Admin | Phase 1 | High | Screening configuration, system parameters |
| 6 | User / Role Management | Admin | Phase 1 | High | Keycloak-integrated user creation, permission control |
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



## 7.2  Validation Gap Analysis (12)


Twelve validation types are specified in requirements but not illustrated in wireframes. All are documented in the Validation Error State Library — a Sprint 0 deliverable:


| # | Validation Type | Affected Screens | UX Spec Required |
| --- | --- | --- | --- |
| 1 | Email format validation (registration) | Supplier Registration | Inline error states |
| 2 | TIN format/checksum validation | Registration Form | Real-time feedback indicator |
| 3 | Bank account number format validation | Bank Details Form | Field-level error + toast |
| 4 | Required field enforcement (dynamic per tenant) | All form screens | Visual indicators + submit blocking |
| 5 | File type/size validation (document upload) | Document Upload | Error toast + supported format list |
| 6 | Duplicate supplier detection feedback | Invitation, Registration | Warning modal with existing supplier details |
| 7 | Approval chain completeness validation | Workflow Configuration | Pre-save validation + error summary |
| 8 | PO quantity bounds validation (partial invoicing) | PO Flip Screen | Inline error: “Cannot exceed PO quantity” |
| 9 | Invoice amount reconciliation validation | Invoice Creation | Warning when total deviates from PO |
| 10 | Date range validation (PO/invoice filters) | List screens | Inline date picker constraints |
| 11 | Session timeout/token expiry handling | All screens | Modal with re-login prompt |
| 12 | Concurrent edit conflict detection | Approval screens | Toast notification + refresh prompt |



## 7.3  Logic Complexity Gaps (7)


Seven areas where actual implementation complexity significantly exceeds what the wireframes convey — all scoped and estimated accordingly:


| # | Area | Wireframe Shows | Actual Complexity |
| --- | --- | --- | --- |
| 1 | Multi-level approval routing | Simple approve/reject | Conditional routing (spend threshold, region, category), SLA escalation, reassignment, delegation |
| 2 | Dynamic form configuration | Static form layout | Tenant-specific field ordering, validation rules, visibility conditions, multi-language labels, reusable templates |
| 3 | Bulk CSV onboarding | Single upload button | Duplicate detection, partial failure handling, progress tracking, error report download, rollback on critical failures |
| 4 | PO-to-Invoice flip | Simple mapping | Partial invoicing, line-item selection, tax/discount calculation, multi-currency, attachment inheritance |
| 5 | Screening orchestration | Sequential checks | 4 parallel checks with independent pass/fail, retry on timeout, partial result display, blocking vs. warning logic |
| 6 | Multi-tenant data isolation | Not shown | Schema-per-tenant resolution, JWT claim extraction, middleware enforcement, cross-tenant query prevention |
| 7 | ERP sync conflict resolution | Simple sync icon | Bi-directional sync handling, conflict detection (stale PO data), retry queues, dead-letter handling |



## 7.4  Missing API Endpoints (3)


Three API endpoints required for complete functionality are absent from the wireframes — all designed and included in the 58 vendor-built APIs:


| # | Endpoint | Purpose | Why Missing |
| --- | --- | --- | --- |
| 1 | Bulk invitation status tracking API | Track progress of CSV bulk imports | Wireframes show upload but not progress tracking |
| 2 | Screening retry/re-trigger API | Allow manual re-trigger of failed screening | Wireframes show results but not retry flow |
| 3 | Audit trail export API | Export filtered audit logs to CSV/PDF | Wireframes show audit screen but not export |



## 7.5  Technical Gaps (9)


Nine infrastructure and integration gaps not covered in wireframes — all mitigated through Sprint 0 architecture and design work:


| # | Gap | Impact | Mitigation |
| --- | --- | --- | --- |
| 1 | WebSocket infrastructure for real-time notifications | Required for live status updates and alerts | Design in Sprint 0; implement in Sprint 1 |
| 2 | File virus scanning integration | Required for secure document uploads | Integrate with ClamAV or S3 scanning in Sprint 0 |
| 3 | Multi-language label management system | Required for i18n form configuration | Design label store schema in Sprint 0 |
| 4 | Tenant provisioning automation | Required for admin tenant setup | Admin API + seed data scripts in Sprint 1 |
| 5 | Rate limiting and throttling configuration | Required for API security | API Gateway configuration in Sprint 0 |
| 6 | Health check and readiness probes | Required for Kubernetes deployment | Standard Spring Boot Actuator + custom checks |
| 7 | Database migration tooling (schema versioning) | Required for multi-tenant schema management | Flyway with tenant-aware migration strategy |
| 8 | Async job queue for long-running operations | Required for bulk imports, screening orchestration | Redis-backed job queue with status polling |
| 9 | Caching strategy for static/config data | Required for performance | Redis cache for form templates, workflow defs, i18n labels |



## 7.6  Workflow Gaps (6)


Six workflow scenarios not specified in the wireframes — all resolved through Sprint 0 design deliverables and documented in the UX specification:


| # | Workflow | Gap Description |
| --- | --- | --- |
| 1 | Invitation expiry and re-invite | Wireframes don’t specify: expiry period, re-invite flow, expired link handling |
| 2 | Draft save/resume lifecycle | Wireframes show save button but not: auto-save interval, draft expiry, resume from last step |
| 3 | Approval SLA escalation | Wireframes show approval but not: escalation triggers, notification chain, auto-approve on SLA breach |
| 4 | Supplier deactivation/reactivation | Not shown in wireframes — required for compliance (e.g., sanctions match after activation) |
| 5 | Master data change impact assessment | Wireframes show change form but not: which changes trigger re-screening, which require approval |
| 6 | Invoice rejection and resubmission | Wireframes show status but not: rejection reason capture, resubmission flow, version tracking |


Mitigation: Sprint 0 Validation Error State Library
A Validation Error State Library is delivered in Sprint 0 — all error messages, toast notifications, and inline validation indicators are documented before Sprint 1 begins. The Sprint 0 design sprint resolves all missing screens, with UX running 1 sprint ahead of development throughout the engagement. No gap remains unaddressed.