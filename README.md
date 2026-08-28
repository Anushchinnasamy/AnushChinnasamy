<div align="center">

<a href="https://portfolio-eta-one-1hhe8hokhj.vercel.app/">
  <img src="./banner.svg" alt="Anush Chinnasamy — Java Backend Developer / GenAI Engineer" width="100%" />
</a>

<br><br>

[![Portfolio](https://img.shields.io/badge/Portfolio-9FFF6E?style=flat-square&logo=vercel&logoColor=black)](https://portfolio-eta-one-1hhe8hokhj.vercel.app/)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-000000?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/anushchinnasamy)
[![LeetCode](https://img.shields.io/badge/LeetCode-000000?style=flat-square&logo=leetcode&logoColor=white)](https://leetcode.com/u/anushchinnasamy/)
[![Email](https://img.shields.io/badge/Email-000000?style=flat-square&logo=gmail&logoColor=white)](mailto:anushchinnasamy@gmail.com)

</div>

<br>

## About

I build distributed backend systems in Java and Spring Boot — services that talk to each other over Kafka, own their own databases, and stay correct under concurrent load — and ship GenAI features (RAG, LLM tool-calling) on top of them.

<br>

## Tech Stack

<table>
<tr>
<td valign="top" width="50%">

**Core Backend**
```
Java 17 · Spring Boot · FastAPI
REST APIs · SQL · Microservices
```

**Databases**
```
PostgreSQL · Neon · Cassandra
Redis · pgvector
```

**Messaging / Real-time**
```
Kafka · WebSocket · WebRTC
Redis Pub/Sub
```

</td>
<td valign="top" width="50%">

**Resilience**
```
Redisson · SAGA · Idempotency Keys
Resilience4j · Caching
```

**GenAI**
```
RAG · Vector Embeddings
LLM Integration · Prompt Engineering
AI Agents / Function Calling
```

**Cloud / DevOps**
```
Azure (AZ-900, AZ-204) · Docker
GitHub Actions · Harness CI/CD
Render · Vercel
```

</td>
</tr>
</table>

<br>

## Selected Projects

<table>
<tr>
<td width="50%" valign="top">

### 01 · Ticket Booking System — `Backend`
Distributed ticketing platform: Redis + Redisson distributed locking, Kafka, Resilience4j circuit breakers, JWT, ZXing/PDFBox tickets. 5 Spring Boot microservices.

**Result:** flash-sale load test at 300,998 requests / 5,000 req/sec across 50 seats, zero overselling. Chaos test confirms the circuit breaker opens correctly under failure.

`Java` `Spring Boot` `Redis` `Redisson` `Kafka` `Resilience4j` `JWT`

[`Anushchinnasamy/ticket-booking-system`](https://github.com/Anushchinnasamy/ticket-booking-system)

</td>
<td width="50%" valign="top">

### 02 · Spicyeat — `Backend`
9 Spring Boot microservices (gateway, auth, user, menu, cart, order, payment, delivery, notifications), database-per-service PostgreSQL with Flyway, Redis caching and gateway rate limiting, Kafka transactional outbox for order/payment events, Stripe payments. React + TypeScript + Vite frontend on Vercel.

**Result:** strict database-per-service ownership; order/payment events survive service crashes without distributed transactions.

`Spring Boot` `Kafka` `Redis` `PostgreSQL` `Stripe` `React` `TypeScript`

[`Anushchinnasamy/SpicyEat`](https://github.com/Anushchinnasamy/SpicyEat)

</td>
</tr>
<tr>
<td width="50%" valign="top">

### 03 · RecruitFlow AI — `GenAI`
8 Spring Boot microservices, RAG pipeline over local LLMs with vector embeddings, pgvector, full Spring Cloud stack (Eureka, Config Server, Gateway, Zipkin, Resilience4j), JWT auth.

**Result:** RAG-based resume-to-role matching backed by a complete Spring Cloud microservice stack.

`Spring Boot` `RAG` `LLM` `pgvector` `Eureka` `Zipkin`

[`Anushchinnasamy/RecruitFlowAI`](https://github.com/Anushchinnasamy/RecruitFlowAI)

</td>
<td width="50%" valign="top">

### 04 · Baaki (TripMeter) — `Backend`
Earnings-truth API for Indian gig riders — real take-home after fuel/EMI/insurance. Modular monolith, Spring Boot, PostgreSQL/Neon, Redis, transactional outbox pattern.

**Result:** deliberate modular-monolith architecture with an outbox pattern for reliable event delivery, sized right for a single-owner project.

`Spring Boot` `PostgreSQL` `Neon` `Redis` `Outbox Pattern`

[`Anushchinnasamy/TripMeterBackend`](https://github.com/Anushchinnasamy/TripMeterBackend)

</td>
</tr>
<tr>
<td width="50%" valign="top">

### 05 · InternFlow AI — `Backend`
17-step state machine for the unpaid-internship lifecycle, Node.js/Express/TypeScript/Prisma/PostgreSQL, LLM-powered, 9 AI-assisted actions, NDA hard gate, full audit trail.

**Result:** every AI action is advisory, logged, and human-reviewable — never autonomous.

`Node.js` `Express` `TypeScript` `Prisma` `PostgreSQL` `LLM`

[`Anushchinnasamy/InternFlow-AI`](https://github.com/Anushchinnasamy/InternFlow-AI) · [`Frontend`](https://github.com/Anushchinnasamy/InternFlow-AI-Frontend)

</td>
</tr>
</table>

<br>

## Architecture Showcase

**Spicyeat** — gateway-fronted microservices, database-per-service, Kafka outbox for order/payment events:

```mermaid
flowchart LR
    Client["React Client"] -->|HTTPS + JWT| GW["API Gateway"]
    GW --> AUTH["Auth Service"]
    GW --> USER["User Service"]
    GW --> MENU["Menu Service"]
    GW --> CART["Cart Service"]
    GW --> ORDER["Order Service"]
    GW --> PAY["Payment Service<br/>(Stripe)"]
    GW --> DEL["Delivery Service"]

    ORDER -.->|order events| KAFKA[("Kafka<br/>outbox")]
    PAY -.->|payment events| KAFKA
    KAFKA -.-> NOTIFY["Notification Service"]

    AUTH --> PG[("PostgreSQL<br/>per service")]
    USER --> PG
    MENU --> PG
    CART --> PG
    ORDER --> PG
    PAY --> PG
    DEL --> PG
    MENU --> REDIS[("Redis<br/>cache")]
    GW --> REDIS
```

**Ticket Booking System** — distributed locking guards a hot 50-seat show against a flash-sale crowd:

```mermaid
flowchart LR
    Client["Client"] --> GW["API Gateway"]
    GW --> USER["User Service"]
    GW --> EVENT["Event Service"]
    GW --> BOOK["Booking Service"]
    GW --> PAY["Payment Service"]

    BOOK -->|tryLock seat| REDIS[("Redis<br/>seat lock")]
    BOOK -->|claim seat| EVENT
    BOOK -.->|booking.created| KAFKA[("Kafka")]
    KAFKA -.-> NOTIFY["Notification Service"]

    USER --> PG[("PostgreSQL<br/>per service")]
    EVENT --> PG
    BOOK --> PG
    PAY --> PG
```

**RecruitFlow AI** — RAG-based candidate ranking behind a full Spring Cloud stack:

```mermaid
flowchart LR
    GW["API Gateway"] --> JOB["Job Service"]
    GW --> CAND["Candidate Service"]
    GW --> MATCH["Matching Service<br/>(pgvector + RAG)"]
    MATCH -->|embed / rank| LLM["Local LLM"]

    EUREKA[("Eureka<br/>service registry")] -.-> GW
    CONFIG[("Config Server")] -.-> GW
    ZIPKIN[("Zipkin<br/>tracing")] -.-> GW
```

**InternFlow AI** — a single state machine gates every lifecycle transition; AI actions are advisory, not autonomous:

```mermaid
flowchart LR
    Client["React Client"] --> API["Express API<br/>(RBAC middleware)"]
    API --> SM["transition()<br/>17-step state machine"]
    SM --> DB[("PostgreSQL<br/>via Prisma")]
    API -->|resume parse / eval / chatbot| LLM["LLM<br/>(logged + human-reviewed)"]
    API --> AUDIT[("Audit trail")]
```

**Baaki (TripMeter)** — modular monolith; a transactional outbox stands in for a message broker:

```mermaid
flowchart LR
    Client["Client"] -->|JWT| API["Spring Boot<br/>modular monolith"]
    API --> RAW["Raw entries<br/>shift / fuel / expense"]
    RAW --> PG[("PostgreSQL / Neon")]
    API --> OUTBOX["Outbox table"]
    OUTBOX -->|poller| JOBS["Async jobs"]
    API --> REDIS[("Redis")]
```

<br>

## Services

```
Backend System Architecture
Microservices Development
Database Design & Optimization
AI Integration & RAG Systems
Performance Tuning & Scaling
```

<br>

## Contact

<div align="center">

[Portfolio](https://portfolio-eta-one-1hhe8hokhj.vercel.app/) &nbsp;·&nbsp; [LinkedIn](https://www.linkedin.com/in/anushchinnasamy) &nbsp;·&nbsp; [LeetCode](https://leetcode.com/u/anushchinnasamy/) &nbsp;·&nbsp; [anushchinnasamy@gmail.com](mailto:anushchinnasamy@gmail.com)

</div>
