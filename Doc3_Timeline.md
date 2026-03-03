# AP SUPPLIER PORTAL — PROJECT TIMELINE & DELIVERY PLAN

| Field | Detail |
|-------|--------|
| **Document** | Timeline & Delivery Plan |
| **Version** | 3.3 |
| **Date** | February 28, 2026 |
| **Client** | HighRadius Corporation |
| **Project** | AP Supplier Portal Development & Deployment |
| **Service Provider** | Metapointer |
| **Status** | READY FOR SUBMISSION |

> **Confidentiality Notice:** This document contains proprietary and confidential information. Distribution is restricted to authorized HighRadius and Metapointer personnel only.

> **Cross-References:**
> - Executive Summary & Business Understanding → *Proposal PDF document*
> - Scope of Work & Solution Overview → *Scope of Work document*
> - Solution Architecture & Security → *Tech Specs document*
> - Commercial Terms & Pricing → *Commercial Agreement document*

---

## Table of Contents

1. [Project Plan & Milestones](#1-project-plan--milestones)
   - 1.1 [Phase Breakdown](#11-phase-breakdown)
   - 1.2 [Timeline](#12-timeline)
   - 1.3 [Calendar Estimates by Discipline](#13-calendar-estimates-by-discipline)
   - 1.4 [Timeline Reality Assessment](#14-timeline-reality-assessment)
   - 1.5 [Key Deliverables](#15-key-deliverables)
2. [Delivery Approach](#2-delivery-approach)
   - 2.1 [Engagement Model & Sprint Cadence](#21-engagement-model--sprint-cadence)
   - 2.2 [Agent-Level KPI Definitions](#22-agent-level-kpi-definitions)
   - 2.3 [Definition of Done](#23-definition-of-done)
   - 2.4 [Defect Management Lifecycle](#24-defect-management-lifecycle)
   - 2.5 [Requirement Mismatch & UAT Rework Policy](#25-requirement-mismatch--uat-rework-policy)
   - 2.6 [Phase-Level Entry & Exit Criteria](#26-phase-level-entry--exit-criteria)
   - 2.7 [Communication & Reporting Plan](#27-communication--reporting-plan)
3. [DevOps & Release Management](#3-devops--release-management)
   - 3.1 [CI/CD & Deployment](#31-cicd--deployment)
   - 3.2 [Monitoring & Observability](#32-monitoring--observability)
4. [Team Structure](#4-team-structure)
5. [Documentation & Knowledge Transfer](#5-documentation--knowledge-transfer)

---

## 1. Project Plan & Milestones

**Classification: PROJECT-SPECIFIC**

### 1.1 Phase Breakdown

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

### 1.2 Timeline

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

### 1.3 Calendar Estimates by Discipline

Based on actual team composition (3 FE + 2 BE + 1 QA, all with Claude Opus AI). All estimates are AI-adjusted:

| Discipline | Team Size | Working Days | Calendar Weeks | Notes |
|-----------|-----------|-------------|----------------|-------|
| Frontend Development | 3 developers | 72 days | ~15 weeks | Parallel execution across 3 devs; AI multiplier on code + unit tests |
| Backend Development | 2 developers | 77 days | ~16 weeks | Includes DevOps, observability; AI multiplier on services + APIs |
| QA Engineering | 1 engineer | ~44 weeks total | ~40% overlaps with dev | E2E, performance, security, WCAG; unit tests written by devs |
| Sprint 0 (Foundation) | Full team | 10 days | 2 weeks | Architecture, design sprint, CI/CD setup, G4 component evaluation |

- Frontend and backend streams run in parallel, with QA overlapping ~40% with active development sprints
- Critical path is backend at ~16 weeks, with frontend completing within the same window
- QA effort extends beyond dev completion for final regression, performance, and security testing

### 1.4 Timeline Reality Assessment

The HighRadius RFP defines three delivery milestones. Our honest assessment with a 7-person team:

| RFP Milestone | RFP Target | Our Realistic Target | Gap | Notes |
|--------------|-----------|---------------------|-----|-------|
| MVP (4 agents) | Feb 2026 | Mid-May 2026 | ~2.5 months | MVP and Phase 1 combined (both = 4 agents, 1 month apart in RFP) |
| Phase 1 (4 agents) | March 2026 | Mid-May 2026 | ~2 months | Treated as combined Phase 1/MVP delivery |
| Phase 2 (3 agents) | June 2026 | Early July 2026 | ~2–3 weeks | Mitigatable by overlapping FE/BE work streams across phases |

**Recommendation:** Deliver in two phases aligned to RFP agent structure. Phase 1 (4 agents) targets production by mid-May 2026 with 1 live customer. Phase 2 (3 agents) targets full delivery by early July 2026. The 2–3 week gap from the June RFP target is mitigatable by overlapping frontend/backend work streams. Total: 20 calendar weeks from kickoff.

### 1.5 Key Deliverables

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

> *For detailed scope of each agent and screen-level breakdown, refer to the **Scope of Work document**.*

---

## 2. Delivery Approach

**Classification: STANDARD CORE + PROJECT ADAPTATION**

*[Standard Metapointer Agile delivery methodology applies]*

### 2.1 Engagement Model & Sprint Cadence

**Project-Specific Adaptations:**
- **Engagement Model:** Fixed-Price with defined scope and milestone-based payments (10–15% scope variance allowance per RFP engagement model)
- **Sprint Cadence:** 2-week sprints (10 sprints total: Sprint 0 + Sprints 1–9)
- **Phase 1 (MVP):** Sprints 0–5 — 4 agents (Onboarding, Screening, Bank Validation, Approval)
- **Phase 2:** Sprints 6–9 — 3 agents (Purchase Order, Invoice Creation, Master Data Change Approval)
- **Communication Cadence:** Weekly status calls with HighRadius, weekly email updates and PVA (Product Velocity Analysis) on deliverables
- **Governance:** Steering committee reviews, defect management SLAs, change control per Change Management Process
- **Scope Variance Management:** Per RFP engagement model, a 10–15% variance in defined deliverables is acceptable. Variance is tracked sprint-over-sprint through story point velocity and backlog burn-down. Any variance exceeding 15% triggers the formal Change Request process with impact assessment on timeline and cost
- **MASC (Success Criteria):** (a) UAT delivery, (b) 1 live customer in production, (c) 90%+ KPI achievement per agent

**Vendor Commitments per RFP Section 5:**
- Design collaboration with HighRadius engineering team with timely sign-offs
- Feature-level technical design documentation
- Functional and regression test cases (JUnit + functional)
- QA completed before delivery to HighRadius
- Handover repository: GIT, design docs, KT sessions, all project resources

**Sign-Off Gates:** Product Management (100% module/feature delivery), Engineering (architecture & handover), Infosec (cybersecurity clearance)

### 2.2 Agent-Level KPI Definitions

For MASC Milestone (c) — 90%+ Achievement Required:

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

### 2.3 Definition of Done

A feature/story is Done only when ALL criteria are met:

1. **Code Complete:** Feature implementation finished, clean, follows coding standards, self-reviewed
2. **Unit Tests Written & Passing:** Minimum 80% coverage (Jest for frontend, JUnit for backend), all tests pass in CI
3. **Code Reviewed:** PR reviewed and approved by at least 1 peer (logic, security, performance, architecture)
4. **Integration Tested:** Feature works end-to-end across FE and BE; API contracts validated; HR service integration verified
5. **No Critical/High Bugs:** No open critical or high-severity bugs; medium/low documented and triaged
6. **Documentation Updated:** API documentation (Swagger), technical design doc, and runbooks updated
7. **Security Scanned:** SAST passed with no critical/high findings; CSP verified; RBAC/ABAC validated
8. **Deployed to QA:** Feature deployed via CI/CD and smoke tested
9. **Acceptance Criteria Met:** All criteria verified and demonstrated

### 2.4 Defect Management Lifecycle

All defects follow a standardized lifecycle from discovery through resolution and closure. The SLA targets below are project-specific commitments aligned to HighRadius's operational expectations and RFP requirements. This applies to both in-sprint defects and production incidents.

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

### 2.5 Requirement Mismatch & UAT Rework Policy

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

### 2.6 Phase-Level Entry & Exit Criteria

| Phase | Entry Criteria | Exit Criteria |
|-------|---------------|--------------|
| Sprint 0 (Foundation) | Signed SOW; HighRadius API access granted; G4 environment available; UX wireframes provided | Architecture document signed off; CI/CD pipeline operational; G4 OOB component evaluation complete; Validation Error State Library created; DB schema v1 approved |
| Phase 1 Development (Sprints 1–5) | Sprint 0 exit criteria met; design sprint outputs approved; Keycloak integration environment ready | 4 agents feature-complete; 17 screens implemented; ~40 APIs deployed to QA; unit tests at 80% coverage |
| Phase 1 QA + UAT | All Phase 1 code merged to QA branch; test data provided by HighRadius; QA environment stable | E2E tests passing; API response <3s validated; Grid <500ms validated; WCAG audit passed; UAT sign-off from HighRadius; 1 live customer in production |
| Phase 2 Development (Sprints 6–9) | Phase 1 in production; Phase 2 design specs approved; ERP sample data for PO/Invoice flows available | 3 agents feature-complete; 12 screens implemented; ~26 APIs deployed to QA; unit tests at 80% coverage |
| Phase 2 QA + Stabilization | All Phase 2 code merged; full regression suite ready; performance test environment configured | Full regression passed; virtual scrolling stress test passed; penetration test completed; UAT feedback addressed |
| Full Delivery + Handover | Phase 2 UAT sign-off; all defects resolved or deferred with HighRadius approval | Production deployment complete; GIT handover accepted; KT sessions delivered; MASC criteria (a)(b)(c) achieved; infosec clearance obtained |

### 2.7 Communication & Reporting Plan

**Classification: STANDARD**

*[Standard Metapointer section — communication cadence, reporting formats, and escalation protocols to be populated from Metapointer standard template]*

---

## 3. DevOps & Release Management

**Classification: STANDARD CORE + PROJECT ADAPTATION**

*[Standard Metapointer CI/CD framework applies]*

### 3.1 CI/CD & Deployment

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

### 3.2 Monitoring & Observability

Production reliability requires comprehensive observability across application performance, logging, infrastructure metrics, and business KPIs. The observability stack integrates with HighRadius G4 platform capabilities.

| Observability Layer | Tools / Approach | What It Monitors |
|--------------------|-----------------|-----------------|
| **Application Performance** | APM integration (G4 platform compatible) | API response times, error rates, throughput, slow queries |
| **Structured Logging** | Centralized log aggregation (ELK/Fluentd) | Application logs, audit events, integration call traces |
| **Infrastructure Metrics** | Kubernetes-native monitoring (Prometheus/Grafana) | CPU, memory, disk, pod health, replica counts, network I/O |
| **Business KPIs** | Custom dashboards | Onboarding cycle time, screening pass rates, invoice processing SLA, approval queue depth |
| **Real-Time Alerting** | PagerDuty/OpsGenie integration | Technical incidents (P1/P2 auto-page), business anomalies (screening failure spike, queue backlog) |
| **Health Checks** | Kubernetes liveness + readiness probes | Every 5 minutes; auto-restart on failure; traffic routing on readiness |

> *For detailed architecture of monitoring infrastructure, refer to the **Tech Specs document**.*

---

## 4. Team Structure

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

**AI Tooling:** All 6 engineers equipped with Claude Opus AI subscriptions for 1.10x–1.50x productivity gains across coding, testing, and documentation activities.

---

## 5. Documentation & Knowledge Transfer

**Classification: STANDARD**

*[Standard section — to be populated with Metapointer standard template]*

*This section will cover: Architecture documentation, API documentation (OpenAPI/Swagger), Deployment guides & runbooks, KT session structure & schedule, Handover acceptance criteria.*

---

*Prepared By: Metapointer | For: HighRadius Corporation | Date: February 28, 2026*
