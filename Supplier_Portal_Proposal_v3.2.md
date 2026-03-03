# AP SUPPLIER PORTAL — ENTERPRISE PROPOSAL

| Field | Detail |
|-------|--------|
| Version | 3.3 |
| Date | February 28, 2026 |
| Client | HighRadius Corporation |
| Project | AP Supplier Portal Development & Deployment |
| Service Provider | Metapointer |
| Status | READY FOR SUBMISSION |

---

## Table of Contents

**PART I — PROPOSAL CONTEXT**
- 1. Cover Page
- 2. Document Control
- 3. Executive Summary
- 4. Business Understanding

**PART II — SOLUTION DESIGN**
- 5. Scope of Work
- 6. Solution Overview
- 7. Solution Architecture
- 8. Non-Functional Requirements

**PART III — ENGINEERING & DELIVERY**
- 9. DevOps & Release Management
- 10. Delivery Approach
- 11. Project Plan & Milestones
- 12. Team Structure

**PART IV — QUALITY & GOVERNANCE**
- 13. Quality Assurance Framework
- 14. Data Migration Strategy
- 15. Risk Management
- 16. Change Management Process

**PART V — SECURITY & SUPPORT**
- 17. Security & Compliance Controls
- 18. Documentation & Knowledge Transfer
- 19. Support & Warranty Model

**PART VI — COMMERCIAL & LEGAL**
- 20. Commercial Proposal
- 21. Legal & Contractual Terms
- 22. About Metapointer

---

## 1. Cover Page

**Classification: PROJECT-SPECIFIC**

- **Client:** HighRadius Corporation
- **Project:** AP Supplier Portal — Development & Deployment
- **Proposal Version:** 3.3
- **Date:** February 28, 2026
- **Prepared By:** Metapointer

---

## 2. Document Control

**Classification: STANDARD**

*[Standard section — to be populated with Metapointer standard template]*

---

## 3. Executive Summary

**Classification: PROJECT-SPECIFIC**

### 3.1 Business Context

HighRadius is a fintech enterprise SaaS provider offering an Agentic AI platform for the Office of the CFO. Its cloud solutions span the end-to-end Order-to-Cash (O2C) cycle, Accounts Payable, Treasury Management, Record-to-Report, and B2B Payments — integrating 180+ AI agents (microservices) to orchestrate financial processes. Adopted by over 1,100 leading companies (including 3M, Unilever, Procter & Gamble, and Johnson & Johnson), HighRadius is consistently recognized as a market leader by Gartner, IDC, and Forrester.

As part of its expanding AP automation capabilities, HighRadius requires a robust Supplier Portal to streamline vendor management operations across its customer base. The portal will serve as a unified platform for buyers to onboard suppliers, manage vendor relationships, and for suppliers to get onboarded, receive POs, submit and track invoices. This aligns with HighRadius's AI-first platform strategy and its mission to automate financial processes in multi-tenant environments handling diverse ERPs like SAP, Oracle, and NetSuite. By integrating with HighRadius's G4 platform, the portal will enhance AP efficiency, support acquisitions, and provide analytics-driven insights.

### 3.2 Problem Statement

Current AP operations at HighRadius rely on manual, fragmented processes that create significant operational and financial risk:

- **Onboarding Delays:** Email-based supplier onboarding takes 15–20 days with inconsistent data collection, processing 50–100+ suppliers per quarter with extended activation delays, lost early-payment discounts, and strained buyer-supplier relationships
- **Compliance Gaps:** Only ~30% of suppliers are screened, creating exposure to sanctions violations ($20M+ OFAC fines), tax/identity fraud from error-prone TIN verification, and banking vulnerabilities from unvalidated changes — with no centralized audit trails
- **Invoice Processing:** Manual channels (email/fax) yield only ~60% SLA compliance with high error rates, late penalties, and forecasting inaccuracies due to 12–15 manual touchpoints per event across hundreds to thousands of invoices monthly
- **Operational Inefficiency:** 60–70% of AP time spent on transactional work rather than strategic activities; 100% reliance on buyer intervention for every supplier interaction
- **Visibility & Data Silos:** Supplier data scattered across ERPs, spreadsheets, and emails — no single source of truth, manual reports, and delayed decision-making

### 3.3 Proposed Solution

The Supplier Portal is structured around **7 intelligent agents** (4 automated, 3 assisted) across three personas, delivering **29 screens + 11 modals** with **66 APIs** (58 vendor-built, 7 integrations, 1 orchestration) supporting **25+ core features**:

| Agent Name | Type | Key Capabilities |
|------------|------|-----------------|
| Supplier Onboarding | Automated | End-to-end invitation, dynamic multi-language form configuration, document upload/validation, draft save/resume |
| Supplier Screening | Automated | Real-time compliance verification — address, TIN, and sanctions checks in parallel |
| Bank Account Validation | Automated | Financial security through real-time bank details verification and ownership validation |
| Supplier Approval | Assisted | Multi-level approval workflows with configurable routing, SLA-based escalation |
| Master Data Change Approval | Assisted | Orchestrates approval workflows for master data updates with conditional routing |
| Purchase Order | Automated | ERP ingestion (multi-customer), acknowledgment/reject synchronization |
| Portal Invoice Creation | Assisted | Manual entry and PO-flip capability with validation, attachments, and AP synchronization |

**Technology Stack:**
- **Frontend:** React 18.x + HighRadius G4 DSL with WCAG 2.0 AA accessibility
- **Backend:** Spring Boot 3.x (Java 17+), microservices architecture
- **Database:** PostgreSQL OLAP with multi-tenant 100% data isolation (schema-per-tenant, row-level security)
- **Security:** Keycloak IAM integration, HashiCorp Vault secrets management, TLS 1.3, AES-256 encryption
- **Deployment:** Docker containers, Kubernetes orchestration in HighRadius G4 environment

**AI-Powered Productivity:** Leveraging Claude Opus AI for code generation, testing automation, and documentation, delivering 1.10x–1.50x productivity gains with 6 core engineers.

### 3.4 Timeline Summary

- **Kickoff:** March 2026
- **Sprint 0 (Foundation):** 2 weeks — architecture, DevOps setup, G4 component evaluation & scaffolding, design sprint
- **Phase 1 (MVP):** 4 agents (Onboarding, Screening, Bank Validation, Approval) — Sprints 1–5 (10 weeks) — UAT + 1 live customer by mid-May 2026
- **Phase 2:** 3 agents (Purchase Order, Portal Invoice Creation, Master Data Change Approval) — Sprints 6–9 (8 weeks) — Full delivery by early July 2026
- **Hypercare:** 6 months post-go-live through January 2027 with production support and knowledge transfer
- **Total Duration:** 20 calendar weeks aligned to RFP milestones with built-in risk buffers

### 3.5 Commercial Summary

- **Engagement Model:** Fixed-Price with defined scope and deliverables
- **Payment Structure:** Milestone-based with Go/No-Go gates (5 milestones: 20%–30%–20%–20%–10%)
- **Detailed Pricing:** Provided in separate Pricing Agreement document
- **Change Management:** Formal change control process for scope modifications

---

## 4. Business Understanding

**Classification: PROJECT-SPECIFIC**

### 4.1 Current State

HighRadius's current accounts payable (AP) operations are characterized by manual and fragmented supplier management processes, lacking a dedicated self-service portal:

- **Onboarding:** Primarily email-driven, involving unstructured workflows with inconsistent data collection and extended cycles of 15–20 days
- **Invoice Processing:** Relies on disparate channels (email, fax, manual entry), leading to ~60% SLA compliance and elevated error rates
- **Compliance:** Reactive and ad-hoc, with screening covering only ~30% of suppliers and no centralized audit trails
- **Supplier Interactions:** All interactions require full buyer intervention with no self-service capabilities for PO acknowledgment or invoice tracking
- **Data Management:** Scattered across ERPs (SAP, Oracle, NetSuite), spreadsheets, and emails — poor real-time visibility and manual reporting

This setup supports three main personas — Supplier Manager (handling invitations and workflows), Supplier (submitting documents manually), and HighRadius Admin/Client Admin (managing configurations) — but in an inefficient, non-digital manner.

### 4.2 Key Challenges

- **Manual Onboarding Delays:** Processing 50–100+ suppliers per quarter via email leads to activation delays, lost early-payment discounts, and strained buyer-supplier relationships
- **Invoice and PO Processing Inefficiencies:** Handling hundreds to thousands of invoices monthly through fragmented channels causes late penalties, forecasting inaccuracies, and high manual touchpoints (12–15 per event), diverting AP resources from strategic tasks
- **Compliance and Risk Gaps:** With ~70% of suppliers unscreened, there is significant exposure to regulatory violations (OFAC sanctions fines up to $20M+), tax/identity fraud from error-prone TIN verification, and banking fraud due to unvalidated changes — exacerbated by scattered audit trails
- **Lack of Self-Service and Scalability:** 100% reliance on buyer intervention hampers scaling, especially for multi-tenant environments or acquisitions, leading to high per-supplier costs and inability to absorb growth without proportional headcount increases
- **Data Fragmentation:** Siloed data across 3+ systems results in no single source of truth, manual reports, delayed decisions, and opportunity costs (60–70% of AP time on transactional work)

### 4.3 Compliance & Audit Risk Exposure

The absence of a dedicated supplier portal creates quantifiable compliance and financial risk:

| Risk Area | Current Exposure | Financial Impact |
|-----------|-----------------|-----------------|
| **Sanctions Risk** | ~70% of suppliers unscreened against OFAC, EU, and UN sanctions lists | Fines up to $20M+ per violation; reputational damage |
| **Tax/Identity Fraud** | Manual TIN verification is error-prone and inconsistent | Risk of incorrect 1099 reporting; IRS penalties and audit exposure |
| **Banking Fraud** | Bank account changes processed without automated validation | Primary BEC (Business Email Compromise) fraud vector; direct financial loss |
| **Audit Trail Gaps** | No centralized audit trail; actions scattered across emails, spreadsheets, and ERPs | Inability to demonstrate compliance during audits; regulatory penalties |

### 4.4 Cost of Inaction

| Dimension | Impact |
|-----------|--------|
| **Scaling Bottleneck** | Manual model requires linear headcount growth with supplier volume — unsustainable for multi-tenant, acquisition-driven growth |
| **Supplier Attrition** | Competitors with self-service portals offer better experience; risk of losing preferred suppliers to digitally mature alternatives |
| **Regulatory Exposure** | Compliance requirements are tightening (OFAC, GDPR, SOX); the cost of a single sanctions violation exceeds the entire portal investment |
| **Opportunity Cost** | 60–70% of AP team time spent on transactional work (data entry, follow-ups, manual routing) rather than strategic supplier relationship management |
| **Acquisition Integration Cost** | Each acquisition requires manual onboarding of supplier base — weeks of effort per acquisition vs. automated tenant provisioning |

### 4.5 Target State

The Supplier Portal will transform HighRadius's AP operations into a fully digitized, automated, and scalable ecosystem:

| Area | Current State | Target State |
|------|--------------|--------------|
| Supplier Onboarding | 15–20 days, email-driven | 3–5 days, automated with real-time screening |
| Screening Coverage | ~30% of suppliers screened | 100% automated compliance checks |
| Invoice SLA Compliance | ~60% | >90% with automated validation |
| First-Pass Accuracy | ~65% | >95% via PO-flip and field validation |
| Supplier Self-Service | 0% (full buyer intervention) | >80% adoption target |
| Manual Touchpoints | 12–15 per event | 80%+ reduction through automation |
| Audit Trail | Scattered across emails/spreadsheets | Centralized, immutable, 2-year retention |
| Data Visibility | Manual reports, delayed decisions | Real-time dashboards and KPI tracking |

### 4.6 Business Outcomes & ROI Indicators

The Supplier Portal is expected to deliver measurable business value across multiple dimensions:

| Outcome Area | Metric | Expected Impact |
|-------------|--------|----------------|
| Cost Savings | FTE equivalent saved through automation | 2–3 FTEs redirected from transactional to strategic work |
| Late Payment Penalties | Reduction in missed SLA penalties | Significant reduction through >90% SLA compliance |
| Compliance Risk | Non-compliant supplier exposure | Eliminated — 100% screening coverage with full audit trail |
| Supplier Satisfaction | Self-service adoption & onboarding speed | >80% adoption; 3–5 day onboarding vs 15–20 days |
| Scalability | Ability to absorb growth without headcount | Multi-tenant automation handles acquisitions without linear staffing |
| Data-Driven Decisions | Real-time visibility | KPI dashboards replace manual reports; proactive management |

**Value Realization Timeline:**
- **Months 1–3 (Post Go-Live):** Onboarding cycle reduction, screening automation, initial self-service adoption
- **Months 3–6:** Invoice SLA improvements, dashboard-driven decisions, supplier satisfaction gains
- **Months 6–12:** Full ROI realization — cost savings, compliance maturity, scalability proven through tenant expansion

### 4.7 Assumptions

- HighRadius will provide timely access to owned services and dependencies: Keycloak IAM, screening/bank validation APIs, ERP samples (SAP/Oracle/NetSuite), G4 platform for deployment, and test data/environments for UAT
- The RFP scope (7 agents, specified NFRs) remains fixed; changes managed through formal change control with impact assessments
- Weekly UX/UI sign-offs and stakeholder feedback will be provided by HighRadius to avoid design iteration delays
- Multi-tenancy requirements align with HighRadius standards for 100% data isolation with tenant resolution via JWT claims
- Project kickoff assumes March 2026 start, with no major external disruptions
- Performance testing will use production-scale datasets provided by HighRadius
- Product requirements and UX specifications will be provided by HighRadius as per RFP Section 5

### 4.8 Constraints

- **Platform Constraint:** All deployment must target HighRadius G4 containerized environment — no standalone infrastructure or alternative cloud hosting
- **Technology Constraint:** Frontend must use React 18.x with G4 DSL components; backend must use Spring Boot 3.x (Java 17+) per HighRadius engineering standards
- **Timeline Constraint:** March 2026 kickoff is non-negotiable; any delay in kickoff shifts all milestones proportionally
- **Team Size Constraint:** Fixed team of 7 FTE (6 engineers + 1 PM) — scope adjustments required if team availability changes
- **Scope Freeze Constraint:** RFP-defined scope (7 agents, 29 screens, specified NFRs) is frozen post-Sprint 0; changes require formal CR process with timeline/cost impact assessment
- **Integration Constraint:** Vendor has no control over HighRadius-owned services (Keycloak, screening APIs, bank validation, G4 platform) — delivery timelines depend on these services being available and stable
- **Compliance Constraint:** All code must pass HighRadius infosec clearance before production deployment; no exceptions for timeline acceleration

### 4.9 Dependencies (Client / Third Party)

| # | Dependency | Owner | Impact if Delayed | Mitigation |
|---|-----------|-------|-------------------|------------|
| D1 | Keycloak IAM environment provisioned and accessible | HighRadius | Blocks authentication development; delays Sprint 1+ | Mock IAM layer for dev; parallel integration once available |
| D2 | G4 DSL component library and documentation | HighRadius | Blocks frontend development; forces custom component builds | Evaluate OOB components in Sprint 0; fallback to plain React where needed |
| D3 | Screening service API (sanctions, TIN, address) | HighRadius | Blocks Supplier Screening agent | Stub/mock API responses for dev/QA; integrate when live |
| D4 | Bank validation API access | HighRadius / Third Party | Blocks Bank Account Validation agent | Same stub approach; validate with real API in UAT |
| D5 | ERP sample data (SAP/Oracle/NetSuite) for PO & Invoice | HighRadius | Blocks PO and Invoice agent development and testing | Generate synthetic test data; validate with real ERP data in UAT |
| D6 | UX wireframes / design specs for 16 undesigned screens | HighRadius | Forces vendor-designed screens; increases mismatch risk | Sprint 0 design sprint; UX 1 sprint ahead of dev |
| D7 | QA / UAT environment provisioned | HighRadius | Blocks testing phases; delays go-live | Use dev environment for early testing; escalate provisioning in Sprint 0 |
| D8 | Stakeholder availability for reviews & approvals | HighRadius | Delays sign-offs; blocks phase transitions | Define RACI in Sprint 0; escalation matrix for delayed responses |
| D9 | Infosec clearance review slots | HighRadius | Blocks production deployment | Submit for clearance early (during QA phase); parallel track |
| D10 | HashiCorp Vault access for secrets management | HighRadius | Blocks secure credential storage implementation | Use environment variables in dev; integrate Vault pre-UAT |

---

## 5. Scope of Work

**Classification: PROJECT-SPECIFIC**

### 5.1 In Scope

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

| Workflow/Feature | Screens | Complexity | Est. Hours/Screen | Total Hours |
|-----------------|---------|------------|-------------------|-------------|
| Supplier Onboarding | 6 | High | 40 | 240 |
| Supplier Screening | 3 | Medium | 35 | 105 |
| Bank Validation | 2 | Medium | 30 | 60 |
| Approval Workflows | 4 | High | 45 | 180 |
| PO Management | 5 | High | 40 | 200 |
| Invoice Management | 5 | High | 40 | 200 |
| Master Data Management | 2 | Medium | 35 | 70 |
| Dashboards | 2 | High | 50 | 100 |

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

- **Modals & Pop-ups Total: ~200 hours**
- **Screen Development Total: ~1,355 hours**

**Workflow/Feature Development (Backend Services):**

| Agent/Service | Workflows | Est. Hours/Workflow | Total Hours |
|---------------|-----------|---------------------|-------------|
| Supplier Onboarding Agent | 3 | 120 | 360 |
| Supplier Screening Agent | 2 | 100 | 200 |
| Bank Validation Agent | 1 | 80 | 80 |
| Supplier Approval Agent | 2 | 140 | 280 |
| Master Data Approval Agent | 2 | 120 | 240 |
| Purchase Order Agent | 3 | 130 | 390 |
| Portal Invoice Agent | 3 | 130 | 390 |

- **Agent/Service Development Total: ~1,940 hours**

#### Integrations

- Keycloak IAM for OIDC/SSO with RBAC/ABAC
- Screening APIs (address, TIN, sanctions) — parallel checks
- Bank validation API
- ERP/AP for PO/invoice sync (SAP/Oracle/NetSuite)
- Document storage (S3-compatible with virus scans)
- HashiCorp Vault for secrets management
- Notification services (email/WebSocket)
- Fault tolerance with circuit breakers, retries, and dead-letter queues

#### Testing & Quality Assurance

**Unit Testing:**

| Area | Target Coverage | Estimated Effort |
|------|----------------|-----------------|
| Frontend Unit Tests (React/Jest) | 80% coverage (RFP mandate) | ~5 weeks (QA) |
| Backend Unit Tests (JUnit) | 80% coverage (RFP mandate) | ~6 weeks (QA) |
| Regression Test Suite (JUnit) | Automated regression per RFP requirement | ~3 weeks (QA) |

**Integration & E2E Testing:**

| Area | Scope | Effort |
|------|-------|--------|
| Supplier Onboarding | Invite → Form fill → Screening → Approval → Activation (6 features) | ~4 weeks (QA) |
| Screening & Bank Validation (Integration) | Verify vendor orchestration calls HR screening/bank APIs correctly; validate result display and error handling | ~2 weeks (QA) |
| Approval Workflows | Multi-level onboarding approval, Master data change, Payment terms (3 features) | ~3 weeks (QA) |
| PO / Invoice Flows | PO import → Acknowledge → Flip to Invoice → Submit → AP Sync (7 features) | ~5 weeks (QA) |
| Document Management | Upload, Download, Delete, Version control, Bulk operations | ~1.5 weeks (QA) |
| Dashboard & Reporting | KPI calculations, Data aggregation, Drill-downs | ~1.5 weeks (QA) |
| Portal Cross-cutting Flows | Keycloak SSO token flow → RBAC → Multi-tenant isolation → Session mgmt | ~2 weeks (QA) |

**Performance & Load Testing:**

| Test Area | Benchmark | Effort |
|-----------|-----------|--------|
| API Response Time Validation | All APIs < 3 seconds (RFP requirement) | ~1.5 weeks (QA) |
| Grid Load Time | < 500ms for 1000 rows (NFR requirement) | ~1 week (QA) |
| Virtual Scrolling Stress | > 1000 rows, 30+ columns performance | ~1 week (QA) |
| Concurrent User Load | Simulate 100–500 concurrent suppliers | ~1.5 weeks (QA) |
| ERP Sync Throughput | PO import + Invoice sync under load | ~1 week (QA) |
| Horizontal Scaling Validation | Container scaling under G4 environment | ~1 week (QA) |

**Security Testing:**

| Security Area | Scope | Effort |
|---------------|-------|--------|
| Vulnerability Scanning (OWASP Top 10) | SAST + DAST scanning of all vendor-built endpoints | ~1.5 weeks (QA) |
| SSO Token Validation Testing | Keycloak token consumption, session handling, expiry edge cases | ~1 week (QA) |
| RBAC / Permission Boundary Testing | Role-based access enforcement across all 29 screens + 11 popups | ~1.5 weeks (QA) |
| Data Protection & Isolation | Multi-tenant data isolation verification, PII handling | ~1 week (QA) |
| CSP & Headers Validation | Content Security Policy, unsafe-eval prevention | ~3 days (QA) |
| HashiCorp Vault Integration Test | Key store operations, secret rotation | ~3 days (QA) |
| Infosec Clearance Prep | Documentation and remediation for HighRadius cybersecurity team | ~1 week (QA) |

**ABAC / RBAC Testing:**

| ABAC/RBAC Area | Scope | Effort |
|----------------|-------|--------|
| Role Matrix Validation | Supplier, Supplier Manager, Admin, Approver — all 29 screens + 11 popups | ~1.5 weeks (QA) |
| Access Boundary Enforcement | Cross-tenant data access prevention, Row-level security | ~1 week (QA) |
| Permission Escalation Testing | Ensure no privilege escalation via API manipulation | ~1 week (QA) |
| Multi-Tenant RBAC Isolation | Roles scoped to tenant, no cross-tenant role leakage | ~1 week (QA) |

#### Post-Deployment Support

- 6-month hypercare at 0.5 FTE
- Production monitoring and issue resolution per SLAs
- Weekly updates (email/call/PVA)
- Root cause analysis and knowledge transfer

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

### 5.2 Out of Scope

- **HighRadius-Owned Services Build:** Development or modification of Keycloak authentication/login/signup, bank validation service, screening services (address/TIN/sanctions), or G4 OOB components — vendor scope limited to integration effort only
- **Additional ERP Integrations:** ERP types beyond SAP/Oracle/NetSuite or custom multi-customer mappings exceeding RFP specs
- **Data Migration:** Migration of existing supplier data from ERPs, spreadsheets, or other legacy systems
- **Infrastructure Provisioning:** Hardware, cloud resources, or environment setup beyond containerized G4 deployment
- **Testing Exclusions:** Real-world production data testing (vendor uses mocks/samples); compliance certifications beyond SOX/GDPR support
- **Scope Changes:** Requirements exceeding defined scope without approved change requests, including major wireframe revisions after design sign-off

---

## 6. Solution Overview

**Classification: PROJECT-SPECIFIC**

### 6.1 Solution Vision

The Supplier Portal is a secure, scalable, self-service web application designed to digitize and streamline supplier onboarding, compliance validation, purchase order management, and invoice processing for HighRadius's AP automation platform.

**The solution aims to:**
- Eliminate manual, email-driven supplier interactions by providing a single system of engagement
- Enforce compliance and validation at the point of data entry through automated real-time checks
- Improve operational efficiency through automation, reducing onboarding cycles from 15–20 days to 3–5 days and invoice SLAs from ~60% to >90%
- Provide real-time visibility to suppliers and internal stakeholders via dashboards
- Support multi-tenant, enterprise-grade scalability with 100% data isolation

### 6.2 Capability Map

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

### 6.3 Transformation Vision — From Current State to Future State

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

### 6.4 High-Level Workflow

1. Supplier Manager sends onboarding invitation (individual or bulk via CSV)
2. Supplier completes self-registration: multi-step dynamic form, document upload, real-time validation, with draft save/resume and multi-language support
3. Automated compliance screening triggered: address, TIN, sanctions, and bank validation run in parallel with progress indicators
4. Submission enters approval workflow: multi-level, configurable routing with SLA-based escalation
5. Upon approval, supplier is activated, notified, and granted full portal access via Keycloak SSO
6. Supplier views/acknowledges/rejects POs (imported from ERPs), creates/submits invoices (manual or PO-flip)
7. Invoice and PO data syncs with ERP/AP systems with pre-submission field-level validation
8. Stakeholders track progress via real-time dashboards, notification center, and exportable reports

### 6.5 RFP Requirement Traceability

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

### 6.6 Persona Journeys

**Supplier Journey:**
- Receives email invitation with secure, time-limited link → completes multi-step registration → automated screening → approval workflow → dashboard access → PO management → invoice creation via PO-flip → status tracking

**Supplier Manager Journey:**
- SSO login → Manager Dashboard with pipeline metrics → send invitations (individual/bulk) → monitor worklist with status filters → review screening results → process approval tasks → track SLA compliance

**Admin Journey:**
- Configure onboarding forms (drag-and-drop builder, multi-language labels, reusable templates) → define approval workflows (chains, escalation rules, conditional routing) → manage users/roles via Keycloak → view audit trail (filterable, exportable)

---

## 7. Solution Architecture

**Classification: PROJECT-SPECIFIC**

### 7.1 Architecture Overview

The architecture follows a modular, layered approach designed to meet HighRadius NFRs: sub-3-second API responses, 100% multi-tenant data isolation, containerized G4 deployment, and Keycloak-based authentication. Clear separation between presentation, API gateway, service, integration, and data layers ensures maintainability and independent scalability.

### 7.2 Application Architecture

- **Presentation Layer:** React 18.x + G4 DSL, responsive SPA with role-based routing, WCAG 2.0 AA compliance, ARIA tags, virtual scrolling
- **API Gateway:** Request routing, JWT validation, tenant context injection, rate limiting
- **Service Layer:** Spring Boot 3.x microservices with stateless design supporting horizontal scaling; workflow-driven business logic for onboarding, approvals, and invoice processing
- **Integration Layer:** Adapter pattern with circuit breaker, retry, and dead-letter queues for all external system communication

### 7.3 Data Architecture

- **Multi-Tenancy Model:** Schema-per-tenant with shared infrastructure; each HighRadius customer gets an isolated PostgreSQL schema with row-level security policies
- **Common Schema:** Shared configuration (form templates, workflow definitions, i18n labels)
- **Tenant Resolution:** JWT claim (tenant_id extracted from Keycloak token) applied at middleware layer before any DB query
- **Core Entities:** Supplier, Invitation, Screening Result, Approval Workflow, Purchase Order, Invoice, Document, Audit Log
- **Strategy:** PostgreSQL OLAP with read replicas, Redis caching layer, immutable audit logs with 2-year retention

### 7.4 Integration Architecture

| External System | Integration Method | Ownership |
|----------------|-------------------|-----------|
| Keycloak IAM | OIDC/SSO, JWT validation, RBAC | HighRadius-owned; vendor integrates |
| Screening Services (Address/TIN/Sanctions) | REST API, parallel execution | HighRadius-owned; vendor integrates |
| Bank Validation Service | REST API | HighRadius-owned; vendor integrates |
| ERP Systems (SAP/Oracle/NetSuite) | REST API for PO import/invoice sync | Vendor builds adapter/orchestration |
| Document Storage | S3-compatible API with virus scanning | Vendor builds integration |
| HashiCorp Vault | Secrets management API | HighRadius-provided; vendor integrates |
| Notification Service | Email/WebSocket for real-time alerts | Vendor builds |

All integrations use fault tolerance patterns: circuit breaker, exponential retry, dead-letter queues.

### 7.5 Security Architecture

- **Authentication:** Keycloak SSO with OIDC/JWT; no request reaches business logic without validated token, tenant context, and role verification (zero-trust model)
- **Authorization:** Hybrid RBAC + ABAC — roles assigned in Keycloak (RBAC), runtime attributes for fine-grained control (ABAC)
- **Enforcement Points:** Frontend route guards → API Gateway JWT + RBAC middleware → Service Layer ABAC checks → Database tenant_id WHERE clause + row-level security → Audit logging of all decisions
- **Encryption:** TLS 1.3 in transit, AES-256 at rest
- **Secrets Management:** HashiCorp Vault for all credentials, API keys, certificates
- **Audit:** Immutable audit logs with full traceability — filterable by user, action, date; exportable for compliance

**Screen-Level Permission Matrix (29 Screens + 11 Modals):**

Permission levels: **Full** = view + all actions | **View** = read-only | **None** = no access | **Own** = own records only | **Config** = configuration only

| Screen / Area | Supplier | Supplier Manager | Approver | Admin |
|--------------|----------|-----------------|----------|-------|
| Supplier Dashboard | Full (Own) | None | None | None |
| Manager Dashboard | None | Full | View | View |
| Supplier Registration Form | Full (Own) | None | None | None |
| Supplier List / Worklist | Own | Full | View | View |
| Screening Dashboard | None | Full | View | View |
| Approval Worklist | None | View | Full | View |
| PO List | Full (Own) | View | None | None |
| PO Detail | Full (Own) | View | None | None |
| Invoice List | Full (Own) | View | None | None |
| Invoice Creation / PO Flip | Full (Own) | None | None | None |
| Form Builder | None | None | None | Config |
| Workflow Configuration | None | None | None | Config |
| User/Role Management | None | None | None | Full |
| Admin Settings | None | None | None | Config |
| Audit Trail | None | View | None | Full |
| Notification Center | Full (Own) | Full (Own) | Full (Own) | Full |
| Document Management | Full (Own) | Full | View | View |
| Master Data Change | Full (Own) | View | Full | View |

**Button-Level Visibility Rules:**

Key actions are controlled by role-based visibility rules. Examples:

| Button / Action | Supplier | Supplier Manager | Approver | Admin |
|----------------|----------|-----------------|----------|-------|
| Send Invitation | Hidden | Visible | Hidden | Visible |
| Bulk Upload (CSV) | Hidden | Visible | Hidden | Visible |
| Approve / Reject | Hidden | Hidden | Visible | Hidden |
| Reassign Approval | Hidden | Hidden | Visible | Visible |
| Create Invoice | Visible | Hidden | Hidden | Hidden |
| Acknowledge PO | Visible | Hidden | Hidden | Hidden |
| Configure Form Fields | Hidden | Hidden | Hidden | Visible |
| Export Audit Trail | Hidden | Visible | Hidden | Visible |

**RBAC / ABAC Enforcement Model (5-Layer Enforcement Chain):**

The system uses a hybrid RBAC + ABAC model. Roles are assigned in Keycloak (RBAC). Runtime attributes provide fine-grained control (ABAC):

| Layer | Enforcement Point | What It Checks | Failure Action |
|-------|-------------------|----------------|---------------|
| 1. Frontend | Route guards + component visibility | Role → show/hide routes, buttons, tabs | Hidden UI elements; redirect to dashboard |
| 2. API Gateway | JWT validation + RBAC middleware | Token validity, role claim, tenant_id | 401 Unauthorized / 403 Forbidden |
| 3. Service Layer | ABAC checks | Runtime attributes: ownership, tenant, status, threshold | 403 Forbidden with reason code |
| 4. Database | tenant_id WHERE clause + row-level security | Every query scoped to tenant; RLS policies enforced | Query returns empty set (no cross-tenant leakage) |
| 5. Audit | All access decisions logged | Every allow/deny decision recorded | Immutable audit trail for compliance |

**Multi-Tenant Access Isolation:**
- Tenant_id extracted from Keycloak JWT at API Gateway — injected into request context before any business logic
- Database middleware appends tenant_id filter to every query — no query reaches DB without tenant scope
- Row-level security (RLS) policies act as database-level safety net even if middleware is bypassed
- Cross-tenant API calls return 403 with no data leakage — validated in automated isolation tests

### 7.6 Deployment Architecture

- **Containerization:** Docker containers with Helm charts for Kubernetes orchestration
- **Environment Promotion:** Dev (local) → QA (auto on merge) → UAT (manual, QA sign-off) → Production (manual, UAT + HighRadius Engineering sign-off)
- **High Availability:** Redundant components, health checks, auto-scaling policies
- **G4 Platform:** Deployed within HighRadius G4 environment per RFP requirements

---

## 8. Non-Functional Requirements

**Classification: PROJECT-SPECIFIC**

### 8.1 Availability

- 99.5% system availability target
- Redundant components to minimize single points of failure
- Health checks and auto-restart policies
- Planned maintenance windows with minimal disruption

### 8.2 Performance

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

### 8.3 Scalability

- 1,000 concurrent users / 10,000 transactions per hour
- Horizontal scalability — frontend, backend, and integration layers scale independently
- Architecture supports onboarding additional tenants without impacting existing users
- Multi-tenant automation absorbs acquisitions without proportional headcount

### 8.4 Security

- Keycloak-based SSO with OIDC/JWT authentication
- RBAC/ABAC enforcement at every layer (zero-trust)
- TLS 1.3 for data in transit, AES-256 for data at rest
- HashiCorp Vault for secrets management
- OWASP Top 10 compliance
- Secure file handling with virus scanning for document uploads
- CSP headers and XSS protection

### 8.5 Compliance

- Full immutable audit trail for all onboarding, approval, and invoice actions
- 2-year audit log retention, filterable and exportable
- SOX/GDPR support alignment
- 100% screening coverage eliminating non-compliant supplier risk
- Data retention and traceability aligned with enterprise audit standards

### 8.6 Code Quality

- 80% minimum test code coverage (backend — JUnit, frontend — Jest)
- Static code analysis with no critical/high findings
- PR review policy: every merge requires at least 1 peer review
- Definition of Done includes: code complete, tests passing, reviewed, integration tested, security scanned, documented

---

## 9. DevOps & Release Management

**Classification: STANDARD CORE + PROJECT ADAPTATION**

*[Standard Metapointer CI/CD framework applies]*

**Project-Specific Adaptations:**
- CI/CD pipeline follows HighRadius engineering practices (per RFP Section 5)
- Deployment to HighRadius G4 containerized environment using Docker/Helm
- Environment promotion: Dev → QA (auto on merge) → UAT (manual, QA sign-off) → Production (manual, UAT + HighRadius Engineering sign-off)
- Rollback procedures defined for each deployment stage:

| Failure Type | Rollback Strategy | Estimated Recovery |
|-------------|-------------------|-------------------|
| Application bug (post-deploy) | Revert to previous container image via Helm rollback | < 5 minutes |
| Database schema migration failure | Execute pre-written rollback migration script | < 15 minutes |
| Integration failure (HR service) | Circuit breaker activates; fallback to cached/queued state | Automatic |
| Configuration error | Revert ConfigMap/Secret via version control | < 5 minutes |
| Full deployment failure | Automated rollback to last known good state | < 10 minutes |

- Pre-deployment checklist: all automated tests passing, code review completed, security scan passed (no high/critical), documentation updated, stakeholder approval obtained, rollback plan documented and tested
- Adherence to HighRadius cybersecurity policies during development

**Monitoring & Observability (Project-Specific):**

Production reliability requires comprehensive observability across application performance, logging, infrastructure metrics, and business KPIs. The observability stack integrates with HighRadius G4 platform capabilities.

| Observability Layer | Tools / Approach | What It Monitors |
|--------------------|-----------------|-----------------|
| **Application Performance** | APM integration (G4 platform compatible) | API response times, error rates, throughput, slow queries |
| **Structured Logging** | Centralized log aggregation (ELK/Fluentd) | Application logs, audit events, integration call traces |
| **Infrastructure Metrics** | Kubernetes-native monitoring (Prometheus/Grafana) | CPU, memory, disk, pod health, replica counts, network I/O |
| **Business KPIs** | Custom dashboards | Onboarding cycle time, screening pass rates, invoice processing SLA, approval queue depth |
| **Real-Time Alerting** | PagerDuty/OpsGenie integration | Technical incidents (P1/P2 auto-page), business anomalies (screening failure spike, queue backlog) |
| **Health Checks** | Kubernetes liveness + readiness probes | Every 5 minutes; auto-restart on failure; traffic routing on readiness |

---

## 10. Delivery Approach

**Classification: STANDARD CORE + PROJECT ADAPTATION**

*[Standard Metapointer Agile delivery methodology applies]*

**Project-Specific Adaptations:**
- **Engagement Model:** Fixed-Price with defined scope and milestone-based payments (10–15% scope variance allowance per RFP engagement model)
- **Sprint Cadence:** 2-week sprints (10 sprints total: Sprint 0 + Sprints 1–9)
- **Phase 1 (MVP):** Sprints 0–5 — 4 agents (Onboarding, Screening, Bank Validation, Approval)
- **Phase 2:** Sprints 6–9 — 3 agents (Purchase Order, Invoice Creation, Master Data Change Approval)
- **Communication Cadence:** Weekly status calls with HighRadius, weekly email updates and PVA (Product Velocity Analysis) on deliverables
- **Governance:** Steering committee reviews, defect management SLAs, change control per Section 16
- **Scope Variance Management:** Per RFP engagement model, a 10–15% variance in defined deliverables is acceptable. Variance is tracked sprint-over-sprint through story point velocity and backlog burn-down. Any variance exceeding 15% triggers the formal Change Request process (Section 16) with impact assessment on timeline and cost
- **MASC (Success Criteria):** (a) UAT delivery, (b) 1 live customer in production, (c) 90%+ KPI achievement per agent

**Agent-Level KPI Definitions (for MASC Milestone (c) — 90%+ Achievement Required):**

| Agent | KPI Metric | Target | Measurement Method |
|-------|-----------|--------|-------------------|
| Supplier Onboarding | % of invitations resulting in completed registrations | >90% | Completed registrations / total invitations sent (excluding expired) |
| Supplier Onboarding | Average onboarding cycle time (invitation to activation) | < 5 business days | Timestamp: invitation sent → supplier activated |
| Supplier Screening | % of submissions auto-screened without manual intervention | >95% | Auto-screened / total submissions (excluding HR service outages) |
| Supplier Screening | Average screening execution time | < 30 seconds | Timestamp: screening triggered → all 4 checks complete |
| Bank Account Validation | % of bank details validated on first submission | >90% | First-attempt validations passed / total validations |
| Supplier Approval | % of approvals completed within SLA | >90% | Approvals within SLA / total approvals (per configured SLA per tenant) |
| Supplier Approval | Average approval cycle time | < 2 business days | Timestamp: approval request created → final decision |
| Purchase Order | % of POs successfully imported from ERP | >95% | Successfully imported POs / total POs sent from ERP |
| Purchase Order | PO acknowledgment sync accuracy | >99% | Acknowledgment/reject status correctly synced to ERP / total syncs |
| Portal Invoice Creation | Invoice first-pass accuracy rate | >95% | Invoices accepted on first submission / total invoices submitted |
| Portal Invoice Creation | Average invoice creation time (PO-flip) | < 5 minutes | Timestamp: PO flip initiated → invoice submitted |
| Master Data Change | % of changes processed through workflow without error | >90% | Successfully processed changes / total change requests |
| Master Data Change | Average change approval cycle time | < 3 business days | Timestamp: change requested → approved/rejected |

- **Vendor Commitments per RFP Section 5:**
  - Design collaboration with HighRadius engineering team with timely sign-offs
  - Feature-level technical design documentation
  - Functional and regression test cases (JUnit + functional)
  - QA completed before delivery to HighRadius
  - Handover repository: GIT, design docs, KT sessions, all project resources
- **Sign-Off Gates:** Product Management (100% module/feature delivery), Engineering (architecture & handover), Infosec (cybersecurity clearance)

**Definition of Done — A feature/story is Done only when ALL criteria are met:**
1. **Code Complete:** Feature implementation finished, clean, follows coding standards, self-reviewed
2. **Unit Tests Written & Passing:** Minimum 80% coverage (Jest for frontend, JUnit for backend), all tests pass in CI
3. **Code Reviewed:** PR reviewed and approved by at least 1 peer (logic, security, performance, architecture)
4. **Integration Tested:** Feature works end-to-end across FE and BE; API contracts validated; HR service integration verified
5. **No Critical/High Bugs:** No open critical or high-severity bugs; medium/low documented and triaged
6. **Documentation Updated:** API documentation (Swagger), technical design doc, and runbooks updated
7. **Security Scanned:** SAST passed with no critical/high findings; CSP verified; RBAC/ABAC validated
8. **Deployed to QA:** Feature deployed via CI/CD and smoke tested
9. **Acceptance Criteria Met:** All criteria verified and demonstrated

**Defect Management Lifecycle (Project-Specific SLAs):**

All defects follow a standardized lifecycle from discovery through resolution and closure. The SLA targets below are project-specific commitments aligned to HighRadius's operational expectations and RFP requirements. These SLAs apply during the 20-week development phase (full team available). Post-go-live hypercare SLAs are defined in Section 19 (Support & Warranty Model).

| Severity | Description | Response SLA | Resolution SLA | Examples |
|----------|-------------|-------------|----------------|----------|
| P1 — Critical | System down or data loss | < 2 hours | < 8 hours | Portal inaccessible, data corruption, cross-tenant data leak |
| P2 — High | Major feature impaired, no workaround | < 4 hours | < 24 hours | Approval workflow broken, screening fails silently, PO sync error |
| P3 — Medium | Feature impaired, workaround available | < 8 hours | < 3 business days | Dashboard metrics incorrect, filter not working, UI alignment |
| P4 — Low | Cosmetic or minor enhancement | Next business day | Next sprint | Tooltip missing, color mismatch, minor label typo |

**Defect Metrics Tracked (reported weekly):**
- Open defect count by severity
- Defect aging (days open)
- Defect injection rate per sprint
- Defect leakage to UAT/production
- Mean time to resolution (MTTR) by severity

**Requirement Mismatch & UAT Rework Policy:**

When UAT or sprint demos reveal that a delivered feature does not match the requirement intent — even if it matches the written specification — a formal mismatch handling process is triggered. This is distinct from defects (where code is wrong) and scope changes (where requirements are new).

| Mismatch Category | Rework Cost |
|------------------|-------------|
| Specification was ambiguous and vendor interpreted reasonably | Vendor absorbs rework cost |
| HighRadius requirement changed after written sign-off | Change request required |
| UX spec not provided and vendor designed from scratch | Shared responsibility — 1 revision included; further revisions via CR |

**Prevention Strategy:** The 16 undesigned screens are the primary mismatch risk. Four preventive measures reduce mismatch probability by an estimated 70–80%:
1. Sprint 0 design sprint for all undesigned screens
2. UX running 1 sprint ahead of development throughout
3. Weekly design review sessions with HighRadius product team
4. Written confirmation of ambiguous requirements before coding begins

**Phase-Level Entry & Exit Criteria:**

| Phase | Entry Criteria | Exit Criteria |
|-------|---------------|--------------|
| Sprint 0 (Foundation) | Signed SOW; HighRadius API access granted; G4 environment available; UX wireframes provided | Architecture document signed off; CI/CD pipeline operational; G4 OOB component evaluation complete; Validation Error State Library created; DB schema v1 approved |
| Phase 1 Development (Sprints 1–5) | Sprint 0 exit criteria met; design sprint outputs approved; Keycloak integration environment ready | 4 agents feature-complete; 17 screens implemented; ~40 APIs deployed to QA; unit tests at 80% coverage |
| Phase 1 QA + UAT | All Phase 1 code merged to QA branch; test data provided by HighRadius; QA environment stable | E2E tests passing; API response <3s validated; Grid <500ms validated; WCAG audit passed; UAT sign-off from HighRadius; 1 live customer in production |
| Phase 2 Development (Sprints 6–9) | Phase 1 in production; Phase 2 design specs approved; ERP sample data for PO/Invoice flows available | 3 agents feature-complete; 12 screens implemented; ~26 APIs deployed to QA; unit tests at 80% coverage |
| Phase 2 QA + Stabilization | All Phase 2 code merged; full regression suite ready; performance test environment configured | Full regression passed; virtual scrolling stress test passed; penetration test completed; UAT feedback addressed |
| Full Delivery + Handover | Phase 2 UAT sign-off; all defects resolved or deferred with HighRadius approval | Production deployment complete; GIT handover accepted; KT sessions delivered; MASC criteria (a)(b)(c) achieved; infosec clearance obtained |

### 10.7 Communication & Reporting Plan

*[Standard Metapointer section — communication cadence, reporting formats, and escalation protocols to be populated from Metapointer standard template]*

---

## 11. Project Plan & Milestones

**Classification: PROJECT-SPECIFIC**

### 11.1 Phase Breakdown

**Sprint 0 — Foundation (Weeks 1–2):**
- Architecture finalization, design sprint for undesigned screens
- DevOps/CI-CD pipeline setup per HighRadius practices
- G4 OOB component evaluation and custom component scaffolding
- Validation Error State Library creation
- Integration environment setup with HighRadius APIs

**Phase 1 — MVP: Core Onboarding & Compliance (Sprints 1–5, Weeks 3–12):**
- Supplier Onboarding Agent (invitation, dynamic forms, document upload, draft/resume)
- Supplier Screening Agent (address, TIN, sanctions — parallel real-time checks)
- Bank Account Validation Agent (bank detail verification)
- Supplier Approval Agent (multi-level workflows, SLA escalation)
- Core dashboards (Supplier Dashboard, Manager Dashboard)
- Initial integrations (Keycloak, screening APIs, bank validation)
- UAT completion and 1 live customer in production

**Phase 2 — Transactional Enablement (Sprints 6–9, Weeks 13–20):**
- Purchase Order Agent (multi-ERP import, acknowledge/reject, sync)
- Portal Invoice Creation Agent (manual entry, PO-flip, AP sync)
- Master Data Change Approval Agent (update workflows)
- Enhanced reporting and analytics
- Full ERP synchronization
- Production-ready deployment and handover

**Hypercare & Stabilization (6 months post-go-live):**
- 0.5 FTE dedicated support rotating across team
- Production monitoring and issue resolution per SLAs
- Performance tuning and optimization
- Knowledge transfer to HighRadius operations team
- Weekly updates via email/call + PVA

### 11.2 Timeline

| Sprint | Weeks | Focus | Milestone |
|--------|-------|-------|-----------|
| Sprint 0 | 1–2 | Foundation, architecture, DevOps setup | Design Sign-off |
| Sprint 1–2 | 3–6 | Onboarding + Screening agents | — |
| Sprint 3–4 | 7–10 | Bank Validation + Approval agents + Dashboards | — |
| Sprint 5 | 11–12 | Integration testing, UAT prep | MVP UAT Complete |
| — | ~Mid-May 2026 | MVP Go-Live | **1 Live Customer** |
| Sprint 6–7 | 13–16 | PO Agent + Invoice Agent | — |
| Sprint 8–9 | 17–20 | Master Data Agent + Full integration + Hardening | Phase 2 UAT Complete |
| — | ~Early July 2026 | Full Portal Go-Live | **Full Delivery & Handover** |
| — | Jul 2026 – Jan 2027 | Hypercare | Hypercare Closure |

**Total Program Duration: 20 calendar weeks** (Sprint 0 through Handover) + 6 months hypercare

### 11.3 Calendar Estimates by Discipline

Based on actual team composition (3 FE + 2 BE + 1 QA, all with Claude Opus AI). All estimates are AI-adjusted:

| Discipline | Team Size | Working Days | Calendar Weeks | Notes |
|-----------|-----------|-------------|----------------|-------|
| Frontend Development | 3 developers | 72 days | ~15 weeks | Parallel execution across 3 devs; AI multiplier on code + unit tests |
| Backend Development | 2 developers | 77 days | ~16 weeks | Includes DevOps, observability; AI multiplier on services + APIs |
| QA Engineering | 1 engineer + Automation | ~28 person-weeks | ~17 weeks | Parallel test streams (BE + FE overlap Weeks 6–11); completes Week 17; unit tests written by devs |
| Sprint 0 (Foundation) | Full team | 10 days | 2 weeks | Architecture, design sprint, CI/CD setup, G4 component evaluation |

- Frontend and backend streams run in parallel, with QA overlapping dev from Week 3 through parallel test streams
- Critical path is backend at ~16 weeks, with frontend completing within the same window
- QA completes at Week 17 (regression + release hardening), providing 3-week handover buffer before program end

### 11.4 Timeline Reality Assessment

The HighRadius RFP defines three delivery milestones. Our honest assessment with a 7-person team:

| RFP Milestone | RFP Target | Our Realistic Target | Gap | Notes |
|--------------|-----------|---------------------|-----|-------|
| MVP (4 agents) | Feb 2026 | Mid-May 2026 | ~2.5 months | MVP and Phase 1 combined (both = 4 agents, 1 month apart in RFP) |
| Phase 1 (4 agents) | March 2026 | Mid-May 2026 | ~2 months | Treated as combined Phase 1/MVP delivery |
| Phase 2 (3 agents) | June 2026 | Early July 2026 | ~2–3 weeks | Mitigatable by overlapping FE/BE work streams across phases |

**Recommendation:** Deliver in two phases aligned to RFP agent structure. Phase 1 (4 agents) targets production by mid-May 2026 with 1 live customer. Phase 2 (3 agents) targets full delivery by early July 2026. The 2–3 week gap from the June RFP target is mitigatable by overlapping frontend/backend work streams. Total: 20 calendar weeks from kickoff.

### 11.5 Key Deliverables

| Phase | Calendar Window | Team | Deliverables |
|-------|----------------|------|-------------|
| Sprint 0 (Setup + Design) | Weeks 1–2 | All 7 engineers | CI/CD (following HR practices), G4 onboarding + OOB component evaluation, Keycloak + Vault setup, design system tokens, DB schema v1, Validation Error State Library |
| Phase 1 Development | Weeks 3–8 | 3 FE + 2 BE + 1 QA | 4 agents: Onboarding, Screening, Bank Validation, Approval. 17 screens, ~40 APIs |
| Phase 1 QA + UAT + Production | Weeks 9–12 | 3 FE + 2 BE + 1 QA | E2E testing, JUnit regression, perf validation (API<3s, Grid<500ms), WCAG audit, UAT, 1st live customer |
| Phase 2 Development | Weeks 13–16 | 3 FE + 2 BE + 1 QA | 3 agents: PO, Invoice, Master Data Change. 12 screens, ~26 APIs |
| Phase 2 QA + Stabilization | Weeks 17–18 | 3 FE + 2 BE + 1 QA | E2E testing, full regression, virtual scrolling perf test, pen test, UAT feedback |
| Full Delivery + Handover | Weeks 19–20 | 3 FE + 2 BE + 1 QA | Phase 2 production deploy, feature-level tech docs, GIT handover, KT, MASC milestone (c) |

**Cross-Phase Deliverables:**
- Security configuration and multi-tenant isolation
- CI/CD deployment pipelines per HighRadius practices
- Feature-level technical design documentation
- OpenAPI/Swagger API documentation
- Functional and regression test suites (JUnit + functional)
- Deployment guides and runbooks
- Knowledge transfer sessions

---

## 12. Team Structure

**Classification: STANDARD CORE + PROJECT ALLOCATION**

*[Standard Metapointer role descriptions and responsibilities apply]*

**Project-Specific Allocation:**

| Role | Count | FTE-Months | Project Focus |
|------|-------|------------|--------------|
| Architect / Technical Lead | 1 | 6 | System design, G4 integration, code quality, performance optimization |
| Senior Backend Engineers | 2 | 12 | Microservices, API implementation, database design, DevOps |
| Frontend Engineers | 2 | 12 | UI/UX with G4 DSL, responsive design, WCAG compliance |
| QA Engineer | 1 | 6 | E2E automation, performance testing, security validation, WCAG testing |
| Project Manager | 1 | 6 | Timeline management, stakeholder communication, risk tracking, PVA reporting |

**Total Team Capacity:** 7 FTE (6 months core development + extended hypercare phase at 0.5 FTE)

**Note:** Architect/Technical Lead contributes ~40% backend effort and ~20% frontend effort alongside dedicated engineers, giving effective capacity of 3 FE developers and 2.4 BE developers for calendar estimation purposes (see Section 11.3).

**AI Tooling:** All 6 engineers equipped with Claude Opus AI subscriptions for 1.10x–1.50x productivity gains across coding, testing, and documentation activities.

---

## 13. Quality Assurance Framework

**Classification: STANDARD**

*[Standard section — to be populated with Metapointer standard template]*

> *For detailed QA strategy, tool stack, test case plan, release controls, and quality metrics, refer to the **QA Strategy document**.*

---

## 14. Data Migration Strategy

**Classification: CONDITIONAL — PROJECT-SPECIFIC**

**Not Applicable.** Data migration of existing supplier data from ERPs, spreadsheets, or legacy systems is explicitly out of scope for this engagement. The Supplier Portal will start with fresh data, with suppliers onboarded through the new portal workflows.

---

## 15. Risk Management

**Classification: STANDARD FRAMEWORK + PROJECT RISKS**

*[Standard Metapointer risk methodology applies]*

**Project-Specific Risks:**

| # | Risk | Likelihood | Impact | Mitigation |
|---|------|-----------|--------|------------|
| 1 | **G4 Platform Integration Delays:** G4 OOB components or environment not ready on time | Medium | High | Early Sprint 0 integration testing; mock services as fallback; weekly sync with HighRadius platform team |
| 2 | **HighRadius API Instability:** Screening, bank validation, or Keycloak APIs unstable or undocumented | Medium | High | API contract validation in Sprint 0; adapter pattern with circuit breakers; fallback error handling |
| 3 | **Multi-Tenancy Complexity:** Data isolation errors or tenant configuration conflicts | Low | Critical | Schema-per-tenant design validation; automated isolation testing; row-level security enforcement |
| 4 | **Undesigned Screens (16 of 29):** 55% of screens require UX design from scratch before development | Medium | Medium | Sprint 0 design sprint; UX running 1 sprint ahead of development; weekly design reviews with HighRadius |
| 5 | **Workflow Configuration Complexity:** Complex approval chains causing routing conflicts | Low | Medium | Clear workflow design docs; validation before activation; escalation logic testing |
| 6 | **Performance at Scale:** Large PO/invoice datasets affecting grid performance | Medium | Medium | Virtual scrolling, pagination, query optimization, load testing before go-live |
| 7 | **ERP Integration Variability:** Different ERP formats/behaviors across SAP/Oracle/NetSuite | Medium | Medium | Adapter pattern per ERP; early integration with sample data; dedicated Sprint 0 API mapping |
| 8 | **Regulatory/Compliance Changes:** Updated sanctions lists or compliance requirements mid-project | Low | Medium | Modular validation architecture; configurable rule engine; decoupled screening service |
| 9 | **User Adoption Risk:** Low supplier adoption of self-service portal | Low | Medium | Intuitive UX design, onboarding communication templates, dashboard visibility, training support |
| 10 | **Requirement Mismatch at UAT:** Delivered features not matching requirement intent despite matching spec | Medium | Medium | Sprint 0 design sprint + UX 1 sprint ahead + weekly design reviews + written confirmation of ambiguous requirements |
| 11 | **Disaster Recovery / Data Loss:** Infrastructure failure, data corruption, or security breach in production | Low | Critical | Backup strategy, DR scenarios, BCP procedures (see below) |

**Disaster Recovery & Business Continuity:**

| DR Component | Strategy |
|-------------|----------|
| **Database Backups** | Automated daily full backups + continuous WAL (Write-Ahead Log) archiving; point-in-time recovery capability; backups stored in separate availability zone |
| **Application State** | Stateless microservices — no in-memory state to recover; Kubernetes handles pod replacement automatically |
| **Configuration & Secrets** | HashiCorp Vault with HA configuration; Helm charts and infrastructure-as-code in version control; reproducible deployments |
| **Document Storage** | S3-compatible storage with cross-region replication; versioning enabled for all uploaded documents |

**Disaster Recovery Scenarios:**

| Scenario | RTO (Recovery Time) | RPO (Recovery Point) | Recovery Procedure |
|----------|-------------------|---------------------|-------------------|
| Single pod/container failure | < 1 minute | Zero data loss | Kubernetes auto-restart; health check detects and replaces |
| Database primary failure | < 15 minutes | < 1 minute (WAL) | Automatic failover to read replica; promote to primary |
| Full cluster failure | < 1 hour | < 5 minutes | Restore from backup; redeploy via Helm charts; DNS failover |
| Data corruption (logical) | < 2 hours | Point-in-time | PostgreSQL PITR to pre-corruption timestamp; validate data integrity |
| Security breach | < 4 hours | Varies | Isolate affected systems; rotate all credentials via Vault; forensic analysis; restore from clean backup |

**Business Continuity Plan:**
- **Incident Detection:** Automated monitoring alerts (PagerDuty/OpsGenie), user-reported incidents via support portal, regular health checks every 5 minutes
- **Incident Response:** Activate on-call engineer → assess severity per SLA tiers → execute recovery per scenario matrix → communicate with stakeholders via pre-defined escalation channels
- **Post-Incident:** Root cause analysis (RCA) within 48 hours of resolution. Implement preventive measures. Update runbooks and documentation. Blameless post-mortem shared with HighRadius engineering team

---

## 16. Change Management Process

**Classification: STANDARD**

*[Standard section — to be populated with Metapointer standard template]*

---

## 17. Security & Compliance Controls

**Classification: STANDARD CORE + PROJECT ADAPTATION**

*[Standard Metapointer security controls apply]*

**Project-Specific Adaptations:**
- **Access Control:** Keycloak integration with hybrid RBAC/ABAC model; 4 personas (Supplier, Supplier Manager, Approver, Admin) with screen-level and button-level permissions across 29 screens + 11 modals
- **Encryption:** TLS 1.3 in transit, AES-256 at rest; HashiCorp Vault for all secrets management per HighRadius security requirements
- **Audit Logging:** Immutable audit trail for all portal actions — onboarding, screening, approvals, invoice submissions; filterable by user, action type, date; exportable for compliance; 2-year retention
- **Multi-Tenant Isolation:** Schema-per-tenant with row-level security; tenant_id enforced at middleware layer before any database query; JWT-based tenant resolution
- **Regulatory Alignment:** SOX/GDPR support; OFAC sanctions screening compliance; 100% supplier screening coverage; OWASP Top 10 compliance
- **Adherence to HighRadius cybersecurity policies** during development per RFP Section 5
- **Infosec Clearance Process:**

| Phase | Activity | Timeline | Owner |
|-------|----------|----------|-------|
| Pre-Development | Security architecture review with HighRadius infosec team | Sprint 0 | Vendor + HR Infosec |
| During Development | Continuous SAST scanning in CI/CD pipeline; no critical/high findings allowed to merge | Every sprint | Vendor |
| Pre-UAT | Comprehensive security assessment: OWASP Top 10, RBAC/ABAC validation, tenant isolation testing | Sprint 5 (Phase 1), Sprint 9 (Phase 2) | Vendor |
| Pre-Production | Formal infosec review submission to HighRadius cybersecurity team; remediation of findings | 2 weeks before each go-live | Vendor + HR Infosec |
| Sign-Off | HighRadius infosec clearance certificate as production deployment gate | Required before each go-live | HR Infosec |

Remediation SLA: Critical findings resolved within 48 hours; High findings within 1 sprint; Medium/Low tracked and resolved before final handover

---

## 18. Documentation & Knowledge Transfer

**Classification: STANDARD**

*[Standard section — to be populated with Metapointer standard template]*

---

## 19. Support & Warranty Model

**Classification: STANDARD CORE + PROJECT TERMS**

*[Standard Metapointer support structure applies]*

**Project-Specific Terms:**
- **Hypercare Duration:** 6 months post-go-live (approximately July 2026 – January 2027)
- **Hypercare Staffing:** 0.5 FTE dedicated support resource rotating across the 6-person engineering team (~13 weeks of part-time effort)
- **Support SLAs:**
  - P1 (Critical — system down): < 4 hours response
  - P2 (High — major feature impaired): < 8 hours response
  - P3 (Medium — workaround available): < 24 hours response
  - P4 (Low — cosmetic/minor): Next business day
- **Reporting:** Weekly updates via email/call and PVA (Product Velocity Analysis) on deliverables per RFP Section 5
- **Escalation Matrix:**

| Tier | Scope | Timeframe | Auto-Escalation Rule | Personnel |
|------|-------|-----------|---------------------|-----------|
| Tier 1 — Technical | Bug fixes, configuration, environment issues | 24 hours | If unresolved after 24h → auto-escalate to Tier 2 with notification to both PMs | Engineering team lead |
| Tier 2 — Management | Cross-team blockers, resource conflicts, priority disputes | 48 hours | If unresolved after 48h → auto-escalate to Tier 3 with incident brief | Project Managers (both sides) |
| Tier 3 — Executive | Contractual issues, scope disputes, critical failures | Per agreement | Executive review with formal incident report | Delivery heads / stakeholders |

All escalations logged in Jira with timestamps and resolution notes
- **Handover Repository:** GIT repository, design documents, KT sessions, deployment runbooks, and all resources used for the product per RFP Section 6

---

## 20. Commercial Proposal

**Classification: PROJECT-SPECIFIC**

### 20.1 Pricing Structure

**Engagement Type:** Fixed-Price Development & Deployment

**Scope Coverage:**
- Complete development, testing, and deployment of 7 intelligent agents (4 automated, 3 assisted)
- 29 screens + 11 modals with responsive design and WCAG 2.0 AA accessibility
- 66 APIs (58 vendor-built, 7 integrations, 1 orchestration)
- 6-month hypercare support
- Knowledge transfer and team enablement
- All team costs and AI tooling (6 Claude Opus subscriptions)

**Quality Guarantees:**
- 80% code coverage (backend and frontend)
- < 3 second API response time (P95)
- 99.5% system availability
- 90%+ KPI achievement at agent level

*FYI — Detailed pricing breakdown and payment milestone schedule are provided in the Pricing Agreement (separate document).*

### 20.2 Milestone Payment Plan

| Milestone | Description | Payment % |
|-----------|-------------|-----------|
| M0 | Project Kickoff & Design Approval | 20% |
| M1 | MVP Development Complete (UAT Ready) | 30% |
| M2 | MVP Go-Live (1 Live Customer) | 20% |
| M3 | Phase 2 UAT Complete | 20% |
| M4 | Full Project Completion & Handover | 10% |

**Project-Specific Payment Terms:**
- Net 30 days from invoice date
- Monthly invoices for ongoing hypercare
- Late payment penalty: 1.5% per month on overdue amounts

### 20.3 Invoicing Terms

*[Standard Metapointer section — standard invoicing terms, currency, tax treatment, and billing procedures to be populated from Metapointer standard template]*

### 20.4 Assumptions

- Pricing based on defined RFP scope (7 agents, 29 screens, 66 APIs, specified NFRs) with 10–15% scope variance allowance per RFP engagement model
- Scope variance within 10–15% is absorbed within the fixed price; variance exceeding 15% is managed through formal Change Request process
- External services (screening, bank validation, IAM) available and stable
- ERP integration APIs accessible and documented
- Required stakeholders available for timely review and approvals
- Multi-tenant architecture follows agreed design patterns
- Any deviation from these assumptions may impact cost and timeline

### 20.5 Change Billing Model

**Baseline Scope:** 7 intelligent agents (4 automated, 3 assisted), 29 screens + 11 modals, 66 APIs (58 vendor-built, 7 integrations, 1 orchestration), 25+ core features

**Change Management Process:**
1. **Change Request Submission:** HighRadius submits change request with business justification
2. **Impact Assessment:** Metapointer provides detailed analysis within 3 business days (technical feasibility, schedule impact, resource requirements, cost implications)
3. **Change Advisory Board (CAB) Review:** HighRadius approves, defers, or rejects change
4. **Change Order:** If approved, formal change order signed with cost and schedule adjustments
5. **Billing:** Cost adjustment deducted from final payment or invoiced separately per change order

---

## 21. Legal & Contractual Terms

**Classification: STANDARD**

*[Standard section — to be populated with Metapointer standard template]*

---

## 22. About Metapointer

**Classification: STANDARD**

*[Standard section — to be populated with Metapointer standard template]*

---

**Prepared By:** Metapointer
**For:** HighRadius Corporation
**Date:** February 28, 2026
