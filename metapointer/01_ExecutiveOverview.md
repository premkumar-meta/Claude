Executive Overview

AP Supplier Portal

Prepared for:  HighRadius Corporation

Prepared by:  Metapointer Labs Pvt. Ltd.

Date:  March 2026

Version:  3.3

Table of Contents

1.  Project Context & Business Problem	3

1.1  Business Context	3

1.2  Problem Statement	3

2.  Project Objectives	5

3.  Proposed Solution Overview	6

3.1  Agent Architecture	6

3.2  Technology Stack	6

3.3  End-to-End Process Flow	7

4.  Scope Summary	10

5.  Delivery Timeline	11

6.  Team Composition	12

7.  Project Cost	13

8.  Key Assumptions & Dependencies	14

9.  Major Risks	15

10.  Why Metapointer — Key Differentiators	16


# 1.  Project Context & Business Problem



## 1.1  Business Context


HighRadius is a fintech enterprise SaaS provider delivering an Agentic AI platform for the Office of the CFO. Its cloud solutions span the end-to-end Order-to-Cash (O2C) cycle, Accounts Payable, Treasury Management, Record-to-Report, and B2B Payments — integrating 180+ AI agents to orchestrate financial processes at scale. Adopted by over 1,100 leading enterprises including 3M, Unilever, Procter & Gamble, and Johnson & Johnson, HighRadius is consistently recognised as a market leader by Gartner, IDC, and Forrester.

As part of its expanding AP automation capabilities, HighRadius requires a robust Supplier Portal to streamline vendor management operations across its customer base. The portal will serve as a unified platform for buyers to onboard suppliers, manage vendor relationships, and for suppliers to receive purchase orders, submit invoices, and track their status — fully integrated with HighRadius’s G4 platform and supporting multi-tenant environments handling diverse ERPs including SAP, Oracle, and NetSuite.


## 1.2  Problem Statement


Current AP operations at HighRadius rely on manual, fragmented processes that create significant operational and financial risk:

•  Onboarding Delays: Email-based supplier onboarding takes 15–20 days with inconsistent data collection, processing 50–100+ suppliers per quarter. Extended activation delays result in lost early-payment discounts and strained buyer-supplier relationships.

•  Compliance Gaps: Only ~30% of suppliers are screened against sanctions and identity databases, creating exposure to OFAC violations ($20M+ fines), tax/identity fraud from error-prone TIN verification, and banking fraud from unvalidated account changes. No centralised audit trails exist.

•  Invoice Processing Inefficiency: Manual channels (email, fax, manual entry) yield only ~60% SLA compliance with high error rates, late penalties, and forecasting inaccuracies. Each event involves 12–15 manual touchpoints across hundreds to thousands of invoices monthly.

•  Operational Overhead: 60–70% of AP team time is spent on transactional work rather than strategic activities. 100% of supplier interactions require full buyer intervention with no self-service capability.

•  Visibility & Data Silos: Supplier data is scattered across ERPs, spreadsheets, and emails — no single source of truth, manual reports, and delayed decision-making across all stakeholders.


| Risk Area | Current Exposure | Financial Impact |
| --- | --- | --- |
| Sanctions Risk | ~70% of suppliers unscreened against OFAC, EU, and UN sanctions lists | Fines up to $20M+ per violation; reputational damage |
| Tax / Identity Fraud | Manual TIN verification — error-prone and inconsistent | Incorrect 1099 reporting; IRS penalties and audit exposure |
| Banking Fraud | Bank account changes processed without automated validation | Primary BEC fraud vector; direct financial loss |
| Audit Trail Gaps | No centralised audit trail; actions scattered across emails and spreadsheets | Inability to demonstrate compliance; regulatory penalties |



# 2.  Project Objectives


The AP Supplier Portal is designed to transform HighRadius’s accounts payable operations from a manual, fragmented model into a fully digitised, automated, and scalable ecosystem. The following table defines the current state, target state, and expected impact:


| Objective Area | Current State | Target State |
| --- | --- | --- |
| Supplier Onboarding Speed | 15–20 days, email-driven | 3–5 days, automated with real-time screening |
| Compliance Coverage | ~30% of suppliers screened | 100% automated compliance checks on every submission |
| Invoice SLA Compliance | ~60% | >90% with automated field validation and workflow |
| First-Pass Invoice Accuracy | ~65% | >95% via PO-flip and field-level validation |
| Supplier Self-Service | 0% — full buyer intervention required | >80% adoption target — self-service portal access |
| Manual Touchpoints per Event | 12–15 | 80%+ reduction through intelligent automation |
| Audit Trail | Scattered across emails and spreadsheets | Centralised, immutable, 2-year retention |
| Data Visibility | Manual reports, delayed decisions | Real-time dashboards and KPI tracking for all personas |


Value Realization Timeline
Months 1–3 (Post Go-Live): Onboarding cycle reduction, screening automation, initial self-service adoption. Months 3–6: Invoice SLA improvements, dashboard-driven decisions, supplier satisfaction gains. Months 6–12: Full ROI realization — cost savings, compliance maturity, and scalability proven through tenant expansion.


# 3.  Proposed Solution Overview


The Supplier Portal is a secure, scalable, self-service web application structured around 7 intelligent agents (4 automated, 3 assisted) across three personas, delivering 29 screens + 11 modals with 66 APIs (58 vendor-built, 7 integrations, 1 orchestration) and 25+ core features. The portal integrates directly with the HighRadius G4 platform and supports multi-tenant enterprise environments.


## 3.1  Agent Architecture



| Agent | Type | Key Capabilities |
| --- | --- | --- |
| Supplier Onboarding | Automated | Individual and bulk (CSV) invitations; dynamic multi-language forms; document upload and validation; draft save and resume; duplicate detection |
| Supplier Screening | Automated | Real-time parallel checks: address verification, TIN validation, OFAC sanctions screening; actionable error feedback and retry |
| Bank Account Validation | Automated | Real-time bank detail verification; ownership validation; fraud prevention against BEC attacks |
| Supplier Approval | Assisted | Multi-level configurable workflows; conditional routing by spend threshold or region; SLA-based auto-escalation; approve, reject, reassign |
| Master Data Change Approval | Assisted | Orchestrates approval workflows for supplier data updates and payment term changes with conditional routing |
| Purchase Order | Automated | Multi-ERP PO import and sync (SAP, Oracle, NetSuite); supplier acknowledgement and rejection; real-time status tracking |
| Portal Invoice Creation | Assisted | Manual invoice entry and one-click PO-flip; partial invoicing; tax and discount lines; attachments; AP synchronisation |



## 3.2  Technology Stack



| Layer | Technology | Details |
| --- | --- | --- |
| Frontend | React 18.x + HighRadius G4 DSL | WCAG 2.0 AA accessibility; virtual scrolling for 1,000+ row grids |
| Backend | Spring Boot 3.x (Java 17+) | Stateless microservices architecture; horizontal scaling |
| Database | PostgreSQL (OLAP) | Schema-per-tenant; row-level security; 100% data isolation |
| Security | Keycloak IAM + HashiCorp Vault | OIDC/JWT SSO; RBAC/ABAC; TLS 1.3; AES-256 encryption |
| Deployment | Docker + Kubernetes | Containerised deployment in HighRadius G4 environment |
| AI Tooling | Claude Opus AI | 1.10x–1.50x productivity gains across all 6 engineers |



## 3.3  End-to-End Process Flow


The diagram below illustrates the complete supplier lifecycle from invitation through payment, covering both Phase 1 (Onboarding & Compliance) and Phase 2 (Transactional Enablement):

Figure 1: AP Supplier Portal — End-to-End Process Flow


# 4.  Scope Summary


The following summary provides a high-level view of the quantified deliverables covered under this engagement:


| Deliverable | Count | Detail |
| --- | --- | --- |
| Intelligent Agents | 7 | 4 Automated + 3 Assisted across the full supplier lifecycle |
| Application Screens | 29 | Across Supplier, Supplier Manager, and Admin personas |
| Popup / Modal Workflows | 11 | Confirmation, action, preview, and configuration modals |
| APIs (Vendor-Built) | 58 | Full end-to-end ownership: design, implement, test, deploy |
| APIs (HR Integrations) | 7 | HighRadius-owned services; vendor builds adapter/integration layer |
| APIs (Orchestration) | 1 | Vendor-built orchestration coordinating multiple HR services |
| Total APIs | 66 | Complete API surface across all agents and cross-cutting services |
| Core Features | 25+ | Onboarding, screening, approval, PO, invoice, dashboards, admin |
| Personas Supported | 4 | Supplier, Supplier Manager, Approver, HighRadius/Client Admin |


UI Gap Analysis Accounted For
48 gaps identified across the 91-page HighRadius wireframes have been fully accounted for in our estimation: 16 missing screens designed from scratch, 12 validation states, 7 logic complexity gaps, 9 technical gaps, and 6 workflow gaps. All are included in delivery scope with no hidden costs.


# 5.  Delivery Timeline


The programme is structured across Sprint 0 (Foundation), Phase 1 (MVP — 4 agents), and Phase 2 (Transactional Enablement — 3 agents), delivering a 20-week programme with 6 months of hypercare post go-live:


| Sprint / Phase | Weeks | Focus | Milestone |
| --- | --- | --- | --- |
| Sprint 0 | 1–2 | Architecture, DevOps setup, design sprint, G4 evaluation, Validation Error State Library | Design Sign-off |
| Sprints 1–2 | 3–6 | Supplier Onboarding Agent + Supplier Screening Agent | — |
| Sprints 3–4 | 7–10 | Bank Validation + Supplier Approval + Core Dashboards | — |
| Sprint 5 | 11–12 | Integration testing, UAT preparation, performance validation | Phase 1 (MVP) UAT Complete |
| Phase 1 (MVP) Go-Live | ~Week 12 from Kickoff | 4 agents in production (Onboarding, Screening, Bank Validation, Approval) | 1 Live Customer |
| Sprints 6–7 | 13–16 | Purchase Order Agent + Portal Invoice Creation Agent | — |
| Sprints 8–9 | 17–20 | Master Data Change Approval Agent + full integration hardening + handover | Phase 2 UAT Complete |
| Full Go-Live | ~Week 20 from Kickoff | Complete portal in production with all 7 agents | Full Delivery & Handover |
| Hypercare | Months 5–11 from Kickoff (6-month Hypercare) | 6-month post-go-live support at 0.5 FTE; SLA monitoring and KT | Hypercare Closure |



# 6.  Team Composition


The engagement is delivered by a dedicated team of 7 FTE across a 20-week (5-month) core delivery, followed by 6-month hypercare at 0.5 FTE. All team members are equipped with Claude Opus AI subscriptions delivering 1.10x–1.50x productivity multipliers across development, testing, and documentation activities:


| Role | Count | FTE-Months | Project Focus |
| --- | --- | --- | --- |
| Architect / Technical Lead | 1 | 5 | System design, G4 integration, code quality, performance optimisation |
| Senior Backend Engineers | 2 | 10 | Microservices, API implementation, database design, DevOps pipelines |
| Frontend Engineers | 3 | 15 | UI/UX with G4 DSL, responsive design, WCAG 2.0 AA compliance |
| QA Engineer | 1 | 5 | E2E automation, performance testing, security validation, WCAG testing |
| Project Manager | 1 | 5 | Timeline management, stakeholder communication, risk tracking, PVA reporting |
| Hypercare Support | 0.5 | 3 | Production monitoring, performance tuning, KT, issue resolution |
| **Total** | **7 + 0.5** | **38** | **20-week core delivery + 6-month hypercare at 0.5 FTE** |



# 7.  Project Cost


This engagement is structured as a Fixed-Price delivery model, providing HighRadius with full cost certainty from kickoff to final handover. The fixed-price commitment is backed by our detailed scope analysis, effort estimation, and AI-assisted productivity model.

•  Engagement Model: Fixed-Price with defined scope and milestone-based payments. No cost overrun risk for HighRadius within the agreed scope.

•  Payment Structure: 6 milestones: 30%–20%–15%–20%–10%–5%, each tied to a verified delivery gate. 30% advance on contract signing; final 5% released on Hypercare completion (6 months post Phase 2 Go-Live).


| M# | Milestone | Trigger | % | Cumulative |
| --- | --- | --- | --- | --- |
| M1 | Advance — Contract Signing | Contract executed; mobilisation begins | 30% | 30% |
| M2 | Phase 1 UAT Complete | 4 agents passing UAT; PM sign-off; 80%+ coverage — MASC (a) | 20% | 50% |
| M3 | Phase 1 Go-Live (MVP) | 4 agents in production; 1 live customer — MASC (b) | 15% | 65% |
| M4 | Phase 2 UAT Complete | All 7 agents passing UAT; PM + engineering sign-offs | 20% | 85% |
| M5 | Phase 2 Go-Live + Handover | All 7 agents live; GIT + docs + KT delivered — MASC (c) | 10% | 95% |
| M6 | Hypercare Completion | 6-month hypercare concluded; HighRadius eng sign-off | 5% | 100% |


•  Change Management: Formal change control process for any scope modifications. Up to 10–15% scope variance is accommodated without additional cost.

•  Detailed Pricing: Full pricing breakdown, milestone payment schedule, and legal terms are provided in the separate Commercial & Legal document (Document 6).

Cost Certainty Guarantee
The fixed-price model means HighRadius pays exactly what is agreed — regardless of actual hours incurred. Scope changes are formally managed and never silently absorbed into the base price. Every milestone payment is contingent on verified delivery acceptance.


# 8.  Key Assumptions & Dependencies


The following dependencies are owned by HighRadius and are critical path items. Each has a documented mitigation strategy to protect delivery continuity:


| # | Dependency | Owner | Impact if Delayed | Mitigation |
| --- | --- | --- | --- | --- |
| D1 | Keycloak IAM environment provisioned and accessible | HighRadius | Blocks authentication development; delays Sprint 1+ | Mock IAM layer for dev; parallel integration once available |
| D2 | G4 DSL component library and documentation | HighRadius | Blocks frontend development; forces custom component builds | Evaluate OOB components in Sprint 0; fallback to plain React |
| D3 | Screening service API (sanctions, TIN, address) | HighRadius | Blocks Supplier Screening Agent | Stub/mock API responses for dev and QA; integrate when live |
| D4 | Bank validation API access | HighRadius | Blocks Bank Account Validation Agent | Same stub approach; validate with real API in UAT |
| D5 | ERP sample data (SAP/Oracle/NetSuite) for PO and Invoice | HighRadius | Blocks PO and Invoice agent development and testing | Generate synthetic test data; validate with real ERP in UAT |
| D6 | UX wireframes and design specs for 16 undesigned screens | HighRadius | Forces vendor-designed screens; increases mismatch risk | Sprint 0 design sprint; UX 1 sprint ahead of dev throughout |
| D7 | QA / UAT environment provisioned | HighRadius | Blocks testing phases; delays go-live | Use dev environment for early testing; escalate in Sprint 0 |
| D8 | Stakeholder availability for reviews and approvals | HighRadius | Delays sign-offs; blocks phase transitions | RACI defined in Sprint 0; escalation matrix for delays |
| D9 | Infosec clearance review slots | HighRadius | Blocks production deployment | Submit for clearance early (during QA phase); parallel track |
| D10 | HashiCorp Vault access for secrets management | HighRadius | Blocks secure credential storage implementation | Use environment variables in dev; integrate Vault pre-UAT |



# 9.  Major Risks


The following risks have been identified, quantified, and mitigated within our delivery plan. All risks are actively tracked throughout the programme:


| Risk | Probability | Impact | Mitigation Strategy |
| --- | --- | --- | --- |
| HighRadius service unavailability (Keycloak, screening, bank validation) | Medium | High | Stub/mock all HR-owned services from Sprint 0. Development proceeds unblocked; real integration validated in UAT. |
| 16 undesigned screens create UX mismatch at demo | Medium | High | Sprint 0 design sprint covers all 16 screens. UX 1 sprint ahead of development throughout. Weekly design reviews with HR product team. |
| ERP integration complexity (multi-customer SAP/Oracle/NetSuite) | Medium | High | Adapter pattern isolates ERP-specific logic. Synthetic test data covers dev phase. Real ERP validation in UAT. |
| Timeline delay from late Keycloak environment provisioning | Medium | Medium | Mock IAM layer built in Sprint 0. Keycloak integration parallelised once available. Escalation path defined in RACI. |
| Scope creep through informal change requests | High | Medium | Formal Change Request process enforced from kickoff. Written sign-off required before coding begins on any new requirement. |
| Multi-tenant isolation defect discovered late in testing | Low | Critical | Automated tenant isolation tests run from Sprint 1. Schema-per-tenant + RLS acts as safety net. Cross-tenant prevention validated every sprint. |



# 10.  Why Metapointer — Key Differentiators


Metapointer brings a combination of deep fintech domain knowledge, enterprise-grade delivery methodology, and AI-powered engineering capability that is uniquely suited to the HighRadius AP Supplier Portal engagement:

•  Deep RFP Comprehension: Our response is built on a detailed analysis of the 91-page HighRadius wireframes, identifying 48 gaps and accounting for all of them within our estimation and delivery plan. No hidden scope, no surprise change requests.

•  AI-Powered Engineering Team: All 6 engineers use Claude Opus AI, delivering 1.10x–1.50x productivity multipliers on code generation, unit test writing, API documentation, and integration work. This directly translates to faster delivery and higher quality output within the fixed price.

•  Proven Fixed-Price Discipline: Our fixed-price model is backed by bottom-up effort estimation at the screen, workflow, and API level. HighRadius gets complete cost certainty with no budget overrun risk within the agreed scope.

•  G4-Native Architecture: The solution is architected specifically for the HighRadius G4 environment — React 18.x + G4 DSL frontend, Spring Boot 3.x microservices, Keycloak integration, and containerised deployment. No rework required to fit your platform.

•  Multi-Tenant Security-First Design: Schema-per-tenant with row-level security and a 5-layer enforcement chain (Frontend → API Gateway → Service → Database → Audit) ensures 100% data isolation. Compliance is built into architecture, not bolted on.

•  Transparent Risk Ownership: We clearly document what is our responsibility and what depends on HighRadius. Our RACI matrix and dependency register protect both parties. Risks are identified early and mitigated proactively — not discovered at go-live.

•  Hypercare Commitment: 6 months of post-go-live hypercare at 0.5 FTE ensures a smooth transition to operations. Knowledge transfer, runbooks, and production support are included — not optional extras.