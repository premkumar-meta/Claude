Delivery Plan

AP Supplier Portal

Prepared for:  HighRadius Corporation

Prepared by:  Metapointer Labs Pvt. Ltd.

Date:  March 2026

Version:  3.3

Table of Contents

1.  Delivery Approach	3

1.1  Engagement Model	3

1.2  Agile Sprint Cadence	3

1.3  Vendor Commitments (RFP Section 5)	3

2.  Project Phases	5

2.1  Sprint 0 — Foundation (Weeks 1–2)	5

2.2  Phase 1 (MVP): Core Onboarding & Compliance (Sprints 1–5, Weeks 3–12)	5

2.3  Phase 2 — Transactional Enablement (Sprints 6–9, Weeks 13–20)	6

2.4  Hypercare & Stabilisation (Months 5–11 from Kickoff — 6-Month Hypercare)	6

3.  Milestones & Timeline	7

3.1  Programme Timeline	7

3.2  Calendar Estimates by Discipline	7

3.3  Key Deliverables by Phase	8

3.4  Payment Milestone Schedule	8

4.  Governance & Reporting	10

4.1  Phase Entry & Exit Criteria	10

4.2  Weekly Reporting	10

4.3  Sign-Off Gates	10

5.  Risk & Issue Management	12

5.1  Risk Register	12

5.2  Issue Escalation Path	12

6.  Change Management	13

6.1  Change Request Process	13

6.2  Scope Variance Policy	13

7.  Communication Plan	14

7.1  Communication Cadence	14

7.2  RACI Summary	14


# 1.  Delivery Approach



## 1.1  Engagement Model


The AP Supplier Portal is delivered under a Fixed-Price engagement model with milestone-based payments. This model provides HighRadius with full cost certainty while maintaining delivery discipline and accountability at every phase:

•  Fixed-Price: Total cost agreed upfront based on defined scope. No cost overrun risk for HighRadius within the agreed deliverables.

•  Milestone-Based Payments: 6 milestones tied to verified delivery gates (30%–20%–15%–20%–10%–5%, cumulative 30%–50%–65%–85%–95%–100%). 30% advance on contract signing; final 5% on Hypercare completion. No payment without delivery acceptance.

•  Scope Variance Allowance: Up to 10–15% variance in defined deliverables is accommodated without additional cost. Variance beyond this threshold triggers a formal Change Request with cost/timeline impact assessment.

•  MASC Success Criteria: (a) UAT delivery, (b) 1 live customer in production, (c) 90%+ KPI achievement per agent — all required for final payment milestone.


## 1.2  Agile Sprint Cadence


The programme runs on 2-week sprints (10 sprints total: Sprint 0 + Sprints 1–9) with a structured cadence that maintains momentum and enables early risk identification:

•  Sprint 0 (2 weeks): Foundation sprint — architecture, DevOps, design sprint, G4 evaluation. No feature development begins until Sprint 0 is complete and signed off.

•  Sprints 1–5 (10 weeks): Phase 1 (MVP) — 4 agents. UX runs 1 sprint ahead of development throughout.

•  Sprints 6–9 (8 weeks): Phase 2 — 3 transactional agents. Frontend and backend streams run in parallel.

•  Hypercare (6 months): 0.5 FTE dedicated support post go-live.

•  Total Programme Duration: 20 calendar weeks from kickoff to full handover.


## 1.3  Vendor Commitments (RFP Section 5)


Metapointer commits to the following vendor obligations per RFP Section 5:

•  Design collaboration with HighRadius engineering team with written sign-offs

•  Feature-level technical design documentation for every delivered agent

•  Functional and regression test cases (JUnit + Playwright E2E)

•  QA completed and all P1/P2 defects resolved before delivery to HighRadius

•  Handover repository: GIT source code, design docs, KT sessions, API documentation, runbooks

•  Adherence to HighRadius cybersecurity policies during all development activities

•  CI/CD pipeline following HighRadius engineering practices

AI-Powered Delivery
All 6 engineers are equipped with Claude Opus AI subscriptions, delivering 1.10x–1.50x productivity multipliers across code generation (1.30–1.40x), unit test writing (1.40x), API documentation (1.50x), integration code (1.15x), and DevOps configuration (1.10x). These are conservative multipliers applied to experienced developers — resulting in faster delivery within the fixed price.


# 2.  Project Phases



## 2.1  Sprint 0 — Foundation (Weeks 1–2)


Sprint 0 is a non-negotiable foundation sprint. Development does not begin until all Sprint 0 deliverables are complete and signed off:

•  Architecture finalisation and documentation (system design, data model, integration architecture)

•  Design sprint for all 16 undesigned screens — UX delivered before Sprint 1 begins

•  DevOps/CI-CD pipeline setup following HighRadius engineering practices

•  G4 OOB component evaluation — identify reusable components vs. custom builds

•  Validation Error State Library creation — all error messages, toast notifications, inline states documented

•  Integration environment setup: Keycloak mock, screening API stubs, bank validation stubs

•  Database schema v1 design and Flyway migration framework setup

•  HashiCorp Vault access provisioned and integrated (or environment variables configured as fallback)


## 2.2  Phase 1 (MVP): Core Onboarding & Compliance (Sprints 1–5, Weeks 3–12)


Phase 1 delivers the 4 highest-value agents targeting production at ~Week 12 from Kickoff:


| Agent | Screens | APIs | Key Deliverables |
| --- | --- | --- | --- |
| Supplier Onboarding | 6 | 12 | Individual/bulk invitations, dynamic multi-language forms, document upload, draft/resume, duplicate detection |
| Supplier Screening | 3 | 7 | Parallel real-time checks (address, TIN, OFAC, bank pre-validation); progress indicators; retry capability |
| Bank Account Validation | 2 | 3 | Real-time bank detail verification; ownership validation; fraud prevention |
| Supplier Approval | 4 | 8 | Multi-level configurable workflows; SLA auto-escalation; approve/reject/reassign; delegation |
| Core Dashboards | 2 | 9 | Supplier Dashboard (invoice pipeline, payments) + Manager Dashboard (funnel metrics, SLA compliance) |
| Phase 1 (MVP) Total | 17 | 39 | 1 live customer in production by ~Week 12 from Kickoff |



## 2.3  Phase 2 — Transactional Enablement (Sprints 6–9, Weeks 13–20)


Phase 2 delivers the 3 transactional agents, completing the full portal:


| Agent | Screens | APIs | Key Deliverables |
| --- | --- | --- | --- |
| Purchase Order | 5 | 10 | Multi-ERP PO import/sync (SAP/Oracle/NetSuite); supplier acknowledge/reject; real-time status; ERP sync |
| Portal Invoice Creation | 5 | 11 | Manual invoice entry + one-click PO-flip; partial invoicing; tax/discount lines; attachments; AP sync |
| Master Data Change Approval | 2 | 6 | Structured change request form; configurable approval workflow; re-screening triggers; version tracking |
| Phase 2 Total | 12 | 27 | Full portal in production by ~Week 20 from Kickoff |



## 2.4  Hypercare & Stabilisation (Months 5–11 from Kickoff — 6-Month Hypercare)


6-month post-go-live hypercare at 0.5 FTE, rotating across team members:

•  Production monitoring and issue resolution per contractual SLA commitments (P1–P4)

•  Performance tuning and optimisation based on real production load patterns

•  Weekly status updates via email/call and PVA (Product Velocity Analysis)

•  Root cause analysis for all P1 production incidents

•  Knowledge transfer to HighRadius operations team — structured sessions covering architecture, deployment, and operations

•  Formal hypercare closure with HighRadius sign-off at 6 months


# 3.  Milestones & Timeline



## 3.1  Programme Timeline



| Sprint / Phase | Calendar Window | Focus Area | Milestone / Gate |
| --- | --- | --- | --- |
| Sprint 0 | Weeks 1–2 | Architecture, DevOps, design sprint (16 screens), G4 evaluation, Error State Library, Keycloak/Vault setup | Design Sign-off — Sprint 0 exit gate |
| Sprint 1–2 | Weeks 3–6 | Supplier Onboarding Agent + Supplier Screening Agent — backend + frontend parallel | — |
| Sprint 3–4 | Weeks 7–10 | Bank Account Validation + Supplier Approval + Manager/Supplier Dashboards | — |
| Sprint 5 | Weeks 11–12 | Integration testing, E2E test suite, performance validation (API < 3s, Grid < 500ms), UAT prep | Phase 1 (MVP) UAT Complete |
| Phase 1 (MVP) Go-Live | ~Week 12 from Kickoff | 4 agents + dashboards deployed to production; infosec clearance obtained | 1 Live Customer in Production |
| Sprint 6–7 | Weeks 13–16 | Purchase Order Agent + Portal Invoice Creation Agent — multi-ERP adapters | — |
| Sprint 8–9 | Weeks 17–20 | Master Data Change Approval Agent + full integration hardening + regression + pen test | Phase 2 UAT Complete |
| Full Go-Live | ~Week 20 from Kickoff | All 7 agents in production; GIT handover; KT sessions delivered; MASC criteria achieved | Full Delivery & Handover |
| Hypercare | Months 5–11 from Kickoff (6-month Hypercare) | 6-month production support at 0.5 FTE; SLA monitoring; performance tuning; knowledge transfer | Hypercare Closure |



## 3.2  Calendar Estimates by Discipline


Based on actual team composition (3 FE + 2 BE + 1 QA, all with Claude Opus AI). All estimates are AI-adjusted:


| Discipline | Team | Working Days | Calendar Weeks | Notes |
| --- | --- | --- | --- | --- |
| Frontend Development | 3 FE devs | 72 days | ~15 weeks | Parallel across 3 devs; AI multiplier (1.40x) on code and unit tests |
| Backend Development | 2 BE devs + Architect (40%) | 77 days | ~16 weeks | Includes DevOps, observability; AI multiplier (1.30x) on services and APIs |
| QA Engineering | 1 QA + automation | 28 p-weeks | ~17 weeks | Parallel test streams (BE+FE overlap Weeks 6–11); completes Week 17 |
| Sprint 0 (Foundation) | Full team — 7 engineers | 10 days | 2 weeks | Architecture, design sprint, CI/CD setup, G4 evaluation |



## 3.3  Key Deliverables by Phase



| Phase | Deliverables |
| --- | --- |
| Sprint 0 | CI/CD pipeline (HR practices), G4 OOB evaluation, Keycloak + Vault setup, design system tokens, DB schema v1, Validation Error State Library, all 16 undesigned screen designs |
| Phase 1 Dev | 4 agents feature-complete (17 screens, ~40 APIs), 80% unit test coverage, RBAC matrix validated, dashboards live |
| Phase 1 QA | E2E test suite passing, API < 3s validated, Grid < 500ms validated, WCAG 2.0 AA audit passed, UAT sign-off, 1st live customer |
| Phase 2 Dev | 3 agents feature-complete (12 screens, ~27 APIs), full ERP adapters, 80% unit test coverage |
| Phase 2 QA | Full regression, virtual scrolling stress test, penetration test, month-end simulation, UAT feedback addressed |
| Handover | Production deployment, GIT handover accepted, KT sessions delivered, OpenAPI/Swagger docs, runbooks, MASC criteria (a)(b)(c) achieved, infosec clearance |



## 3.4  Payment Milestone Schedule


Each payment is released only upon verified acceptance of the corresponding delivery gate:


| M# | Milestone | Trigger | % | Cumulative |
| --- | --- | --- | --- | --- |
| M1 | Advance — Contract Signing | Contract executed; mobilisation begins | 30% | 30% |
| M2 | Phase 1 UAT Complete | 4 agents passing UAT; PM sign-off; 80%+ coverage — MASC (a) | 20% | 50% |
| M3 | Phase 1 Go-Live (MVP) | 4 agents in production; 1 live customer — MASC (b) | 15% | 65% |
| M4 | Phase 2 UAT Complete | All 7 agents passing UAT; PM + engineering sign-offs | 20% | 85% |
| M5 | Phase 2 Go-Live + Handover | All 7 agents live; GIT + docs + KT delivered — MASC (c) | 10% | 95% |
| M6 | Hypercare Completion | 6-month hypercare concluded; HighRadius eng sign-off | 5% | 100% |


Timeline Reality Assessment
Our honest assessment: the 20-week delivery (Phase 1 at ~Week 12 from Kickoff, Phase 2 at ~Week 20 from Kickoff) represents a 2–3 week slip from the RFP’s Phase 2 target. This gap is mitigatable by overlapping frontend/backend work streams across phases. We prefer transparent honesty over an optimistic plan that fails at execution.


# 4.  Governance & Reporting



## 4.1  Phase Entry & Exit Criteria


Each phase transition is gated by documented entry and exit criteria. No phase begins without the previous phase’s exit criteria being met and signed off:


| Phase | Entry Criteria | Exit Criteria |
| --- | --- | --- |
| Sprint 0 | Signed SOW; HighRadius API access granted; G4 environment available; UX wireframes provided | Architecture signed off; CI/CD operational; G4 OOB evaluation complete; Error State Library created; DB schema v1 approved |
| Phase 1 Dev (Sprints 1–5) | Sprint 0 exit met; design sprint approved; Keycloak integration environment ready | 4 agents feature-complete; 17 screens implemented; ~40 APIs in QA; 80% unit test coverage |
| Phase 1 QA + UAT | All Phase 1 code in QA branch; test data from HighRadius; QA environment stable | E2E passing; API < 3s and Grid < 500ms validated; WCAG passed; UAT sign-off; 1 live customer |
| Phase 2 Dev (Sprints 6–9) | Phase 1 in production; Phase 2 designs approved; ERP sample data available | 3 agents feature-complete; 12 screens implemented; ~27 APIs in QA; 80% unit test coverage |
| Phase 2 QA + Stabilisation | All Phase 2 code merged; full regression suite ready; performance environment configured | Full regression passed; virtual scrolling stress test passed; pen test complete; UAT feedback addressed |
| Full Delivery + Handover | Phase 2 UAT sign-off; all defects resolved or accepted by HighRadius | Production deployed; GIT handover accepted; KT sessions delivered; MASC (a)(b)(c) achieved; infosec clearance obtained |



## 4.2  Weekly Reporting


Metapointer delivers the following to HighRadius stakeholders every week:

•  Written Weekly Status Update: Sprint progress, deliverables completed, blockers, risks, decisions needed

•  PVA (Product Velocity Analysis): Story point velocity, backlog burn-down, sprint goal achievement %, scope variance tracking

•  Defect Report: Open P1–P4 defect counts, MTTD, MTTR, injection rate, leakage rate

•  QA Progress: Test execution status, coverage %, failed cases, performance benchmark results

•  Dependency & Risk Log: Updated status of all 10 dependencies and project risks


## 4.3  Sign-Off Gates


Three mandatory sign-off gates protect delivery integrity:

•  Product Management Sign-Off: 100% module/feature delivery confirmed against requirements. Required before each payment milestone.

•  Engineering Sign-Off: Architecture, code quality, handover completeness, and integration acceptance. Required at Phase 1 and Phase 2 go-live.

•  Infosec Clearance: HighRadius cybersecurity team review and certificate. Required before every production deployment. No exceptions.


# 5.  Risk & Issue Management



## 5.1  Risk Register


All risks are actively tracked and reported weekly. Risk owners are assigned at kickoff and reviewed at every sprint retrospective:


| Risk | Prob. | Impact | Owner | Mitigation |
| --- | --- | --- | --- | --- |
| HighRadius service unavailability (Keycloak, screening, bank validation) | Med | High | HighRadius | Stub/mock all HR-owned services from Sprint 0. Development proceeds unblocked. |
| 16 undesigned screens cause UAT mismatch | Med | High | Shared | Sprint 0 design sprint. UX 1 sprint ahead throughout. Weekly design reviews with HR product team. |
| ERP integration complexity beyond estimates | Med | High | Metapointer | Adapter pattern isolates ERP logic. Synthetic test data in dev. Real ERP in UAT. |
| Scope creep from informal change requests | High | Med | Both | Formal CR process from kickoff. Written sign-off before coding any new requirement. |
| Cross-tenant data isolation defect in production | Low | Critical | Metapointer | 5-layer enforcement. Automated isolation tests every sprint. Pen test pre-production. |
| Timeline slip from delayed HighRadius environment provisioning | Med | Med | HighRadius | Environment provisioning tracked as D1/D7 in dependency register. Escalation path defined. |



## 5.2  Issue Escalation Path


•  Level 1: Metapointer Project Manager resolves within 1 business day for team-level issues

•  Level 2: Escalation to HighRadius SPOC (Single Point of Contact) for cross-team or dependency issues — response within 2 business days

•  Level 3: Escalation to HighRadius Steering Committee for strategic decisions, scope changes, or unresolvable blockers — resolution within 5 business days

•  Emergency path: P1 production incidents bypass normal escalation — direct page to on-call engineer + immediate HighRadius notification


# 6.  Change Management



## 6.1  Change Request Process


All scope changes — whether originating from HighRadius or identified by Metapointer — follow a formal Change Request (CR) process. No change is implemented without written approval:

•  Step 1 — Identification: Change identified and documented by either party. Preliminary description logged in Jira.

•  Step 2 — Impact Assessment: Metapointer assesses impact on scope, timeline, cost, and risks within 3 business days. Assessment documented.

•  Step 3 — Proposal: Formal CR proposal submitted to HighRadius: scope delta, timeline adjustment, cost adjustment (if any), risks.

•  Step 4 — Approval: HighRadius Product Management and Engineering review and approve or reject the CR in writing.

•  Step 5 — Implementation: Approved CR added to sprint backlog with priority assignment. Rejected CR documented with rationale.

•  Step 6 — Tracking: All CRs tracked in Jira CR log, referenced in weekly status reports, and reflected in updated SOW.


## 6.2  Scope Variance Policy


•  0–15% variance: Accommodated within the fixed price. Metapointer absorbs the effort without a CR, provided the change aligns with the intent of the original requirement.

•  >15% variance: Formal Change Request required with cost and timeline impact assessment. Work on the changed item does not begin until written approval is received.

•  New features: Any requirement not in the original SOW is treated as a scope addition and requires a CR regardless of size.

•  Design changes after sign-off: One revision included for vendor-designed screens (16 undesigned screens from UX gap). Additional revisions require a CR.


# 7.  Communication Plan



## 7.1  Communication Cadence



| Communication | Frequency | Format | Participants | Purpose |
| --- | --- | --- | --- | --- |
| Weekly Status Update | Weekly — every Monday | Written report + email | PM + HighRadius SPOC | Sprint progress, blockers, risks, decisions needed |
| PVA Report | Weekly | Structured report | PM + HighRadius PM | Velocity, burn-down, scope variance, dependency status |
| Sprint Demo | Bi-weekly (end of sprint) | Live demo call | Full team + HighRadius stakeholders | Demonstrate completed features; gather feedback; get sign-off |
| Design Review | Weekly during design phases | Screen review call | UX + HighRadius Product | Review and approve UX designs before development begins |
| Defect Review | Weekly | Jira dashboard review | QA + HighRadius QA | Open defects, aging, resolution status, UAT readiness |
| Steering Committee | Monthly or on escalation | Formal meeting | Leadership + Sponsors | Strategic decisions, scope changes, programme health |
| Sprint Retrospective | Bi-weekly | Internal + shared | Full Metapointer team + HighRadius PM | Process improvement; risks; team health |



## 7.2  RACI Summary


Key responsibilities for the delivery programme (R = Responsible, A = Accountable, C = Consulted, I = Informed):


| Activity | Metapointer | HighRadius | Notes |
| --- | --- | --- | --- |
| UI/UX Development (29 screens + 11 modals) | R, A | C, I | Vendor builds; HR provides wireframes and sign-off |
| Backend Services (58 vendor-built APIs) | R, A | C | Vendor full ownership |
| Keycloak IAM (Auth/Login/SSO) | I | R, A | HR-owned; vendor integrates only |
| Screening & Bank Validation Services | C | R, A | HR-owned; vendor builds integration + stores results |
| ERP Integration (SAP/Oracle/NetSuite) | R | A, C | Vendor builds adapters; HR provides API access |
| Multi-Tenant Architecture | R, A | C | Vendor designs and implements isolation |
| Testing & QA (all types) | R, A | C | Vendor owns QA; HR provides test data and UAT sign-off |
| DevOps / CI-CD Pipeline | R | A, C | Vendor sets up per HR engineering practices |
| Product Requirements & UX Specs | C | R, A | HR provides; vendor implements |
| Hypercare Support (6 months) | R | A, I | Vendor provides 0.5 FTE |
| Knowledge Transfer & Handover | R | A | Completion requires HR engineering sign-off |


Single Point of Contact
HighRadius is requested to designate a Single Point of Contact (SPOC) with authority to make decisions on product requirements, design approvals, and issue resolution. A clear SPOC dramatically reduces the risk of delayed sign-offs and requirement ambiguity — two of the highest-probability risks in this delivery.