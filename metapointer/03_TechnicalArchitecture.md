Technical Architecture

AP Supplier Portal

Prepared for:  HighRadius Corporation

Prepared by:  Metapointer Labs Pvt. Ltd.

Date:  March 2026

Version:  3.3

Table of Contents

1.  Architecture Overview	3

1.1  Five-Layer Architecture Stack	3

1.2  System Architecture Diagram	3

2.  System Design	5

2.1  Application Architecture	5

2.2  End-to-End Process Flow	5

2.3  Microservice Domain Boundaries	7

3.  Technology Stack	8

4.  Integrations	10

5.  Data Design	11

5.1  Multi-Tenancy Model	11

5.2  Core Data Entities	11

5.3  Database Strategy	11

6.  Security Design	13

6.1  Authentication & Authorisation	13

6.2  Five-Layer Enforcement Chain	13

6.3  Encryption & Secrets Management	13

6.4  Screen-Level Permission Matrix (Key Screens)	14

7.  DevOps & Environments	15

7.1  Environment Promotion Pipeline	15

7.2  CI/CD Pipeline	15

7.3  Rollback Strategy	15

7.4  Monitoring & Observability	16

8.  Performance & Scalability	17

8.1  Performance Benchmarks	17

8.2  Scalability Design	17

9.  Technical Risks	18


# 1.  Architecture Overview


The AP Supplier Portal follows a modular, layered architecture designed to meet HighRadius’s non-functional requirements: sub-3-second API responses, 100% multi-tenant data isolation, containerised G4 deployment, and Keycloak-based authentication. Clear separation between presentation, API gateway, service, integration, and data layers ensures independent maintainability and scalability of each tier.


## 1.1  Five-Layer Architecture Stack



| Layer | Technology | Components | Responsibility |
| --- | --- | --- | --- |
| Presentation | React 18.x + G4 DSL | 3 persona-specific SPAs sharing a common component library | Responsive UI, WCAG 2.0 AA, virtual scrolling (1,000+ rows), role-based route guards |
| API Gateway | Spring Cloud Gateway | JWT Validator, Rate Limiter, Tenant Injector, RBAC Middleware | Every request passes 4 sequential gates — no request reaches business logic without valid JWT + tenant context + role |
| Service | Spring Boot 3.x | 12 microservices across 4 domains (Onboarding, Compliance, PO, Invoice) | Stateless, horizontally scalable, independently deployable; 66 APIs total |
| Integration | Adapter Pattern | Circuit breaker, retry, dead-letter queues for all 7 external integrations | Fault-tolerant integration with HighRadius-owned and ERP services |
| Data | PostgreSQL + Redis | Schema-per-tenant DB; Redis cache; immutable audit log store | Multi-tenant isolation, caching of config/templates, 2-year audit log retention |



## 1.2  System Architecture Diagram


The following diagram illustrates the five-layer system architecture and component relationships:

Figure 4: AP Supplier Portal — System Architecture (5-Layer Stack)

Architecture Design Principles
Stateless services for horizontal scaling — each microservice can scale independently. Zero-trust security: every request is authenticated, authorised, and tenant-scoped before any business logic executes. Fault tolerance at every integration boundary: circuit breakers prevent cascading failures from HighRadius-owned service outages.


# 2.  System Design



## 2.1  Application Architecture


The application follows a microservices architecture with domain-driven boundaries. Each agent is implemented as an independently deployable service:

•  Presentation Layer: React 18.x SPA with G4 DSL component library. Three persona-specific application shells sharing a common component library. Role-based routing enforced at the frontend layer. WCAG 2.0 AA compliance with ARIA tags and keyboard navigation. Virtual scrolling for grids with 1,000+ rows.

•  API Gateway: Central entry point for all frontend requests. Performs JWT validation, tenant context injection (tenant_id from Keycloak claims), RBAC middleware check, and rate limiting before routing to backend services.

•  Service Layer: Spring Boot 3.x microservices, one per agent domain plus cross-cutting services (audit, notifications, admin). Stateless design with horizontal scaling. Workflow-driven business logic for onboarding, approvals, and invoice processing.

•  Integration Layer: Adapter pattern with circuit breaker, exponential retry, and dead-letter queues for all external system calls. No blocking calls to external services in the critical path.


## 2.2  End-to-End Process Flow


The complete supplier lifecycle from invitation through invoice processing and ERP synchronisation is illustrated below:

Figure 5: AP Supplier Portal — End-to-End Process Flow (Phase 1 + Phase 2)


## 2.3  Microservice Domain Boundaries



| Domain | Services | APIs | Phase |
| --- | --- | --- | --- |
| Onboarding Domain | Invitation Service, Registration Service, Draft Management | 12 | Phase 1 |
| Compliance Domain | Screening Orchestrator, Bank Validation Adapter | 10 | Phase 1 |
| Approval Domain | Approval Workflow Engine, Master Data Change Service | 14 | Phase 1 + 2 |
| PO Domain | PO Import Service, ERP Adapter (SAP/Oracle/NetSuite) | 10 | Phase 2 |
| Invoice Domain | Invoice Creation Service, PO-Flip Engine, AP Sync Service | 11 | Phase 2 |
| Cross-cutting | Audit Service, Notification Service, Admin Config Service | 9 | Phase 1 |
| Total | — | 66 | — |



# 3.  Technology Stack


The technology stack is fully aligned with HighRadius engineering standards as specified in RFP Section 5. All technology choices are G4-native or G4-compatible:


| Layer | Technology | Version | Details |
| --- | --- | --- | --- |
| Frontend UI | React + HighRadius G4 DSL | 18.x | Design System component library; WCAG 2.0 AA; virtual scrolling |
| API Gateway | Spring Cloud Gateway | 3.x | JWT validation, tenant injection, rate limiting, RBAC middleware |
| Backend Services | Spring Boot (Java) | 3.x / Java 17+ | Stateless microservices; horizontal scaling; workflow-driven logic |
| Database | PostgreSQL (OLAP) | Latest stable | Schema-per-tenant; row-level security; read replicas for analytics |
| Caching | Redis | Latest stable | Session management; form template cache; i18n label cache; job queues |
| Authentication | Keycloak IAM | HighRadius env | OIDC/JWT SSO; RBAC/ABAC; multi-tenant token claims (tenant_id) |
| Secrets Mgmt | HashiCorp Vault | HighRadius env | Dynamic secrets; credential rotation; API key management |
| Encryption | TLS 1.3 / AES-256 | — | TLS 1.3 in transit; AES-256 for data at rest |
| Containerisation | Docker + Kubernetes + Helm | Latest stable | Containerised deployment in HighRadius G4 environment |
| CI/CD | Per HighRadius practices | — | RFP Section 5 mandate; environment promotion: Dev → QA → UAT → Prod |
| Async Processing | Redis-backed Job Queue | — | Bulk imports, screening orchestration, long-running ERP sync |
| DB Migrations | Flyway | — | Tenant-aware schema versioning; rollback migration scripts |
| Observability | Prometheus / Grafana / ELK | — | Infrastructure metrics; structured logging; application performance |
| AI Tooling | Claude Opus AI | — | All 6 engineers; 1.10x–1.50x productivity on code, tests, docs |



# 4.  Integrations


The portal integrates with 7 external systems. All integrations use fault-tolerance patterns: circuit breaker, exponential retry, and dead-letter queues. Vendor responsibility is limited to integration layer only for HighRadius-owned services:


| External System | Integration Method | Ownership | Fault Tolerance |
| --- | --- | --- | --- |
| Keycloak IAM | OIDC/SSO; JWT validation; RBAC | HighRadius-owned; vendor integrates | Token refresh; re-authentication on expiry |
| Screening Services (Addr/TIN/OFAC) | REST API; 4 parallel checks | HighRadius-owned; vendor builds orchestration layer | Retry on timeout; stub for dev; partial result display |
| Bank Validation Service | REST API; synchronous | HighRadius-owned; vendor builds adapter | Circuit breaker; mock for dev; re-trigger API |
| ERP Systems (SAP/Oracle/NetSuite) | REST API; PO import and invoice sync | Vendor builds adapter and orchestration | Bi-directional sync conflict detection; dead-letter queue; retry queue |
| Document Storage (S3-compatible) | S3 API; virus scanning on upload | Vendor builds integration; HR provides infra | Upload retry; virus scan failure handling; quarantine flow |
| HashiCorp Vault | Secrets management API | HighRadius-provided; vendor integrates | Credential rotation; fallback to environment variables in dev |
| Notification Service | Email via SMTP + WebSocket for real-time | Vendor builds | Async delivery; retry on failure; notification centre fallback |


Integration Resilience Pattern
All 7 integrations implement the same resilience pattern: Circuit Breaker (prevents cascading failures from HR service outages) → Exponential Retry (handles transient failures with backoff) → Dead-Letter Queue (captures unprocessable messages for manual review). No integration failure can bring down the portal.


# 5.  Data Design



## 5.1  Multi-Tenancy Model


The portal implements a schema-per-tenant multi-tenancy model, providing the strongest possible data isolation for a SaaS environment while sharing infrastructure cost:

•  Schema-per-Tenant: Each HighRadius customer (tenant) gets a dedicated PostgreSQL schema. No data from one tenant can physically exist in another tenant's schema.

•  Row-Level Security: PostgreSQL RLS policies act as a database-level safety net. Even if application middleware is bypassed, RLS prevents any cross-tenant data access.

•  Tenant Resolution: Tenant ID is extracted from the Keycloak JWT (tenant_id claim) at the API Gateway layer. It is injected into the request context before any business logic executes.

•  Query Enforcement: Every database query is automatically scoped with a tenant_id WHERE clause at the middleware layer. No query reaches the database without tenant scope.

•  Common Schema: A shared common schema stores non-tenant-specific configuration: form templates, workflow definitions, and i18n labels. These are read-only for tenant services.


## 5.2  Core Data Entities



| Entity | Schema | Key Attributes | Retention |
| --- | --- | --- | --- |
| Supplier | Tenant | supplier_id, tenant_id, status, created_at, activated_at, master_data fields | Indefinite (active records) |
| Invitation | Tenant | invitation_id, email, status, expiry, sent_at, completed_at | 2 years |
| Screening Result | Tenant | screening_id, supplier_id, check_type, status, result_payload, screened_at | 7 years (compliance) |
| Approval Workflow | Tenant | workflow_id, entity_id, step, approver, decision, decided_at, escalation_count | 7 years (compliance) |
| Purchase Order | Tenant | po_id, erp_id, supplier_id, status, line_items, acknowledged_at | 7 years (audit) |
| Invoice | Tenant | invoice_id, po_id, supplier_id, status, line_items, submitted_at, approved_at | 7 years (audit) |
| Document | Tenant | document_id, entity_id, type, s3_key, virus_scan_status, uploaded_at | 7 years (compliance) |
| Audit Log | Tenant | log_id, actor_id, action, entity_type, entity_id, timestamp, ip_address, outcome | 2 years minimum (RFP mandate) |



## 5.3  Database Strategy


•  PostgreSQL OLAP with read replicas for analytics and dashboard queries

•  Redis caching layer for form templates, workflow definitions, and i18n labels — reduces DB read load for frequently-accessed configuration

•  Flyway for schema versioning with tenant-aware migration strategy — each migration runs per tenant schema

•  Immutable audit log — append-only table with no UPDATE or DELETE operations permitted; filterable and exportable

•  Async job queue (Redis-backed) for bulk imports, screening orchestration, and long-running ERP sync operations


# 6.  Security Design



## 6.1  Authentication & Authorisation


The portal implements a zero-trust security model. No request reaches business logic without passing all authentication, authorisation, and tenant-scoping checks:

•  Authentication: Keycloak SSO with OIDC/JWT. No request bypasses authentication. Tokens validated at API Gateway on every request.

•  RBAC: Roles assigned in Keycloak: Supplier, Supplier Manager, Approver, Admin. Role claims included in JWT and validated at API Gateway.

•  ABAC: Runtime attribute-based checks at Service Layer for fine-grained control: record ownership, spend threshold, tenant scope, workflow status.

•  Multi-Tenant: Tenant_id extracted from JWT and injected into all downstream service calls. No tenant can access another tenant's data at any layer.


## 6.2  Five-Layer Enforcement Chain



| Layer | Enforcement Point | What It Checks | Failure Action |
| --- | --- | --- | --- |
| 1. Frontend | Route guards + component visibility | Role → show/hide routes, buttons, tabs, modals | Hidden UI elements; redirect to dashboard |
| 2. API Gateway | JWT validation + RBAC middleware | Token validity, role claim, tenant_id in claims | 401 Unauthorised / 403 Forbidden |
| 3. Service Layer | ABAC checks | Ownership, tenant match, status, spend threshold, role actions | 403 Forbidden with reason code |
| 4. Database | tenant_id WHERE clause + RLS policies | Every query scoped to tenant; RLS enforced at DB level | Query returns empty set — no cross-tenant leakage |
| 5. Audit | All access decisions logged | Every allow/deny decision recorded with actor, action, entity | Immutable audit trail for compliance review |



## 6.3  Encryption & Secrets Management


•  In Transit: TLS 1.3 enforced on all API endpoints. No HTTP — all traffic is HTTPS. CSP headers enforced.

•  At Rest: AES-256 encryption for sensitive data fields. Document storage encrypted at rest via S3-compatible storage.

•  Secrets: HashiCorp Vault for all credentials, API keys, and certificates. Dynamic secrets with automatic rotation. No hardcoded credentials anywhere in the codebase.

•  OWASP: SAST + DAST scanning of all vendor-built endpoints. OWASP Top 10 compliance validated before every production release.


## 6.4  Screen-Level Permission Matrix (Key Screens)



| Screen / Area | Supplier | Supplier Manager | Approver | Admin |
| --- | --- | --- | --- | --- |
| Supplier Dashboard | Full (Own) | None | None | None |
| Manager Dashboard | None | Full | View | View |
| Supplier Registration Form | Full (Own) | None | None | None |
| Supplier List / Worklist | Own | Full | View | View |
| Screening Dashboard | None | Full | View | View |
| Approval Worklist | None | View | Full | View |
| PO List & PO Detail | Full (Own) | View | None | None |
| Invoice List & Creation | Full (Own) | None | None | None |
| Form Builder | None | None | None | Config |
| Workflow Configuration | None | None | None | Config |
| User / Role Management | None | None | None | Full |
| Audit Trail | None | View | None | Full |
| Notification Centre | Full (Own) | Full (Own) | Full (Own) | Full |



# 7.  DevOps & Environments



## 7.1  Environment Promotion Pipeline


All deployments follow a linear environment promotion pipeline with manual gates at UAT and Production stages:


| Environment | Trigger | Purpose | Sign-off Required |
| --- | --- | --- | --- |
| Development (Local) | Developer machine | Feature development and unit testing | None |
| QA | Auto on merge to QA branch | Integration testing, E2E automation, API validation | QA Engineer |
| UAT | Manual — QA sign-off | Client acceptance testing with HighRadius stakeholders | HighRadius Product + QA |
| Production | Manual — UAT sign-off | Live customer deployment via HighRadius G4 containerised environment | HighRadius Engineering + Infosec |



## 7.2  CI/CD Pipeline


•  Pipeline follows HighRadius engineering practices as mandated in RFP Section 5

•  Deployment uses Docker containers with Helm charts for Kubernetes orchestration in the G4 environment

•  Every merge to QA triggers: unit test run, SAST scan, container build, deployment, smoke test

•  No merge permitted with critical/high SAST findings or failing unit tests

•  Pre-deployment checklist: all automated tests passing, code review completed, security scan clean, documentation updated, stakeholder approval obtained, rollback plan documented


## 7.3  Rollback Strategy



| Failure Type | Rollback Strategy | Estimated Recovery Time |
| --- | --- | --- |
| Application bug (post-deploy) | Revert to previous container image via Helm rollback | < 5 minutes |
| Database migration failure | Execute pre-written rollback migration script (Flyway) | < 15 minutes |
| Integration failure (HR service) | Circuit breaker activates; fallback to cached/queued state | Automatic |
| Configuration error | Revert ConfigMap/Secret via version control | < 5 minutes |
| Full deployment failure | Automated rollback to last known good state | < 10 minutes |



## 7.4  Monitoring & Observability



| Observability Layer | Tools / Approach | What It Monitors |
| --- | --- | --- |
| Application Performance | APM integration (G4 compatible) | API response times, error rates, throughput, slow queries |
| Structured Logging | Centralised log aggregation (ELK/Fluentd) | Application logs, audit events, integration call traces |
| Infrastructure Metrics | Kubernetes-native (Prometheus/Grafana) | CPU, memory, pod health, replica counts, network I/O |
| Business KPIs | Custom dashboards | Onboarding cycle time, screening pass rates, invoice SLA, approval queue depth |
| Real-Time Alerting | PagerDuty/OpsGenie integration | Technical incidents (P1/P2 auto-page), business anomalies |
| Health Checks | Kubernetes liveness + readiness probes | Every 5 minutes; auto-restart on failure; traffic routing on readiness |



# 8.  Performance & Scalability



## 8.1  Performance Benchmarks


The following performance targets are contractually committed and validated through automated performance testing before every production release:


| Metric | Target | Validation Method |
| --- | --- | --- |
| API Response Time (P95) | < 3 seconds | Artillery load test — 100–500 concurrent users |
| API Response Time (P99) | < 3 seconds | Artillery stress test — beyond expected capacity |
| Grid Load (1,000+ rows) | < 500 ms | Virtual scrolling stress test with synthetic data |
| Page Load Time | < 2 seconds | Lighthouse performance audit per sprint |
| Screening Execution (4 checks) | Real-time < 30s | E2E test: screening triggered → all 4 checks complete |
| File Upload/Download | < 5 seconds | Upload stress test with max file sizes |
| Concurrent Users | 1,000 | 8-hour soak test; sustained load with no memory leaks |
| Transactions per Hour | 10,000 | Month-end simulation test; peak invoice/PO volume |



## 8.2  Scalability Design


•  Frontend, backend, and integration layers scale independently via Kubernetes HPA (Horizontal Pod Autoscaler)

•  Stateless microservices — any instance can handle any request; no session affinity required

•  Schema-per-tenant database architecture allows new tenants to be onboarded without impacting existing tenants

•  Multi-tenant automation absorbs acquisitions without proportional headcount increases

•  Redis caching reduces database load for high-read configuration data (form templates, workflow definitions)

•  Asynchronous processing via Redis job queue for bulk imports and long-running ERP sync operations

•  Read replicas for PostgreSQL reduce primary database load for dashboard and analytics queries


# 9.  Technical Risks


The following technical risks have been identified and mitigated through architecture decisions and delivery planning:


| Risk | Probability | Impact | Architecture Mitigation |
| --- | --- | --- | --- |
| G4 DSL component gaps requiring custom builds | Medium | Medium | Sprint 0 G4 OOB component evaluation; custom components built only for identified gaps; component-per-screen mapping in sprint planning |
| ERP sync conflict resolution complexity | Medium | High | Bi-directional sync with conflict detection; dead-letter queue for unresolvable conflicts; synthetic test data in dev; real ERP validation in UAT |
| Multi-tenant isolation defect in production | Low | Critical | Schema-per-tenant + RLS as defence-in-depth; automated cross-tenant isolation tests every sprint; 5-layer enforcement chain; independent security pen test |
| HighRadius service API breaking changes | Low | High | Adapter pattern isolates integration logic; version-pinned API contracts; circuit breakers prevent cascading failures |
| Performance degradation at scale | Low | High | Redis caching for all high-read data; virtual scrolling for large grids; 8-hour soak test and month-end simulation before every go-live |
| HashiCorp Vault integration delay | Medium | Medium | Environment variables in dev; Vault integration completed pre-UAT; no secrets ever hardcoded in codebase or CI/CD config |
