Quality Strategy

AP Supplier Portal

Prepared for:  HighRadius Corporation

Prepared by:  Metapointer Labs Pvt. Ltd.

Date:  March 2026

Version:  3.3

Table of Contents

1.  Quality Approach	4

1.1  Governance Alignment	4

1.2  Scope Coverage	4

1.3  QA Tool Stack	4

2.  Test Strategy	6

2.1  Backend Testing	6

2.2  Frontend Testing	6

2.3  End-to-End Critical Journey Automation	6

2.4  Performance & Load Testing	7

2.5  Security & Compliance Testing	7

3.  Automation Approach	9

3.1  Automation Framework Architecture	9

3.2  Test Case Design Model	9

3.3  CI/CD Integration	9

4.  Defect Management	11

4.1  Defect Governance	11

4.2  Weekly Defect Reporting	11

5.  Release Controls	12

6.  Quality Metrics	13

7.  Entry & Exit Criteria	14

7.1  Phase Entry Criteria	14

7.2  Phase Exit Criteria	14

8.  Test Environment Readiness Conditions	16

8.1  Environment Infrastructure	16

8.2  Integration Stubs & Test Data	16

8.3  Tooling Readiness	17

9.  QA Delivery Timeline	18

10.  Test Case Lifecycle	20

11.  Requirements Traceability Matrix	22

12.  QA Effort Estimation	24

12.1  Effort by Test Type	24

12.2  Effort by Phase	24


# 1.  Quality Approach



## 1.1  Governance Alignment


The Quality Strategy for the AP Supplier Portal is designed to provide HighRadius with complete confidence in every delivered feature — from individual API correctness through to system-level performance, security, and tenant isolation. Quality is built into the delivery process, not tested in at the end.

This strategy aligns with:

•  HighRadius engineering and CI/CD standards (RFP Section 5)

•  Contractual SLA commitments (P1–P4 defect model) as defined in the Commercial & Legal document

•  Scope of Work security and compliance obligations (29 screens, 11 modals, 66 APIs, 7 agents)

•  Technical architecture (Spring Boot 3.x backend, React 18.x frontend, multi-tenant schema-per-tenant design)

•  MASC success criteria: (a) UAT delivery, (b) 1 live customer in production, (c) 90%+ KPI achievement per agent


## 1.2  Scope Coverage


This QA strategy governs end-to-end validation of all portal deliverables:


| Scope Item | Count | Validation Approach |
| --- | --- | --- |
| Application Screens | 29 | Functional E2E, persona-based access control, WCAG 2.0 AA accessibility |
| Modal Workflows | 11 | Trigger validation, form logic, parent-screen integration, action confirmation |
| APIs | 66 | Functional, negative, boundary, tenant enforcement, failure injection (58 vendor + 7 integrations + 1 orchestration) |
| Personas | 4 | RBAC/ABAC matrix validation: all roles tested across all applicable screens and actions |
| Intelligent Agents | 7 | Agent-level KPI validation per acceptance criteria (>90% target for all KPIs) |
| External Integrations | 7 | Fault injection: timeout simulation, circuit breaker validation, retry logic, dead-letter queue handling |
| Test Cases (estimated) | ~800–900 | UI: ~350, API: ~380, Integration: ~70, Security: ~50, Performance: ~35 |



## 1.3  QA Tool Stack


Where tools are not mandated by HighRadius, the following stack is proposed. Final tool selection is subject to HighRadius engineering approval:


| Category | Proposed Tool | Version | Notes |
| --- | --- | --- | --- |
| Frontend Unit Testing | Jest | 29.7.0 | Developer responsibility; 80% coverage target (RFP mandate) |
| Backend Unit Testing | JUnit 5 + Mockito | — | Developer responsibility; 80% coverage target (RFP mandate) |
| Backend Integration | Testcontainers + WireMock | Latest | Container-based and mock-based integration testing |
| E2E Automation | Playwright | 1.49.0 | Subject to HighRadius approval; fallback: Cypress/Selenium |
| Performance Testing | Artillery | 2.0.21 | Subject to HighRadius approval; fallback: JMeter/Gatling |
| Defect Tracking | Jira | — | Per HighRadius standard |
| Application Monitoring | Sentry | 10.x | Subject to HighRadius approval; fallback to HR-standard APM |
| Infrastructure Monitor | Prometheus / Grafana | — | Per HighRadius standard |
| Logging | ELK / Fluentd | — | Per HighRadius standard |
| Alerting | PagerDuty / OpsGenie | — | Per HighRadius standard |


Unit Test Ownership
Unit tests (Jest for frontend, JUnit for backend) are developer responsibilities — written alongside feature code and included in FE/BE capacity estimates. QA owns E2E, integration, performance, security, and regression testing. This clean ownership split ensures both developer accountability and independent QA validation.


# 2.  Test Strategy



## 2.1  Backend Testing


Stack: Spring Boot 3.x — Java 17+ | JUnit 5 + Mockito + Testcontainers + WireMock

•  Coverage Requirement: 80% overall code coverage (RFP mandate). Target 100% coverage for financial and invoice logic modules.


| Area | Scope |
| --- | --- |
| API Validation | All 66 APIs — functional, negative, boundary condition testing |
| External Integrations | 7 integration points: screening, bank validation, ERP, Keycloak, Vault, S3, notifications |
| Fault Tolerance | Circuit breaker activation, retry logic, dead-letter queue handling — all failure paths tested |
| Database | Flyway schema migrations, schema-per-tenant isolation, row-level security enforcement |
| Security | JWT tenant validation, Vault integration, cross-tenant prevention at service layer |
| Failure Injection | ERP timeout simulation, screening API failures, bank validation unavailability, external dependency downtime |



## 2.2  Frontend Testing


Stack: React 18.x + G4 DSL | Jest 29.7.0 + Playwright 1.49.0

•  Coverage Requirement: 80% unit test coverage (RFP mandate)


| Area | Scope |
| --- | --- |
| Screens | All 29 screens — functional, responsive, persona-based access control |
| Modals | All 11 modals — trigger logic, form validation, parent screen integration |
| Form Builder | Dynamic form configuration, field validation rules, multi-language label rendering |
| Workflow Config | Approval chain configuration, conditional routing preview, escalation rule builder |
| Dashboards | KPI calculation accuracy, real-time data updates, chart rendering, filter interactions |
| Accessibility | WCAG 2.0 AA compliance: ARIA tags, keyboard navigation, screen reader compatibility, colour contrast |



## 2.3  End-to-End Critical Journey Automation


The following critical user journeys are fully automated in the E2E test suite. All journeys run in CI/CD on every merge to QA:


| Journey | Automated Flow |
| --- | --- |
| Supplier Onboarding | Invitation → Registration → Form Fill → Screening (4 checks) → Bank Validation → Multi-Level Approval → Activation |
| PO Lifecycle | PO Import from ERP → Supplier Acknowledgement in Portal → Status Sync to ERP → PO Flip to Invoice |
| Invoice Lifecycle | Invoice Creation (manual + PO-flip) → Field Validation → Submission → AP Sync → Status Tracking |
| Master Data Change | Change Request Form → Approval Workflow Trigger → Approval Decision → Master Data Update → Notification |
| SLA Escalation | SLA breach detection → Auto-escalation notification → Next approver assignment → Override action |
| Month-End Processing | High-volume invoice/PO processing under peak load — validates SLA compliance under stress |


•  Flaky Test Policy: Tests exceeding 3% flakiness threshold are quarantined and fixed before the next sprint. No flaky tests are allowed into the regression suite.


## 2.4  Performance & Load Testing


Performance testing is mandatory before every production release. Release is blocked if SLA benchmarks are breached:


| Test Type | Scope | Pass Criteria |
| --- | --- | --- |
| Load Testing | 100–500 concurrent users, standard workflows | All APIs < 3s; Grid < 500ms |
| Stress Testing | Beyond expected capacity — find breaking points | Graceful degradation; no data loss; circuit breakers activate |
| Soak Testing | 8-hour sustained load at normal traffic levels | No memory leaks; stable response times; no pod restarts |
| Month-End Simulation | Peak invoice/PO volume; ERP sync throughput peak | SLA maintained under peak load; ERP sync queue stable |



## 2.5  Security & Compliance Testing



| Area | Validation Scope |
| --- | --- |
| OWASP Top 10 | SAST + DAST scanning of all vendor-built endpoints; zero critical/high findings required |
| CSP & Headers | Content Security Policy verification; security header validation on all responses |
| Injection Testing | XSS, SQL injection, command injection across all input surfaces and API parameters |
| JWT Security | Token tampering, expiry handling, invalid signature rejection, tenant_id claim manipulation |
| Cross-Tenant Access | Tenant isolation verification at API layer and database layer; privilege escalation attempts |
| Virus Scanning | Document upload validation via S3-compatible storage; malicious file quarantine validation |
| Vault Integration | HashiCorp Vault credential retrieval, rotation, and access control validation |
| RBAC/ABAC Matrix | 4 personas × 29 screens + 11 modals — all role permission combinations validated |



# 3.  Automation Approach



## 3.1  Automation Framework Architecture


The automation framework is designed to be maintainable, scalable, and CI/CD-native. Playwright is the primary E2E and functional test automation tool, directly fulfilling RFP Section 5 (E9) requirement to author functional test cases for automated QA. All test suites are version-controlled alongside the application code:

•  Page Object Model (POM) pattern for all E2E tests — separates test logic from UI selectors for maintainability

•  API test library using Playwright's API testing capabilities + Testcontainers for backend integration

•  Test data management via dedicated test data factory — no shared mutable state between test runs

•  Parallel test execution across 4 workers for fast CI/CD feedback (E2E suite target: < 15 minutes)

•  Screenshot and video capture on test failure — stored as CI artifacts for debugging

•  Test result reporting in JUnit XML format — compatible with Jira/Xray for traceability


## 3.2  Test Case Design Model


All test cases are designed using the following principles:

•  Requirement-based testing — every test case maps to an RFP requirement or user story in Jira

•  Risk-based prioritisation — financial workflows (invoice, approval, bank validation), compliance (screening, audit), and tenant isolation are highest priority

•  Persona validation — all 4 personas tested across every applicable screen and action

•  Positive and negative flows — happy path plus all error handling, boundary conditions, and invalid input scenarios

•  Integration boundary checks — external API failure, timeout, invalid response, and partial failure scenarios

•  SLA and performance mapping — test cases directly linked to NFR benchmarks (< 3s API, < 500ms grid)


## 3.3  CI/CD Integration



| CI Stage | Tests Executed | Blocking |
| --- | --- | --- |
| On every commit | Unit tests (Jest + JUnit); SAST scan | Yes — merge blocked on failure or critical SAST finding |
| On merge to QA | Unit tests + API integration tests + smoke E2E | Yes — deploy blocked on failure |
| Nightly (QA) | Full E2E regression suite + performance smoke tests | Alerts on failure; addressed next business day |
| Pre-UAT promotion | Full E2E + performance validation + security scan + tenant isolation tests | Yes — UAT promotion blocked on failure |
| Pre-production | Full regression + month-end simulation + infosec review | Yes — go-live blocked on any P1/P2 issue or benchmark breach |



# 4.  Defect Management


All defects are tracked in Jira per HighRadius standard. The following SLAs apply during the 20-week development phase with full team available. Post-go-live hypercare SLAs are defined in the Commercial & Legal document (Document 6):


| Severity | Description | Response SLA | Resolution SLA | Examples |
| --- | --- | --- | --- | --- |
| P1 — Critical | System down or data loss | < 2 hours | < 8 hours | Portal inaccessible; data corruption; cross-tenant data leak |
| P2 — High | Major feature impaired; no workaround | < 4 hours | < 24 hours | Approval workflow broken; screening fails silently; PO sync error |
| P3 — Medium | Feature impaired; workaround available | < 8 hours | < 3 business days | Dashboard metrics incorrect; filter not working; UI alignment |
| P4 — Low | Cosmetic issue or minor enhancement | Next business day | Next sprint | Tooltip missing; colour mismatch; minor label typo |



## 4.1  Defect Governance


•  All P1 defects require Root Cause Analysis (RCA) and regression test update before closure

•  All P1 and P2 defects require regression test added to the suite before closure — no defect resolved without preventing recurrence

•  MTTD (Mean Time to Detect) and MTTR (Mean Time to Resolve) tracked and reported per sprint

•  Defect injection rate tracked — spike indicates process or quality issue requiring team review

•  No open P1 or P2 defects allowed at UAT or production go-live gates


## 4.2  Weekly Defect Reporting


Defect metrics reported to HighRadius stakeholders on every weekly status update:

•  Open defect count by severity (P1–P4)

•  Defect aging — days open per severity

•  Defect injection rate per sprint — new defects found vs stories completed

•  Defect leakage rate — defects found in UAT that should have been caught in QA

•  MTTD and MTTR by severity


# 5.  Release Controls


Production release requires all of the following gates to be passed. No exceptions are permitted without explicit written approval from HighRadius Engineering and HighRadius Infosec:


| Release Gate | Criteria | Validated By |
| --- | --- | --- |
| Code Coverage | >= 80% — backend (JUnit) and frontend (Jest) | CI/CD coverage report |
| API Validation | All 66 APIs validated — functional + negative + tenant isolation | QA API test suite |
| Agent KPI Validation | All 7 agents validated against acceptance criteria (>90% targets) | QA E2E test suite + UAT |
| Tenant Isolation | Schema-per-tenant + RLS verified; cross-tenant access prevention confirmed | Automated isolation tests |
| API Performance | All APIs < 3s response time (P95) | Artillery load test report |
| Grid Performance | Grid rendering < 500ms for 1,000+ rows | Virtual scrolling stress test |
| OWASP Compliance | SAST + DAST complete — zero critical/high findings | Security scan report |
| Accessibility | WCAG 2.0 AA validated across all 29 screens | Accessibility audit report |
| Defect Status | No open P1/P2 defects; P3/P4 documented and accepted by HighRadius | Jira defect dashboard |
| Infosec Clearance | HighRadius cybersecurity team sign-off obtained | HR Infosec certificate |
| Month-End Simulation | Peak-volume scenario validated and passed | Artillery soak test report |
| Rollback Validation | Rollback procedure tested and documented for this release | Pre-deployment checklist |


Release Blocked by Performance
If any performance benchmark is breached (API > 3s or Grid > 500ms), the release is automatically blocked regardless of all other gates. Performance is a non-negotiable quality gate, not a best-effort target.


# 6.  Quality Metrics


The following metrics are tracked, measured, and reported to HighRadius on every sprint cycle. All metrics are visible in the weekly PVA (Product Velocity Analysis) report:


| Metric | Target | Reporting Frequency |
| --- | --- | --- |
| Code Coverage % | >= 80% backend and frontend | Per sprint — CI/CD dashboard |
| Flaky Test % | < 3% of total test suite | Per sprint — test execution report |
| API SLA Compliance | 100% of APIs < 3s (P95) | Per sprint — performance test report |
| Grid SLA Compliance | < 500ms grid rendering | Per sprint — performance test report |
| MTTD (Mean Time to Detect) | Tracked — downward trend | Per sprint — defect report |
| MTTR (Mean Time to Resolve) | P1 < 8h; P2 < 24h | Per sprint — defect report |
| Defect Escape Rate | Tracked — < 5% to UAT | Per sprint — defect leakage report |
| Release Stability | Zero P1/P2 at go-live | Per release — go-live report |
| OWASP Findings | Zero critical/high | Per security scan — monthly minimum |
| Tenant Validation Results | 100% isolation confirmed | Per sprint — isolation test report |
| E2E Pass Rate | >= 95% regression pass rate | Per sprint — regression report |


All metrics are maintained in Jira/Xray (or HighRadius-approved test management tool) with full traceability from requirement to test execution to result.


# 7.  Entry & Exit Criteria


Each QA phase is gated by documented entry and exit criteria. QA sign-off is mandatory before any environment promotion. No gate may be waived without written approval from both HighRadius Product Management and HighRadius Engineering:


## 7.1  Phase Entry Criteria



| Phase | Entry Criteria (All Must Be Met) |
| --- | --- |
| Sprint 0 QA Setup | Signed SOW received; Jira project created; test tool stack approved by HighRadius; QA environment provisioned; Validation Error State Library drafted; CI/CD pipeline operational with automated unit test execution |
| Phase 1 (MVP) QA (Sprints 1–5) | Sprint 0 exit criteria met; all Phase 1 (MVP) features code-complete and merged to QA branch; unit test coverage ≥ 80% confirmed by CI/CD; design specs approved for all 17 screens; test data provided by HighRadius; Keycloak integration environment accessible; screening and bank validation API stubs operational |
| Phase 1 (MVP) UAT | All Phase 1 (MVP) E2E tests passing (≥ 95% pass rate); all API < 3s validated; Grid < 500ms validated; WCAG 2.0 AA audit passed; zero open P1/P2 defects; OWASP SAST scan complete with no critical/high findings; test environment stable for ≥ 72 hours without restart |
| Phase 2 QA (Sprints 6–9) | Phase 1 in production with 1 live customer; Phase 2 features code-complete and merged; unit test coverage ≥ 80% confirmed; ERP sample data (SAP/Oracle/NetSuite) available; Phase 2 E2E test cases reviewed and approved |
| Phase 2 UAT | Full regression suite passing; virtual scrolling stress test passed; penetration test complete; month-end simulation passed; zero open P1/P2 defects; UAT environment stable for ≥ 72 hours |
| Production Go-Live | All 12 release gates cleared (ref. Section 5); infosec clearance obtained; rollback procedure tested and documented; HighRadius Infosec certificate received; MASC criteria (a) UAT delivered, (b) 1 live customer confirmed, (c) all agent KPIs ≥ 90% |



## 7.2  Phase Exit Criteria



| Phase | Exit Criteria (All Must Be Met Before Promotion) |
| --- | --- |
| Sprint 0 | Architecture documentation signed off; CI/CD pipeline operational; G4 OOB evaluation complete; Validation Error State Library finalised; DB schema v1 approved; all 16 undesigned screen UX mockups approved |
| Phase 1 (MVP) QA | All 17 screens and ~40 APIs validated (functional + negative + boundary); RBAC/ABAC matrix confirmed across all 4 personas; 4 E2E critical journeys automated and passing; performance SLAs validated; WCAG 2.0 AA audit complete; zero P1/P2 defects open; QA sign-off document issued |
| Phase 1 (MVP) UAT | HighRadius Product Management sign-off received; 1 live customer in production; all agent KPIs ≥ 90% confirmed; hypercare monitoring started |
| Phase 2 QA | All 12 screens and ~27 APIs validated; full regression suite passing; virtual scrolling stress test (1,000+ rows) passed; penetration test passed; month-end simulation passed; zero P1/P2 open; QA sign-off document issued |
| Phase 2 UAT | HighRadius Engineering sign-off received; GIT handover accepted; KT sessions delivered; all MASC success criteria (a)(b)(c) confirmed; infosec clearance certificate issued |



# 8.  Test Environment Readiness Conditions


QA activities cannot proceed until all environment readiness conditions below are confirmed. The QA Engineer validates readiness at the start of every sprint and escalates any unresolved blocker to the Project Manager within 24 hours:


## 8.1  Environment Infrastructure



| Condition | Owner | Required By | Validation Check |
| --- | --- | --- | --- |
| QA environment provisioned and stable | HighRadius | Sprint 0 end | HTTP 200 on health endpoint; no pod restarts in 24 hours |
| UAT environment provisioned and isolated from QA | HighRadius | Sprint 5 start | Separate namespace confirmed; data isolation verified |
| CI/CD pipeline deploys to QA on merge (auto) | Metapointer | Sprint 0 end | Smoke test passes post-auto-deploy |
| Keycloak IAM accessible with test tenant configured | HighRadius | Sprint 1 start | Login flow works for all 4 persona roles |
| HashiCorp Vault accessible or env-var fallback in place | HighRadius | Sprint 1 start | Secrets resolved without hardcoded values |
| PostgreSQL QA database provisioned with schema migrations | Metapointer | Sprint 1 start | All Flyway migrations applied; schema matches v1 design |
| Redis cache operational for session and template storage | Metapointer | Sprint 1 start | Cache hit/miss metrics visible in observability |
| S3-compatible document storage accessible | HighRadius | Sprint 2 start | Upload and download functional; virus scan mock active |



## 8.2  Integration Stubs & Test Data



| Integration | Dev/QA Mode | Switch to Real | Data Requirement |
| --- | --- | --- | --- |
| Screening APIs (address, TIN, OFAC) | WireMock stub — returns configurable pass/fail responses | UAT | Test suppliers with known pass/fail outcomes for all 4 check types |
| Bank Validation API | WireMock stub — returns valid/invalid/BEC-risk responses | UAT | Test bank accounts including BEC-risk and invalid routing numbers |
| ERP Systems (SAP/Oracle/NetSuite) | Synthetic PO and invoice dataset (Metapointer-generated) | Phase 2 UAT | 10 suppliers, 50+ POs, 100+ invoice records across 3 ERP types |
| Keycloak | Test Keycloak instance (HighRadius-provisioned) | Production | 4 test users (1 per persona) per tenant; MFA disabled for test |
| Notification Service (Email/WebSocket) | SMTP test server (Mailpit); WebSocket local mock | UAT | Email capture confirmed; WebSocket real-time event verified |
| HashiCorp Vault | Environment variables (dev); real Vault pre-UAT | Pre-UAT | All secrets retrievable; rotation tested; no hardcoded creds |



## 8.3  Tooling Readiness


•  Jira project configured with QA board, defect workflow (Open → In Progress → Resolved → Closed), and P1–P4 severity labels

•  Playwright (or HighRadius-approved E2E tool) installed, configured, and connected to CI/CD pipeline

•  Artillery (or approved performance tool) configured with QA environment endpoints and baseline load profiles

•  Code coverage reporting integrated with CI/CD — coverage ≥ 80% blocks merge

•  SAST tool configured — critical/high findings block merge to QA branch

•  Observability dashboard accessible: API response times, error rates, pod health, memory/CPU

•  Test result reporting connected to Jira/Xray (or approved test management tool) for traceability


# 9.  QA Delivery Timeline


QA activities run in parallel with development throughout the 20-week programme. The QA engineer is engaged from Sprint 0 and maintains a test-development lag of no more than 1 sprint behind feature delivery:


| Sprint / Phase | Calendar Window | QA Activities | QA Deliverables |
| --- | --- | --- | --- |
| Sprint 0 | Weeks 1–2 | Environment readiness validation; test plan creation; E2E framework setup; Validation Error State Library review; test data design | QA Test Plan (this document); E2E framework skeleton; test data design doc; environment readiness sign-off |
| Sprint 1 | Weeks 3–4 | Supplier Onboarding backend API testing (12 APIs); registration form functional testing; RBAC matrix validation for Supplier and Manager personas | Sprint 1 API test report; defect log; RBAC validation evidence |
| Sprint 2 | Weeks 5–6 | Supplier Screening Agent testing (7 APIs + 3 screens); parallel check validation (address, TIN, OFAC, bank pre-validation); WireMock stub validation for all failure scenarios | Sprint 2 test report; screening failure scenario coverage confirmation |
| Sprint 3 | Weeks 7–8 | Bank Account Validation testing (3 APIs + 2 screens); Supplier Approval workflow testing (8 APIs + 4 screens); SLA escalation path validation; delegation flow testing | Sprint 3 test report; approval workflow test evidence |
| Sprint 4 | Weeks 9–10 | Dashboard testing (Supplier + Manager, 9 APIs + 2 screens); KPI calculation accuracy validation; real-time WebSocket event testing; Admin config screens testing; E2E journey 1 (Onboarding) automation | Sprint 4 test report; E2E Journey 1 automated and passing |
| Sprint 5 | Weeks 11–12 | Phase 1 full regression (17 screens, ~40 APIs); performance validation (Artillery load test); WCAG 2.0 AA audit; OWASP SAST + DAST; tenant isolation automated tests; UAT preparation | Phase 1 QA sign-off; performance report; WCAG audit report; SAST report; UAT test pack |
| Phase 1 (MVP) Go-Live | ~Week 12 from Kickoff | Production smoke test; 1 live customer monitoring; hypercare SLA monitoring activation | Go-live smoke test pass; hypercare monitoring live |
| Sprint 6–7 | Weeks 13–16 | PO Agent testing (10 APIs + 5 screens); ERP adapter validation (SAP/Oracle/NetSuite); Invoice Creation Agent testing (11 APIs + 5 screens); PO-flip automation testing; E2E journeys 2–3 (PO Lifecycle, Invoice Lifecycle) automation | Sprint 6–7 test reports; PO/Invoice E2E journeys automated |
| Sprint 8–9 | Weeks 17–20 | Master Data Change Approval testing (6 APIs + 2 screens); full regression suite run (Phase 1 + Phase 2); virtual scrolling stress test (1,000+ rows); penetration test; month-end simulation (peak volume); E2E journeys 4–6 automation; handover prep | Phase 2 QA sign-off; pen test report; month-end simulation report; full test suite handed over |
| Full Go-Live | ~Week 20 from Kickoff | Production smoke test (all 7 agents); handover validation; MASC criteria (a)(b)(c) evidence assembly | Go-live sign-off; MASC evidence pack; GIT handover with full test suite |
| Hypercare | Months 5–11 from Kickoff (6-month Hypercare) | Production monitoring; P1/P2 incident response; regression test maintenance; KPI tracking | Monthly QA health reports; incident RCA documents; final hypercare closure report |


QA — Development Lag Policy
The QA engineer tests the sprint immediately prior to the current development sprint. UX is 1 sprint ahead of development; QA is ≤ 1 sprint behind development. This cadence ensures no features accumulate untested and provides timely defect feedback to developers while the code context is still fresh.


# 10.  Test Case Lifecycle


Every test case follows a defined lifecycle from creation through to closure. No test case is executed without a linked requirement, and no test cycle is closed with unresolved P1/P2 failures:


| Stage | Activity | Owner | Input | Output |
| --- | --- | --- | --- | --- |
| 1. Requirement Analysis | Review user story, acceptance criteria, and RFP requirement. Identify test conditions and risk areas. | QA Engineer | User story in Jira; RFP section; UX design spec | Test conditions list; risk rating; traceability link to requirement |
| 2. Test Case Design | Write positive, negative, boundary, and edge-case test cases. Design test data. Apply risk-based prioritisation. | QA Engineer | Test conditions; Validation Error State Library; API contract | Test cases in Jira/Xray; test data specification; priority assigned |
| 3. Test Case Review | Peer review of test cases by second QA or developer. Review for coverage gaps, duplicate tests, and data correctness. | QA Engineer + Developer | Draft test cases | Reviewed and approved test cases; coverage gaps documented and resolved |
| 4. Test Environment Readiness | Confirm all environment readiness conditions are met (ref. Section 8). Validate stubs/mocks. Confirm test data loaded. | QA Engineer | Environment readiness checklist | Environment sign-off; test data confirmed; integration stubs validated |
| 5. Test Execution | Execute test cases (manual + automated). Log results in Jira/Xray. Raise defects immediately on failure. | QA Engineer | Approved test cases; stable build in QA environment | Test execution report; pass/fail results; defects raised in Jira with steps to reproduce |
| 6. Defect Management | Developer investigates and resolves defect. QA verifies fix. Regression test for affected area. RCA for P1 defects. | Developer + QA | Jira defect with reproduction steps | Resolved defect; regression test updated; RCA document (P1 only) |
| 7. Regression Validation | Re-run affected test suite after fix. Confirm no new failures introduced. Update automation suite if manual test now automatable. | QA Engineer | Resolved defect; test suite | Regression pass confirmation; automation coverage updated |
| 8. Test Cycle Closure | Confirm all test cases executed. No open P1/P2 defects. Document P3/P4 exceptions accepted by HighRadius. Issue sign-off. | QA Engineer + HighRadius | Completed test execution; defect dashboard | Test cycle closure report; QA sign-off document; metrics captured for weekly report |


Automation-First Policy
Any test case executed manually more than once is a candidate for automation. The QA engineer maintains an automation backlog in Jira. Regression suite coverage grows each sprint — targeting ≥ 95% regression automation by Phase 2 go-live. No manual-only regression runs at production go-live.


# 11.  Requirements Traceability Matrix


Every RFP requirement, user story, and non-functional requirement is mapped to at least one test case. The matrix below confirms 100% requirement coverage across all 7 agents, 29 screens, 66 APIs, and NFRs:


| Requirement Area | RFP Ref | Test Cases | Test Type | Phase | Coverage |
| --- | --- | --- | --- | --- | --- |
| Supplier Onboarding — Individual & bulk invitation | RFP S2 | ~45 | Functional, E2E, RBAC | Phase 1 (MVP) | 100% |
| Supplier Registration — Dynamic multi-language form | RFP S2 | ~38 | Functional, boundary, i18n | Phase 1 (MVP) | 100% |
| Document Upload & Validation | RFP S2 | ~22 | Functional, virus scan, negative | Phase 1 (MVP) | 100% |
| Draft Save & Resume | RFP S2 | ~12 | Functional, state persistence | Phase 1 (MVP) | 100% |
| Duplicate Supplier Detection | RFP S2 | ~8 | Functional, edge case | Phase 1 (MVP) | 100% |
| Supplier Screening — 4 parallel checks | RFP S3 | ~40 | Functional, fault injection, E2E | Phase 1 (MVP) | 100% |
| Screening — Retry & actionable error feedback | RFP S3 | ~15 | Functional, negative | Phase 1 (MVP) | 100% |
| Bank Account Validation — BEC prevention | RFP S4 | ~20 | Functional, security, E2E | Phase 1 (MVP) | 100% |
| Supplier Approval — Multi-level configurable workflow | RFP S5 | ~42 | Functional, E2E, SLA | Phase 1 (MVP) | 100% |
| SLA-Based Auto-Escalation | RFP S5 | ~18 | Functional, timing, RBAC | Phase 1 (MVP) | 100% |
| Master Data Change Approval | RFP S6 | ~25 | Functional, workflow, RBAC | Phase 2 | 100% |
| Purchase Order — Multi-ERP import & sync | RFP S7 | ~38 | Integration, functional, E2E | Phase 2 | 100% |
| PO Acknowledgement & ERP sync-back | RFP S7 | ~20 | Integration, fault tolerance | Phase 2 | 100% |
| Invoice Creation — Manual & PO-flip | RFP S8 | ~45 | Functional, E2E, boundary | Phase 2 | 100% |
| Invoice — Partial invoicing, tax, attachments | RFP S8 | ~28 | Functional, validation | Phase 2 | 100% |
| Supplier & Manager Dashboards | RFP S9 | ~30 | Functional, real-time, RBAC | Phase 1 (MVP) | 100% |
| Admin Config — Form builder, workflow config | RFP S10 | ~35 | Functional, configuration | Phase 1 (MVP) | 100% |
| Multi-Tenancy — Schema-per-tenant isolation | NFR | ~30 | Security, isolation, automation | Both | 100% |
| RBAC / ABAC — 4 personas × 29 screens | NFR | ~40 | Security, permission matrix | Both | 100% |
| WCAG 2.0 AA Accessibility | NFR | ~29 | Accessibility audit (per screen) | Both | 100% |
| API Performance < 3s (P95) | NFR | ~10 | Load test (Artillery) | Both | 100% |
| Grid Performance < 500ms (1,000+ rows) | NFR | ~5 | Stress test (virtual scroll) | Both | 100% |
| OWASP Top 10 Compliance | NFR | ~50 | SAST + DAST + manual pen test | Both | 100% |
| CI/CD — HighRadius engineering practices | RFP S5 | ~8 | Pipeline validation | Both | 100% |
| Audit Trail — Immutable, 2-year retention | NFR | ~12 | Functional, data integrity | Both | 100% |


Traceability Tool
Full bidirectional traceability is maintained in Jira/Xray (or HighRadius-approved test management tool). Every test case links to a Jira story; every story links to an RFP requirement. Coverage gaps are reported weekly and resolved within the sprint. The complete RTM is available on request.


# 12.  QA Effort Estimation


QA effort is estimated at 1 dedicated QA Engineer (6 FTE-months) for the 20-week core delivery programme, plus 0.5 FTE contribution during 6-month hypercare. All estimates include a 1.40x AI productivity multiplier (Claude Opus AI) on test script authoring, API test generation, and defect documentation:


## 12.1  Effort by Test Type



| Test Category | Estimated Test Cases | Effort (Days) | AI Multiplier | Adjusted Days |
| --- | --- | --- | --- | --- |
| Backend API Testing (66 APIs) | ~380 | 28 | 1.40x | 20 |
| Frontend Functional Testing (29 screens) | ~350 | 26 | 1.30x | 20 |
| E2E Critical Journey Automation (6) | ~60 | 18 | 1.40x | 13 |
| Performance & Load Testing | ~35 | 8 | 1.20x | 7 |
| Security & Penetration Testing | ~50 | 10 | 1.10x | 9 |
| Regression Testing (Phase 1 (MVP) + Phase 2) | ~870 | 22 | 1.40x | 16 |
| Tenant Isolation Testing | ~30 | 6 | 1.30x | 5 |
| Accessibility (WCAG 2.0 AA) | ~29 | 5 | 1.10x | 5 |
| UAT Support & Sign-off Preparation | — | 10 | 1.10x | 9 |
| Test Plan, Reporting & Admin | — | 15 | 1.30x | 12 |
| Total (20-week programme) | ~800–900 | 148 | — | 116 |



## 12.2  Effort by Phase



| Phase | Duration | QA Activities | QA Days (Adjusted) |
| --- | --- | --- | --- |
| Sprint 0 | 2 weeks | Framework setup, test plan, environment validation, test data design | 8 |
| Phase 1 (MVP) Dev QA | 10 weeks | Sprint-by-sprint API + UI + E2E testing; defect management; RBAC matrix | 52 |
| Phase 1 (MVP) UAT | 2 weeks | Full regression, performance validation, WCAG audit, SAST, UAT support | 14 |
| Phase 2 Dev QA | 8 weeks | PO/Invoice/MDC testing; ERP adapter validation; E2E journeys 4–6 | 30 |
| Phase 2 UAT | 2 weeks | Full regression, stress test, pen test, month-end simulation, UAT support | 12 |
| Hypercare | 6 months | P1/P2 incident response, monitoring, regression maintenance (0.5 FTE) | 0.5 FTE rotating |


Developer Unit Test Ownership
Unit tests (Jest for frontend, JUnit for backend) are NOT included in QA effort above. Unit tests are developer responsibilities — estimated separately in FE/BE capacity. The 80% coverage mandate is enforced by CI/CD and is a developer delivery criterion, not a QA deliverable. QA validates coverage reports but does not write unit tests.