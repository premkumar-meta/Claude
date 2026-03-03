# AP SUPPLIER PORTAL — TECHNICAL SPECIFICATIONS

| Field | Detail |
|-------|--------|
| **Document** | Technical Specifications |
| **Version** | 3.3 |
| **Date** | February 28, 2026 |
| **Client** | HighRadius Corporation |
| **Project** | AP Supplier Portal Development & Deployment |
| **Service Provider** | Metapointer |
| **Status** | READY FOR SUBMISSION |

> **Confidentiality Notice:** This document contains proprietary and confidential information. Distribution is restricted to authorized HighRadius and Metapointer personnel only.

> **Cross-References:**
> - Executive Summary & Business Understanding → *Proposal PDF document*
> - Scope of Work, Screens & Deliverables → *Scope of Work document*
> - Timeline, Milestones & Delivery Approach → *Timeline document*
> - Commercial Terms & Pricing → *Commercial Agreement document*

---

## Table of Contents

1. [Solution Architecture](#1-solution-architecture)
   - 1.1 [Architecture Overview](#11-architecture-overview)
   - 1.2 [Technology Stack](#12-technology-stack)
   - 1.3 [Application Architecture](#13-application-architecture)
   - 1.4 [Data Architecture](#14-data-architecture)
   - 1.5 [Integration Architecture](#15-integration-architecture)
   - 1.6 [Security Architecture](#16-security-architecture)
   - 1.7 [Deployment Architecture](#17-deployment-architecture)
2. [Security & Compliance Controls](#2-security--compliance-controls)
   - 2.1 [Project-Specific Security Adaptations](#21-project-specific-security-adaptations)
   - 2.2 [Infosec Clearance Process](#22-infosec-clearance-process)
3. [Data Migration Strategy](#3-data-migration-strategy)
4. [Quality Assurance Framework](#4-quality-assurance-framework)

---

## 1. Solution Architecture

**Classification: PROJECT-SPECIFIC**

### 1.1 Architecture Overview

The architecture follows a modular, layered approach designed to meet HighRadius NFRs: sub-3-second API responses, 100% multi-tenant data isolation, containerized G4 deployment, and Keycloak-based authentication. Clear separation between presentation, API gateway, service, integration, and data layers ensures maintainability and independent scalability.

> *For detailed architecture diagrams (E2E process flow, system architecture, onboarding sequence, PO-to-invoice sequence, agent trigger map, security IAM flow, multi-tenant isolation, error handling), refer to `Supplier_Portal_Architecture_Diagrams.md` and the `mermaid/` directory.*

### 1.2 Technology Stack

| Layer | Technology | Details |
|-------|-----------|---------|
| **Presentation** | React 18.x + G4 DSL | HighRadius Design System, WCAG 2.0 AA, virtual scrolling |
| **API Gateway** | G4 Platform Gateway | JWT validation, tenant context injection, rate limiting |
| **Service** | Spring Boot 3.x (Java 17+) | Stateless microservices, horizontal scaling |
| **Database** | PostgreSQL (OLAP) | Schema-per-tenant, row-level security |
| **Caching** | Redis | Session management, configuration lookups |
| **Security** | Keycloak IAM | OIDC/JWT, SSO, RBAC/ABAC |
| **Secrets** | HashiCorp Vault | Dynamic secrets, credential rotation |
| **Encryption** | TLS 1.3 / AES-256 | In-transit and at-rest |
| **Deployment** | Docker, Kubernetes, Helm | G4 containerized environment |
| **CI/CD** | Per HighRadius practices | RFP Section 5 mandate |
| **Integration** | Adapter pattern | Circuit breaker, retry, dead-letter queues |
| **Compliance** | OWASP Top 10, SOX/GDPR | Immutable audit trails, 2-year retention |

### 1.3 Application Architecture

- **Presentation Layer:** React 18.x + G4 DSL, responsive SPA with role-based routing, WCAG 2.0 AA compliance, ARIA tags, virtual scrolling
- **API Gateway:** Request routing, JWT validation, tenant context injection, rate limiting
- **Service Layer:** Spring Boot 3.x microservices with stateless design supporting horizontal scaling; workflow-driven business logic for onboarding, approvals, and invoice processing
- **Integration Layer:** Adapter pattern with circuit breaker, retry, and dead-letter queues for all external system communication

### 1.4 Data Architecture

- **Multi-Tenancy Model:** Schema-per-tenant with shared infrastructure; each HighRadius customer gets an isolated PostgreSQL schema with row-level security policies
- **Common Schema:** Shared configuration (form templates, workflow definitions, i18n labels)
- **Tenant Resolution:** JWT claim (tenant_id extracted from Keycloak token) applied at middleware layer before any DB query
- **Core Entities:** Supplier, Invitation, Screening Result, Approval Workflow, Purchase Order, Invoice, Document, Audit Log
- **Strategy:** PostgreSQL OLAP with read replicas, Redis caching layer, immutable audit logs with 2-year retention

### 1.5 Integration Architecture

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

### 1.6 Security Architecture

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

> *For full screen list with complexity ratings and effort estimates, refer to the **Scope of Work document**.*

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

### 1.7 Deployment Architecture

- **Containerization:** Docker containers with Helm charts for Kubernetes orchestration
- **Environment Promotion:** Dev (local) → QA (auto on merge) → UAT (manual, QA sign-off) → Production (manual, UAT + HighRadius Engineering sign-off)
- **High Availability:** Redundant components, health checks, auto-scaling policies
- **G4 Platform:** Deployed within HighRadius G4 environment per RFP requirements

> *For deployment schedule and environment promotion timeline, refer to the **Timeline document**.*

---

## 2. Security & Compliance Controls

**Classification: STANDARD CORE + PROJECT ADAPTATION**

*[Standard Metapointer security controls apply]*

### 2.1 Project-Specific Security Adaptations

- **Access Control:** Keycloak integration with hybrid RBAC/ABAC model; 4 personas (Supplier, Supplier Manager, Approver, Admin) with screen-level and button-level permissions across 29 screens + 11 modals
- **Encryption:** TLS 1.3 in transit, AES-256 at rest; HashiCorp Vault for all secrets management per HighRadius security requirements
- **Audit Logging:** Immutable audit trail for all portal actions — onboarding, screening, approvals, invoice submissions; filterable by user, action type, date; exportable for compliance; 2-year retention
- **Multi-Tenant Isolation:** Schema-per-tenant with row-level security; tenant_id enforced at middleware layer before any database query; JWT-based tenant resolution
- **Regulatory Alignment:** SOX/GDPR support; OFAC sanctions screening compliance; 100% supplier screening coverage; OWASP Top 10 compliance
- **Adherence to HighRadius cybersecurity policies** during development per RFP Section 5

### 2.2 Infosec Clearance Process

| Phase | Activity | Timeline | Owner |
|-------|----------|----------|-------|
| Pre-Development | Security architecture review with HighRadius infosec team | Sprint 0 | Vendor + HR Infosec |
| During Development | Continuous SAST scanning in CI/CD pipeline; no critical/high findings allowed to merge | Every sprint | Vendor |
| Pre-UAT | Comprehensive security assessment: OWASP Top 10, RBAC/ABAC validation, tenant isolation testing | Sprint 5 (Phase 1), Sprint 9 (Phase 2) | Vendor |
| Pre-Production | Formal infosec review submission to HighRadius cybersecurity team; remediation of findings | 2 weeks before each go-live | Vendor + HR Infosec |
| Sign-Off | HighRadius infosec clearance certificate as production deployment gate | Required before each go-live | HR Infosec |

**Remediation SLA:** Critical findings resolved within 48 hours; High findings within 1 sprint; Medium/Low tracked and resolved before final handover.

---

## 3. Data Migration Strategy

**Classification: CONDITIONAL — PROJECT-SPECIFIC**

**Not Applicable.** Data migration of existing supplier data from ERPs, spreadsheets, or legacy systems is explicitly out of scope for this engagement. The Supplier Portal will start with fresh data, with suppliers onboarded through the new portal workflows.

---

## 4. Quality Assurance Framework

**Classification: STANDARD**

*[Standard section — to be populated with Metapointer standard template]*

> *For project-specific testing strategy (unit, E2E, performance, security, RBAC testing), refer to the **Scope of Work document** Section 1.1 — Testing & Quality Assurance.*

---

*Prepared By: Metapointer | For: HighRadius Corporation | Date: February 28, 2026*
