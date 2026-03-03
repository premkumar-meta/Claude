# AP SUPPLIER PORTAL — COMMERCIAL AGREEMENT & CONTRACTUAL TERMS

| Field | Detail |
|-------|--------|
| **Document** | Commercial Agreement (MSA) |
| **Version** | 3.3 |
| **Date** | February 28, 2026 |
| **Client** | HighRadius Corporation |
| **Project** | AP Supplier Portal Development & Deployment |
| **Service Provider** | Metapointer |
| **Status** | READY FOR SUBMISSION |

> **Confidentiality Notice:** This document contains proprietary and confidential information. Distribution is restricted to authorized HighRadius and Metapointer personnel only.

> **Cross-References:**
> - Executive Summary & Business Understanding → *Proposal PDF document*
> - Scope of Work & Deliverables → *Scope of Work document*
> - Solution Architecture & Security → *Tech Specs document*
> - Timeline, Milestones & Delivery Approach → *Timeline document*

---

## Table of Contents

1. [Commercial Proposal](#1-commercial-proposal)
   - 1.1 [Pricing Structure](#11-pricing-structure)
   - 1.2 [Milestone Payment Plan](#12-milestone-payment-plan)
   - 1.3 [Invoicing Terms](#13-invoicing-terms)
   - 1.4 [Assumptions](#14-assumptions)
   - 1.5 [Change Billing Model](#15-change-billing-model)
2. [Legal & Contractual Terms](#2-legal--contractual-terms)
3. [Support & Warranty Model](#3-support--warranty-model)
   - 3.1 [Hypercare Terms](#31-hypercare-terms)
   - 3.2 [Support SLAs](#32-support-slas)
   - 3.3 [Escalation Matrix](#33-escalation-matrix)
   - 3.4 [Handover Repository](#34-handover-repository)
4. [Change Management Process](#4-change-management-process)
5. [Risk Management](#5-risk-management)
   - 5.1 [Project-Specific Risks](#51-project-specific-risks)
   - 5.2 [Disaster Recovery & Business Continuity](#52-disaster-recovery--business-continuity)

---

## 1. Commercial Proposal

**Classification: PROJECT-SPECIFIC**

### 1.1 Pricing Structure

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

> *For full scope details (screens, APIs, gaps, testing strategy), refer to the **Scope of Work document**.*

### 1.2 Milestone Payment Plan

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

### 1.3 Invoicing Terms

**Classification: STANDARD**

*[Standard Metapointer section — standard invoicing terms, currency, tax treatment, and billing procedures to be populated from Metapointer standard template]*

### 1.4 Assumptions

- Pricing based on defined RFP scope (7 agents, 29 screens, 66 APIs, specified NFRs) with 10–15% scope variance allowance per RFP engagement model
- Scope variance within 10–15% is absorbed within the fixed price; variance exceeding 15% is managed through formal Change Request process
- External services (screening, bank validation, IAM) available and stable
- ERP integration APIs accessible and documented
- Required stakeholders available for timely review and approvals
- Multi-tenant architecture follows agreed design patterns
- Any deviation from these assumptions may impact cost and timeline

### 1.5 Change Billing Model

**Baseline Scope:** 7 intelligent agents (4 automated, 3 assisted), 29 screens + 11 modals, 66 APIs (58 vendor-built, 7 integrations, 1 orchestration), 25+ core features

**Change Management Process:**
1. **Change Request Submission:** HighRadius submits change request with business justification
2. **Impact Assessment:** Metapointer provides detailed analysis within 3 business days (technical feasibility, schedule impact, resource requirements, cost implications)
3. **Change Advisory Board (CAB) Review:** HighRadius approves, defers, or rejects change
4. **Change Order:** If approved, formal change order signed with cost and schedule adjustments
5. **Billing:** Cost adjustment deducted from final payment or invoiced separately per change order

---

## 2. Legal & Contractual Terms

**Classification: STANDARD**

*[Standard section — to be populated with Metapointer standard template]*

---

## 3. Support & Warranty Model

**Classification: STANDARD CORE + PROJECT TERMS**

*[Standard Metapointer support structure applies]*

### 3.1 Hypercare Terms

- **Hypercare Duration:** 6 months post-go-live (approximately July 2026 – January 2027)
- **Hypercare Staffing:** 0.5 FTE dedicated support resource rotating across the 6-person engineering team (~13 weeks of part-time effort)

### 3.2 Support SLAs

| Priority | Description | Response SLA | Resolution Target |
|----------|-------------|-------------|-------------------|
| P1 (Critical — system down) | Portal inaccessible, data corruption, cross-tenant data leak | < 4 hours | < 8 hours |
| P2 (High — major feature impaired) | Approval workflow broken, screening fails silently, PO sync error | < 8 hours | < 24 hours |
| P3 (Medium — workaround available) | Dashboard metrics incorrect, filter not working, UI alignment | < 24 hours | < 3 business days |
| P4 (Low — cosmetic/minor) | Tooltip missing, color mismatch, minor label typo | Next business day | Next sprint |

**Reporting:** Weekly updates via email/call and PVA (Product Velocity Analysis) on deliverables per RFP Section 5.

### 3.3 Escalation Matrix

| Tier | Scope | Timeframe | Auto-Escalation Rule | Personnel |
|------|-------|-----------|---------------------|-----------|
| Tier 1 — Technical | Bug fixes, configuration, environment issues | 24 hours | If unresolved after 24h → auto-escalate to Tier 2 with notification to both PMs | Engineering team lead |
| Tier 2 — Management | Cross-team blockers, resource conflicts, priority disputes | 48 hours | If unresolved after 48h → auto-escalate to Tier 3 with incident brief | Project Managers (both sides) |
| Tier 3 — Executive | Contractual issues, scope disputes, critical failures | Per agreement | Executive review with formal incident report | Delivery heads / stakeholders |

All escalations logged in Jira with timestamps and resolution notes.

### 3.4 Handover Repository

Per RFP Section 6, the following will be delivered:
- GIT repository with full source code
- Design documents (architecture, technical design, API specs)
- KT (Knowledge Transfer) sessions
- Deployment runbooks
- All resources used for the product

---

## 4. Change Management Process

**Classification: STANDARD**

*[Standard section — to be populated with Metapointer standard template]*

---

## 5. Risk Management

**Classification: STANDARD FRAMEWORK + PROJECT RISKS**

*[Standard Metapointer risk methodology applies]*

### 5.1 Project-Specific Risks

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

### 5.2 Disaster Recovery & Business Continuity

**DR Components:**

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

*Prepared By: Metapointer | For: HighRadius Corporation | Date: February 28, 2026*
