# AP SUPPLIER PORTAL — QUALITY ASSURANCE & TEST STRATEGY

| Field | Detail |
|-------|--------|
| **Document** | Quality Assurance & Test Strategy |
| **Version** | 3.3 |
| **Date** | February 28, 2026 |
| **Client** | HighRadius Corporation |
| **Project** | AP Supplier Portal Development & Deployment |
| **Service Provider** | Metapointer |
| **Status** | READY FOR SUBMISSION |

> **Confidentiality Notice:** This document contains proprietary and confidential information. Distribution is restricted to authorized HighRadius and Metapointer personnel only.

> **Cross-References:**
> - Executive Summary & Business Understanding → *Proposal PDF document*
> - Scope of Work, Deliverables & Testing Summary → *Scope of Work document*
> - Timeline, Milestones & Delivery Approach → *Timeline document*
> - Solution Architecture & Security → *Tech Specs document*
> - Commercial Terms, SLAs & Hypercare → *Commercial Agreement document*

---

## Table of Contents

1. [Quality Approach](#1-quality-approach)
   - 1.1 [Governance Alignment](#11-governance-alignment)
   - 1.2 [QA Tool Stack](#12-qa-tool-stack)
2. [Program Scope Coverage](#2-program-scope-coverage)
3. [Test Strategy](#3-test-strategy)
   - 3.1 [Backend Testing](#31-backend-testing)
   - 3.2 [Frontend Testing](#32-frontend-testing)
   - 3.3 [End-to-End Automation](#33-end-to-end-automation)
   - 3.4 [Performance & Load Testing](#34-performance--load-testing)
   - 3.5 [Security & Compliance Testing](#35-security--compliance-testing)
4. [Defect Management](#4-defect-management)
5. [Release Controls](#5-release-controls)
6. [Quality Metrics](#6-quality-metrics)
7. [QA Delivery Timeline](#7-qa-delivery-timeline)
8. [Test Case Plan & Traceability](#8-test-case-plan--traceability)
   - 8.1 [Test Case Design Model](#81-test-case-design-model)
   - 8.2 [Estimated Test Case Volume](#82-estimated-test-case-volume)
   - 8.3 [Requirements Traceability Matrix](#83-requirements-traceability-matrix)
   - 8.4 [Test Case Lifecycle](#84-test-case-lifecycle)
   - 8.5 [Entry & Exit Criteria](#85-entry--exit-criteria)

---

## 1. Quality Approach

**Classification: PROJECT-SPECIFIC**

### 1.1 Governance Alignment

This Quality Strategy aligns with:

- HighRadius engineering and CI/CD standards
- Contractual SLA commitments (P1–P4 model) as defined in the **Commercial Agreement document**
- Scope of Work security and compliance obligations as defined in the **Scope of Work document**
- Technical architecture (Spring Boot 3.x, React 18.x, multi-tenant design) as defined in the **Tech Specs document**

CI/CD execution follows HighRadius-approved pipeline standards per RFP Section 5.

### 1.2 QA Tool Stack

Where tools are not mandated by HighRadius, the following validated stack is proposed. Final tool selection is subject to HighRadius engineering approval:

| Category | Tool | Version | Notes |
|----------|------|---------|-------|
| Frontend Unit Testing | Jest | 29.7.0 | Developer responsibility; 80% coverage target |
| Backend Unit Testing | JUnit 5 + Mockito | — | Developer responsibility; 80% coverage target |
| Backend Integration | Testcontainers + WireMock | — | Container-based and mock-based integration testing |
| E2E Automation | Playwright | 1.49.0 | Subject to HighRadius approval; fallback to Cypress/Selenium if required |
| Performance Testing | Artillery | 2.0.21 | Subject to HighRadius approval; fallback to JMeter/Gatling if required |
| Defect Tracking | Jira | — | Per HighRadius standard |
| Application Monitoring | Sentry | 10.x | Subject to HighRadius approval; fallback to HighRadius-standard APM |
| Infrastructure Monitoring | Prometheus / Grafana | — | Per HighRadius standard |
| Logging | ELK / Fluentd | — | Per HighRadius standard |
| Alerting | PagerDuty / OpsGenie | — | Per HighRadius standard |

> *Unit tests (Jest for frontend, JUnit for backend) are developer responsibilities — written alongside feature code and included in FE/BE capacity. QA owns E2E, integration, performance, security, and regression testing. See **Scope of Work document** for effort breakdown.*

---

## 2. Program Scope Coverage

**Classification: PROJECT-SPECIFIC**

This strategy governs validation of:

| Scope Item | Count | Validation Approach |
|-----------|-------|-------------------|
| Application Screens | 29 | Functional E2E, persona-based access, WCAG 2.0 AA |
| Modal Workflows | 11 | Trigger validation, form logic, parent-screen integration |
| APIs | 66 (58 vendor-built, 7 integrations, 1 orchestration) | Functional, negative, tenant enforcement, failure injection |
| Personas | 4 (Supplier Manager, Supplier, HR Admin, Client Admin) | RBAC/ABAC matrix validation across all screens and actions |
| Intelligent Agents | 7 (4 automated, 3 assisted) | Agent-level KPI validation per **Scope of Work document** |

The financial and approval-driven nature of the portal requires strict validation of data integrity, workflow routing, escalation logic, and tenant isolation.

> *For complete scope details (screen breakdown, API ownership, gap analysis), refer to the **Scope of Work document**.*

---

## 3. Test Strategy

**Classification: PROJECT-SPECIFIC**

### 3.1 Backend Testing

**Stack:** Spring Boot 3.x — Java 17+ | JUnit 5 + Mockito + Testcontainers + WireMock

**Coverage Requirement:**
- 80% overall code coverage (RFP mandate)
- Target 100% coverage for financial/invoice logic modules (subject to feasibility)

**Validated Areas:**

| Area | Scope |
|------|-------|
| API Validation | All 66 APIs — functional, negative, boundary |
| External Integrations | 7 integration points — screening, bank validation, ERP, Keycloak, Vault, S3, notification |
| Fault Tolerance | Circuit breaker, retry logic, dead-letter queue handling |
| Database | Flyway schema migrations, schema-per-tenant isolation, row-level security |
| Security | JWT tenant validation, Vault integration, cross-tenant prevention |
| Failure Injection | ERP timeout simulation, screening API failures, bank validation unavailability, external dependency downtime |

**Performance Benchmark:** API response time < 3 seconds (P95)

### 3.2 Frontend Testing

**Stack:** React 18.x + G4 DSL | Jest 29.7.0 + Playwright 1.49.0

**Coverage Requirement:** 80% unit test coverage (RFP mandate)

**Validated Scope:**

| Area | Scope |
|------|-------|
| Screens | All 29 screens — functional, responsive, persona-based access |
| Modals | All 11 modals — trigger logic, form validation, parent integration |
| Form Builder | Dynamic form configuration, field validation, multi-language |
| Workflow Config | Approval chain configuration, routing preview |
| Dashboards | KPI calculations, data accuracy, real-time updates |
| Accessibility | WCAG 2.0 AA compliance — ARIA tags, keyboard navigation, screen reader |

**Performance Benchmark:** Grid rendering < 500ms (1,000+ rows with virtual scrolling)

### 3.3 End-to-End Automation

**Automated Critical Journeys:**

| Journey | Flow |
|---------|------|
| Supplier Onboarding | Invitation → Registration → Form Fill → Screening → Bank Validation → Approval → Activation |
| PO Lifecycle | PO Import → Acknowledge → PO Flip to Invoice |
| Invoice Lifecycle | Invoice Creation → Validation → Approval → ERP Sync |
| Master Data Change | Change Request → Approval Workflow → Master Data Update |
| SLA Escalation | SLA breach detection → Auto-escalation → Notification |
| Month-End Processing | High-volume invoice/PO processing under load |

**Quality Gate:** Flaky test threshold < 3%. Tests exceeding threshold are quarantined and fixed before next sprint.

### 3.4 Performance & Load Testing

**Tool:** Artillery 2.0.21 (subject to HighRadius approval)

| Test Type | Scope | Pass Criteria |
|-----------|-------|--------------|
| Load Testing | 100–500 concurrent users, standard workflows | API < 3s, Grid < 500ms |
| Stress Testing | Beyond expected capacity, identify breaking points | Graceful degradation, no data loss |
| Soak Testing | 8-hour sustained load | No memory leaks, stable response times |
| Month-End Simulation | Peak invoice/PO volume, ERP sync throughput | SLA maintained under peak load |

Release blocked if SLA benchmarks are breached.

> *For performance NFRs and quality guarantees, refer to the **Scope of Work document** (NFR section) and the **Commercial Agreement document** (quality guarantees).*

### 3.5 Security & Compliance Testing

| Area | Validation Scope |
|------|-----------------|
| OWASP Top 10 | SAST + DAST scanning of all vendor-built endpoints |
| CSP & Headers | Content Security Policy verification, security header validation |
| Injection Testing | XSS, SQLi, command injection across all input surfaces |
| JWT Security | Token tampering, expiry handling, invalid signature rejection |
| Cross-Tenant Access | Tenant isolation verification — API-level and database-level |
| Virus Scanning | Document upload validation via S3-compatible storage |
| Vault Integration | HashiCorp Vault credential retrieval, rotation, access control |
| RBAC/ABAC Matrix | 4 personas x 29 screens + 11 modals — role permission validation |

Infosec clearance from HighRadius cybersecurity team required before production deployment.

> *For detailed security architecture and RBAC enforcement model, refer to the **Tech Specs document** (Security Architecture section).*

---

## 4. Defect Management

**Classification: PROJECT-SPECIFIC**

**System of Record:** Jira

**Development-Phase SLAs:**

| Severity | Description | Response SLA | Resolution SLA | Examples |
|----------|-------------|-------------|----------------|----------|
| P1 — Critical | System down or data loss | < 2 hours | < 8 hours | Portal inaccessible, data corruption, cross-tenant data leak |
| P2 — High | Major feature impaired, no workaround | < 4 hours | < 24 hours | Approval workflow broken, screening fails silently, PO sync error |
| P3 — Medium | Feature impaired, workaround available | < 8 hours | < 3 business days | Dashboard metrics incorrect, filter not working, UI alignment |
| P4 — Low | Cosmetic or minor enhancement | Next business day | Next sprint | Tooltip missing, color mismatch, minor label typo |

These SLAs apply during the 20-week development phase (full team available). Post-go-live hypercare SLAs are defined in the **Commercial Agreement document**.

**Defect Governance:**
- All P1 defects require Root Cause Analysis (RCA) and regression test update before closure
- All P1/P2 defects require regression update before closure
- MTTD (Mean Time to Detect) and MTTR (Mean Time to Resolve) tracked per sprint

---

## 5. Release Controls

**Classification: PROJECT-SPECIFIC**

Release to production requires all of the following gates to be passed:

| Gate | Criteria |
|------|----------|
| Code Coverage | >= 80% (backend — JUnit, frontend — Jest) |
| API Validation | All 66 APIs validated — functional + negative + tenant isolation |
| Agent Validation | All 7 agents validated against KPI targets |
| Tenant Isolation | Schema-per-tenant + RLS verified; cross-tenant access tests passed |
| API Performance | All APIs < 3s response time (P95) |
| Grid Performance | Grid rendering < 500ms (1,000+ rows) |
| OWASP Compliance | SAST + DAST complete with no critical/high findings |
| Accessibility | WCAG 2.0 AA validated |
| Defect Status | No open P1/P2 defects |
| Infosec Clearance | HighRadius cybersecurity team sign-off obtained |
| Month-End Simulation | Peak-volume scenario validated before go-live |
| Rollback Validation | Rollback procedure tested and documented |

> *For deployment promotion pipeline (Dev → QA → UAT → Prod) and rollback strategy, refer to the **Timeline document** (DevOps & Release Management section).*

---

## 6. Quality Metrics

**Classification: PROJECT-SPECIFIC**

The following metrics are reported per sprint:

| Metric | Target | Reporting |
|--------|--------|-----------|
| Code Coverage % | >= 80% | Per sprint |
| Flaky Test % | < 3% | Per sprint |
| API SLA Compliance | 100% of APIs < 3s | Per sprint |
| Grid SLA Compliance | < 500ms rendering | Per sprint |
| MTTD (Mean Time to Detect) | Tracked | Per sprint |
| MTTR (Mean Time to Resolve) | Tracked | Per sprint |
| Defect Escape Rate | Tracked | Per sprint |
| Release Stability | Tracked | Per release |
| OWASP Findings | Zero critical/high | Per security scan |
| Tenant Validation Results | 100% isolation | Per sprint |

> *For sprint reporting cadence and PVA (Product Velocity Analysis), refer to the **Timeline document** (Communication & Reporting section).*

---

## 7. QA Delivery Timeline

**Classification: PROJECT-SPECIFIC**

**Team:** 1 QA Engineer + Automation tooling | **Committed Duration:** 17 calendar weeks | **Effort:** ~28 person-weeks

| QA Phase | Program Weeks | Activities |
|----------|--------------|------------|
| Setup & Framework | 1–2 | Automation framework init, CI integration, RBAC matrix prep, test data modeling |
| Backend Validation | 3–8 | 66 APIs + 7 integrations: functional, negative, tenant enforcement, failure injection |
| Frontend + E2E Automation | 6–11 | 29 screens, 11 modals, persona-based access, critical journey automation |
| Integration Hardening | 9–11 | Deep failure simulation, circuit breaker/retry validation |
| Performance Validation | 12–14 | Load, stress, 8-hour soak, month-end simulation |
| Security & Compliance | 13–15 | OWASP, JWT tampering, tenant cross-access, CSP, WCAG 2.0 AA |
| Regression & Release | 15–17 | Full regression cycles, UAT support, release hardening, go-live readiness |

- QA execution begins Week 1 (setup/framework) and completes Week 17 (regression + release hardening), providing a 3-week handover buffer before program end at Week 20
- ~28 person-weeks fit into 17 calendar weeks through overlapping test streams (backend validation + frontend E2E run concurrently Weeks 6–11; performance + security overlap Weeks 13–15)
- Scope is not reduced under this timeline

> *For program-level timeline (Sprint 0, Phase 1, Phase 2, Hypercare) and team structure, refer to the **Timeline document**. For QA effort breakdown by test area, refer to the **Scope of Work document** (Testing & Quality Assurance section).*

---

## 8. Test Case Plan & Traceability

**Classification: PROJECT-SPECIFIC**

### 8.1 Test Case Design Model

Test cases are designed using:

- **Requirement-based testing** — mapped to RFP requirements and user stories
- **Risk-based prioritization** — financial workflows, compliance, and tenant isolation prioritized
- **Persona validation** — all 4 personas tested across applicable screens and actions
- **Positive & negative flows** — happy path + error handling, boundary conditions
- **Integration boundary checks** — external API failure, timeout, invalid response scenarios
- **SLA & performance mapping** — test cases linked to NFR benchmarks

### 8.2 Estimated Test Case Volume

| Category | Estimated Count | Scope |
|----------|----------------|-------|
| UI Test Cases | ~320–360 | 29 screens + 11 modals, persona-based access, form validation |
| API Test Cases | ~350–400 | 66 APIs — functional, negative, tenant enforcement |
| Integration Cases | ~60–80 | 7 external integrations — fault injection, retry validation |
| Security Cases | ~40–60 | OWASP, JWT, RBAC/ABAC, cross-tenant, CSP |
| Performance Cases | ~25–40 | Load, stress, soak, month-end simulation |
| **Total** | **~800–900** | **Structured test cases** |

Maintained in Jira/Xray (or HighRadius-approved test management tool).

### 8.3 Requirements Traceability Matrix

Each test case maps to:

| Traceability Dimension | Purpose |
|-----------------------|---------|
| Requirement ID | RFP requirement coverage |
| User Story ID | Sprint-level traceability |
| Agent | Agent-level KPI validation |
| API | API-level coverage tracking |
| Persona | Role-based access verification |
| SLA Benchmark | NFR compliance mapping |

Ensures 100% coverage traceability from requirement to test execution.

### 8.4 Test Case Lifecycle

Draft → Review → Approved → Executed → Regressed → Archived

- All P1/P2 defects require regression test update before closure
- Test cases reviewed and approved before sprint execution
- Archived test cases retained for audit and compliance reference

### 8.5 Entry & Exit Criteria

**Entry Criteria:**
- Requirements signed off by HighRadius stakeholders
- Environment stable and accessible
- Build deployed via CI/CD pipeline

**Exit Criteria:**
- All critical scenarios executed
- No open P1 defects; P2 defects resolved or deferred with HighRadius approval
- Regression pass rate >= 95%
- SLA benchmarks met (API < 3s, Grid < 500ms)
- Requirements Traceability Matrix validated — 100% coverage

---

*Prepared By: Metapointer | For: HighRadius Corporation | Date: February 28, 2026*
