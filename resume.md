---
layout: page
title: Résumé
lang: en
alt_url: /ko/resume/
lede: Organised by where the work happened. Each entry covers what I built and what I weighed while building it.
description: Jungwon Sohn — backend and cloud infrastructure. Smart Dong School · SeSAC · side projects · KOSA.
---

## Overview

Four groups, by affiliation: services I owned during full-time employment, two team projects from training programs after leaving, and apps I built and ship solo.

| Where | Period | Projects | Role |
| --- | --- | --- | --- |
| **Smart Dong School** (employment) | 2023.09 – 2025.11 | 11 PHP sites · Naeildong School · Kizdong · Dokhakdong · Edudong · Blogdong · Dotetimer · infrastructure as code | Backend owner (full-stack) · deployment & ops |
| **SeSAC** (training) | 2026.06 – 2026.07 | YouthPick — youth policy recommendation platform (team of 5) | Team lead, full-stack |
| **Side** | 2026.02 – present | Maiary · Curora — two mobile apps | Solo — from concept to operations |
| **KOSA** (training) | 2026.05 – 2026.06 | Final project — Proxmox + AWS hybrid infrastructure (team of 5) | Infrastructure lead · architecture |

---

## Skills

| Area | |
| --- | --- |
| **Language** | Java 21, TypeScript / JavaScript, PHP, Dart |
| **Backend** | Spring Boot 3.5, NestJS, Koa, Express, Apollo Server 4, TypeGraphQL, GraphQL, REST |
| **Data** | MySQL, PostgreSQL, Redis, TypeORM, Prisma, JPA / Hibernate, DataLoader, Flyway, MinIO (S3) |
| **Auth** | OAuth 2.0 implemented from scratch (Google · Naver · Kakao · Apple), JWT, Spring Security, role & permission modelling |
| **Realtime** | Socket.IO 4, STOMP over WebSocket |
| **Test** | JUnit 5 + H2, Mockito, `@WebMvcTest` / `@DataJpaTest`, Jest, Vitest |
| **Cloud** | AWS (EC2, S3, VPC, NLB/ALB, Route 53, ACM, CloudFront, CodeDeploy, EKS/Fargate, Site-to-Site VPN, Client VPN) |
| **IaC** | Terraform, Ansible, Packer |
| **Container** | Kubernetes (kubeadm HA), Docker, Docker Compose, Helm, MetalLB, Ceph CSI |
| **Virtualisation** | Proxmox VE (HA cluster), Ceph RBD, MinIO |
| **Network / Security** | pfSense, VLAN segmentation, HAProxy + Keepalived VIP, WireGuard / IPsec VPN, nginx, IAM role design |
| **CI/CD** | GitHub Actions, ArgoCD (GitOps), AWS CodeDeploy, PM2, blue/green zero-downtime deployment |
| **Observability** | Prometheus, Grafana, Loki, Thanos, New Relic, Log4j2 → database sink |
| **Frontend** | React 19, Next.js, Flutter, TanStack Query, Zustand, Riverpod |
| **Practice** | Domain-driven package design, transaction boundary design, N+1 elimination, zero-downtime deployment, IaC, code review process |

---

## 1. Smart Dong School (employment)

**2023.09 – 2025.11 (2 years 3 months)** · Backend developer (full-stack) · deployment & operations · industrial technical personnel service — enrolled 2023.12, discharged 2025.11

I worked across several education services centred on a government-funded vocational training LMS, and handled their deployment and operations. Most were already live, so half the job was deciding where to cut first when a full rewrite wasn't an option.

### Naeildong School — backend owner, vocational training LMS

`Koa · Apollo Server 4 · TypeGraphQL · TypeORM · MySQL`

- **Instructor settlement system** — a batch that aggregates graded exams, graded assignments and answered Q&A over a period to compute monthly settlement amounts. The figures it produces are the basis for actual payroll.
- **Automated notification rule engine** — modelled 12 condition types (progress rate, exam eligibility, completion status, and so on) with single-table inheritance so operators can assemble learner notification campaigns without a code change. I also split the SMS-only send form into a channel-independent structure and added email.
- **Regulatory data pipeline to a public agency** — periodic transmission of enrolment, attendance and grades to the training monitoring authority. Changed rows are snapshotted into mirror tables in a separate schema first, then sent from the snapshot; results are reported to Slack so success can be confirmed daily.
- **Filter DSL compiler** — a shared module that recursively converts nested GraphQL filter input into ORM predicates, applied across most list queries.
- **Permission system** — authorisation decorators sit not only on resolvers but down at the entity-field level, so resolving them naively means hundreds of permission queries in a single request. I memoise the first lookup on the request context, pinning it to one query per request.
- Resident registration numbers are stored AES-encrypted; an ORM subscriber checks for decrypted plaintext being written back and blocks it, so a mistake in application code is caught at the persistence layer.

### Real-time progress tracking socket server — designed, built and operated solo

`Socket.IO 4 · TypeORM · PM2`

- **Problem** — lecture view tracking lived inside the monolith, so every deployment dropped the connections of learners mid-lecture and lost their progress. Progress is the data that government tuition reimbursement is based on.
- **Constraint** — Socket.IO v2 and v4 are not wire-compatible, so an in-place upgrade wasn't possible.
- **Solution** — I extracted tracking into a separate service with a graceful shutdown: on the termination signal it walks the entire session cache, persists progress for everyone currently watching, then exits. Paired with the process manager's zero-downtime restart, this eliminated progress loss during deployment.
- The shutdown handler is a discriminated union keyed on the reason for termination, so code that would touch an already-closed socket is caught at compile time.
- The session cache is keyed by account rather than socket id, which makes concurrent-session detection constant time.

### Dotetimer — Express to NestJS, without downtime

`NestJS 11 · GraphQL · TypeORM`

- Four years of production code had to move, but a live mobile app API depended on it, so it couldn't be swapped in one go. I spent a week in a separate repository verifying that the legacy app runs inside NestJS behind an adapter and pinning down the migration pattern, then applied it to the main repository in a single day.
- The legacy code grabbed the DataSource at module top level, so the standard ORM module would have split the transaction context in two. I removed that package and wrote a module that walks DataSource metadata at runtime to inject repositories dynamically. Once the migration was done, I removed the module and reverted to the standard approach.
- **Built the B2B HR module's admin screens from scratch** — electronic employment contracts (template → signature → approval), employee management, payroll ledger and payslip printing and mailing, and attendance records, all as a staged funnel UI.
- Also handled database index design, lock and timeout handling in the sync service, and moving the database logger onto winston.

### 11 legacy PHP sites — incremental modernisation

- The 11 sites weren't a shared instance; each was a fork, so the same fix had to be repeated 11 times. They were live revenue-generating sites, so a rewrite was off the table. I consolidated the areas where duplication cost the most, first.
- **Built a REST framework from scratch in PHP** — no Composer, no framework. Router, interceptor chain (session auth, rate limiting), DTOs, feature flags, and a multi-tenancy core that resolves the tenant and its database table prefix from the request host.
- **Introduced a micro-frontend** — screen-level React bundles keyed by build mode, with a branch on the legacy side that renders only the screens still on the allowlist. Migrating a screen means removing it from that list; putting it back rolls the change out in reverse.

### Kizdong · Dokhakdong · Edudong — maintenance

- Three services that branched off the same codebase as Naeildong School. I solved an N+1 in the shopping cart with a composite-key DataLoader — the key is a (user, product) pair, so simple batching doesn't group it — and applied it to two repositories covering three sites. I also added the admin cart view to both frontends.
- I handled issues common to all three in one pass (SMS/LMS auto-switching, payment gateway endpoint changes, video player replacement) and took sole ownership of three backend and payment repositories that had been left without a maintainer.

### Codifying live AWS infrastructure with Terraform (solo)

`Terraform · AWS · IAM · NLB · Client VPN` · 2025.06 – 2025.07

- **Background** — the infrastructure had been built by hand in the console. Nobody knew why anything was configured the way it was, and no change history existed. With a government training-authority audit approaching we needed redundancy and access control, and building that by hand leaves no way to unwind it afterwards.
- **I kept the resources that manage state out of state.** Creating the state bucket and lock table inside the same configuration produces a circular dependency, so they live in a separate configuration. The bucket is hardened with versioning, public-access blocking and non-current version expiry.
- **Live resources are referenced, never imported.** Importing them into management means every subsequent apply mistake becomes a production incident. I made it structurally impossible for Terraform to delete or modify existing infrastructure, and split what is created from what is only read across separate files. Machine images are selected by tag rather than pinned by id.
- **Steady-state and audit configurations are separated by directory and state key**, so an apply on one can't touch the other. When the audit ends, removing that configuration leaves the steady state intact.
- **Audit response** — pass-through redundancy on an NLB rather than an ALB, to leave TLS termination on the existing servers and avoid migrating certificates; a Client VPN with certificate authentication so administrative access comes off the public network. Security group rules reference source security groups rather than CIDRs, so adding instances doesn't mean editing rules.
- **Three IAM roles composed from per-service policies**, so adding a role means changing the combination rather than rewriting policy. Each policy is still a service-level wildcard, though — I did not get to resource-level least privilege, and recorded that limitation in the documentation.
- **I wrote down, in order, the steps Terraform couldn't cover** — the brief outage when re-associating an elastic IP, and the sequence for creating the NAT gateway in the console and fixing the route table.

### Deployment pipeline

`GitHub Actions · AWS CodeDeploy · PM2 · nginx`

- **Built CI/CD across five repositories.** Staging and production deployment applications are separated, and dependencies are packaged with the build artefact so deployment doesn't depend on the network at deploy time.
- **Implemented blue/green zero-downtime deployment without adding instances.** Deploy to the idle port, health check five times at ten-second intervals, switch the proxy only on success, roll back on failure. If the new version never comes up, the old one keeps serving.
- **Per-branch on-premise staging** — branch-prefixed processes on an internal server, so several features can be QA'd at once instead of queueing for a single staging environment.
- After moving to cluster mode, the scheduler ran once per instance and the same message went out multiple times. I fixed it to register the scheduler on a single instance and left the reasoning in the repository, so the next person raising the instance count doesn't hit the same trap.

---

## 2. SeSAC (training) — YouthPick

**2026.06 – 2026.07** · SeSAC first team project · team of 5 · team lead, full-stack
`Spring Boot 3.5 · Java 21 · MySQL · Redis · MinIO · React 19 · Docker Compose · GitHub Actions`

On the backend I owned authentication, admin, chat, files and profile; on the frontend, all admin screens plus the auth and session layer. As team lead I also set up the development process and deployment environment.

**Domain work**

- **Implemented OAuth 2.0 for three providers without a library.** The frontend is an SPA on a separate domain, so we needed direct control over callback handling and token issuance timing. I normalised three different provider responses into one schema and collapsed provider-side failures into a single error code, so no external service detail leaks to the client.
- **Introduced refresh-token rotation, then removed it.** Rotation only holds if there are no concurrent requests, and that premise breaks with two tabs open or under React StrictMode — the result was spurious 401s. I replaced it with hashed storage, HttpOnly cookie delivery and immediate revocation on suspension. The symptom showed up on the frontend, but the cause was a backend design decision.
- **Made error codes an interface rather than one big enum**, implemented per domain. Adding a domain doesn't touch existing files, and the frontend maps user-facing messages from the response body's code rather than the HTTP status.
- **Put tests where failure is silent.** If the onboarding profile enum and the external public-API code table drift apart, that axis of the recommendation silently scores zero — no exception, nothing to notice. I made a test enforce that the two stay in sync.
- **Built the admin back office API and its screens solo**, with a one-way dependency from admin into the domain layer. Authorisation rules live in one security configuration so a new endpoint can't quietly ship without them.
- **STOMP real-time chat** — the broker negotiated heartbeats as disabled when they weren't declared, dropping idle connections; fixed with a consistent setting across client, broker and proxy. Since browsers can't attach headers to the WebSocket handshake, authorisation moved into the STOMP interceptor.

**Team lead and deployment**

- **Docker Compose brings the whole stack up with one command.** The proxy forwards the API to the backend container, so the browser sees a same origin — which means **changing the deployment domain doesn't require touching CORS configuration.**
- **CI on both repositories via GitHub Actions.** The backend runs a format gate, then build plus in-memory database tests, so **it runs in CI with no external infrastructure.** Concurrency cancellation, least privilege (`contents: read`) and `persist-credentials: false` keep the token out of the workspace.
- **Wrote the pipeline that persists application logs to the database.** The built-in JDBC appender binds every column as a string, so an empty value from an unauthenticated request lands in an integer column and the whole insert fails. I wrote a custom appender that binds an explicit NULL when the value is absent and wrapped it in an asynchronous non-blocking buffer, so request threads never wait on a database write. The appender also swallows its own exceptions, so **a logging failure can't take down the application.**
- Defined the branch strategy and PR review rules, and added a request-context filter carrying trace id, path, IP and user id so warnings and above are queryable from the admin screen.

---

## 3. Side projects — Maiary · Curora

**2026.02 – present** · solo · shipped on the App Store · 32 cumulative release builds
`Flutter · Flame · NestJS · Prisma · PostgreSQL · Socket.IO · OpenAI`

Two mobile apps taken from concept to release and operation alone. Most of the work here is deciding what to keep and what to cut when one person has to carry it.

- **Purchases and subscriptions are verified server-side.** Trusting a client-supplied receipt means fraudulent purchases go through, so I verify directly against both vendors' servers and receive renewal, expiry and grace period through webhooks. The raw payload is retained so events can be reprocessed.
- **Every LLM call has a schema constraint and a deterministic fallback**, so a failed model call still leaves every field populated in the user's language. A cache table's expiry timestamp doubles as a rate limiter, capping call volume without a separate quota system, and error responses are cached too so failed requests don't silently retry and bill.
- **Curora moved from a server-crawling design to a local-first one.** For a one-person operation, a scheduled collector is the most expensive part to run, so the app parses feeds and stores them on device while the server handles only auth, AI and payments. Infrastructure dropped to a single API server and offline reading came along with it; cross-device sync was the explicit trade-off.
- Wrote parsers for RSS 2.0, Atom and RDF by hand — BOM handling, RFC-822 date parsing and pagination included — rather than take a dependency.
- **Built four iOS home screen widgets natively in WidgetKit / Swift** with App Group data sharing. Widgets are a subscriber-only feature.
- Attached a Redis adapter to Socket.IO multiplayer from the start, while the user count was still small, so scaling out later doesn't mean revisiting the architecture. The reason is a constraint I hit at work: an in-memory cache that pinned a service to a single instance.
- Supports four languages (Korean, English, Japanese, Hindi). The admin console is generated from the schema rather than built separately.

---

## 4. KOSA (training) — final project

**2026.05 – 2026.06** · KOSA cloud infrastructure engineering · team GARDEN, 5 people · infrastructure lead
`Proxmox VE · Kubernetes · Terraform · Ansible · Packer · AWS`

A hybrid environment: 25 VMs and a Kubernetes HA cluster (7 nodes, 106 pods) on a four-node Proxmox cluster, connected to AWS over VPN.

### Network and high availability

- **Four-tier VLAN segmentation** (public / DMZ and load balancing / internal services / management) plus physical 1G and 10G separation — management and external access on one, storage replication on the other.
- **Five Keepalived VIPs** (DNS, Vault, HAProxy, Kubernetes API, monitoring), with VMs of the same role distributed across different physical hosts.
- **VIP chaining** — HAProxy VIP in front of the Kubernetes API VIP, so changing the master node set doesn't mean editing load balancer configuration.

### Design decisions

- **Breaking circular dependencies** — CI/CD, Vault and object storage sit on VMs outside Kubernetes. If the storage holding Terraform state lives inside the cluster, losing the cluster also loses the means to rebuild it.
- **Where the management interface sits** — putting the hypervisor management IP behind the firewall means losing console access when the firewall fails. It sits under the physical router instead. I judged firewall redundancy unnecessary at this scale and recorded that decision, and its cost, in the documentation.
- **Storage tiering by workload** — Kubernetes masters use local volumes because etcd is sensitive to fsync latency; everything else uses distributed storage, with replication traffic isolated on a dedicated 10G network.
- **Defined the air-gap transition order** — mirror packages while the internet path is still open, then remove the firewall rules. I did not get to verify this end to end and flagged that as a limitation.

### Kubernetes platform

- Helm-based build-out of MetalLB (bare-metal L2 load balancing with an address pool), Ceph CSI, Harbor, ArgoCD, Gitea and a Percona XtraDB Cluster.
- The database cluster uses required — not preferred — anti-affinity, so three replicas can never land on the same node. Preferred scheduling lets the scheduler pack them together when resources are tight, which quietly defeats the point of running three.
- Worked around operator CRD race conditions and immutable selector conflicts at the script level during rollout.

### AWS hybrid

- Nine Terraform modules — VPC, EC2, NLB, Route 53, key pair, EKS, two VPN paths and CloudFront. The decision to modularise came after paying the cost of two configurations duplicating the same blocks in the work repository.
- **IPsec site-to-site VPN** terminated on pfSense, with encryption suites pinned on both tunnels, plus a WireGuard path in parallel.
- **Cloud bursting** — a cron polls Prometheus and, past a CPU threshold, toggles an HAProxy ACL to shift backends from on-premise to cloud.
- **Cost modelling** — I calculated the per-pod Fargate rate directly and priced an active-active 70/30 split at roughly $180 per month, comparing it against bursting at about $120 in steady state and $150–200 while bursting.

### Documentation

Wrote the design documentation myself, recording the reasoning behind each choice alongside the alternatives I rejected — deep-dives on the database cluster, block storage, hypervisor HA and DMZ separation, plus build guides for each of the other four members' areas.

---

## Education

| Period | |
| --- | --- |
| 2017.03 – 2026.08 | **Sejong University** — Computer Engineering (expected graduation) |

---

## Training

| Period | Program |
| --- | --- |
| 2026.06 – present | **SeSAC** — team lead, first project (YouthPick) |
| 2026.05 – 2026.06 | **KOSA Cloud Infrastructure Engineering** — infrastructure lead, final project |

---

## Certifications

| Certification | Issuer | Date |
| --- | --- | --- |
| **AWS Certified Solutions Architect – Associate** | Amazon Web Services | 2025.12.30 |
| **HashiCorp Certified: Terraform Associate (004)** | HashiCorp | 2026.03.21 |
| **Engineer Information Processing** | HRD Korea | 2025.06.13 |
| **SQL Developer (SQLD)** | Korea Data Agency | 2025.04.04 |
| **TOEIC Speaking IH (150)** | YBM | 2026.06.14 |

---

## Awards

| Award | Date |
| --- | --- |
| 3rd place, university SW coding competition | 2020.12.11 |

---

## Military service

| | |
| --- | --- |
| Status | **Completed** — industrial technical personnel, discharged on schedule |
| Placement | Smart Dong School (designated company) — same as the employment above |
