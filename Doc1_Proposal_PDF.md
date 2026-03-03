# AP SUPPLIER PORTAL — ENTERPRISE PROPOSAL

| Field | Detail |
|-------|--------|
| **Document** | Executive Proposal |
| **Version** | 3.3 |
| **Date** | February 28, 2026 |
| **Client** | HighRadius Corporation |
| **Project** | AP Supplier Portal Development & Deployment |
| **Service Provider** | Metapointer |
| **Status** | READY FOR SUBMISSION |

> **Confidentiality Notice:** This document contains proprietary and confidential information. Distribution is restricted to authorized HighRadius and Metapointer personnel only.

> **Companion Documents:**
> - Detailed Scope of Work → *Scope of Work document*
> - Solution Architecture & Security → *Tech Specs document*
> - Timeline, Milestones & Delivery Approach → *Timeline document*
> - Past Experience & Credibility → *Case Studies document*
> - Commercial Terms, Legal & Pricing → *Commercial Agreement document*

---

## Table of Contents

1. [Cover Page](#1-cover-page)
2. [Document Control](#2-document-control)
3. [Executive Summary](#3-executive-summary)
   - 3.1 [Business Context](#31-business-context)
   - 3.2 [Problem Statement](#32-problem-statement)
   - 3.3 [Proposed Solution](#33-proposed-solution)
   - 3.4 [Timeline Summary](#34-timeline-summary)
   - 3.5 [Commercial Summary](#35-commercial-summary)
4. [Business Understanding](#4-business-understanding)
   - 4.1 [Current State](#41-current-state)
   - 4.2 [Key Challenges](#42-key-challenges)
   - 4.3 [Compliance & Audit Risk Exposure](#43-compliance--audit-risk-exposure)
   - 4.4 [Cost of Inaction](#44-cost-of-inaction)
   - 4.5 [Target State](#45-target-state)
   - 4.6 [Business Outcomes & ROI Indicators](#46-business-outcomes--roi-indicators)
   - 4.7 [Assumptions](#47-assumptions)
   - 4.8 [Constraints](#48-constraints)
   - 4.9 [Dependencies (Client / Third Party)](#49-dependencies-client--third-party)
5. [About Metapointer](#5-about-metapointer)

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

> *For complete scope, deliverables breakdown, and gap analysis, refer to the **Scope of Work document**.*
> *For detailed architecture, security matrices, and enforcement model, refer to the **Tech Specs document**.*

### 3.4 Timeline Summary

- **Kickoff:** March 2026
- **Sprint 0 (Foundation):** 2 weeks — architecture, DevOps setup, G4 component evaluation & scaffolding, design sprint
- **Phase 1 (MVP):** 4 agents (Onboarding, Screening, Bank Validation, Approval) — Sprints 1–5 (10 weeks) — UAT + 1 live customer by mid-May 2026
- **Phase 2:** 3 agents (Purchase Order, Portal Invoice Creation, Master Data Change Approval) — Sprints 6–9 (8 weeks) — Full delivery by early July 2026
- **Hypercare:** 6 months post-go-live through January 2027 with production support and knowledge transfer
- **Total Duration:** 20 calendar weeks aligned to RFP milestones with built-in risk buffers

> *For detailed sprint breakdown, milestones, and delivery approach, refer to the **Timeline document**.*

### 3.5 Commercial Summary

- **Engagement Model:** Fixed-Price with defined scope and deliverables
- **Payment Structure:** Milestone-based with Go/No-Go gates (5 milestones: 20%–30%–20%–20%–10%)
- **Detailed Pricing:** Provided in separate Pricing Agreement document
- **Change Management:** Formal change control process for scope modifications

> *For detailed pricing, milestone payment plan, and legal terms, refer to the **Commercial Agreement document**.*

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

## 5. About Metapointer

**Classification: STANDARD**

*[Standard section — to be populated with Metapointer standard template]*

> *For detailed past experience, case studies, and credibility, refer to the **Case Studies document**.*

---

*Prepared By: Metapointer | For: HighRadius Corporation | Date: February 28, 2026*
