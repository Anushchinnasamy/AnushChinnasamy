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

Backend engineer at Hexaware Technologies, focused on system design — how services divide responsibility and stay correct under concurrent load. Making something work once is easy; making it hold when everything arrives at the same time and half of it fails is the part I care about. Lately that means designing with LLMs in the loop — RAG, LangChain, agents that call real tools — where the hard part is never the model, it's everything around it.
<br>

## Tech Stack

<div align="center">

**Languages & Backend**

<img src="https://skillicons.dev/icons?i=java,spring,fastapi,nodejs,express&theme=dark" />

**Databases & Messaging**

<img src="https://skillicons.dev/icons?i=postgres,cassandra,redis,kafka&theme=dark" />

**Frontend & Tools**

<img src="https://skillicons.dev/icons?i=react,ts,git,github,vercel,idea,postman&theme=dark" />

**Cloud / DevOps**

<img src="https://skillicons.dev/icons?i=azure,docker,githubactions&theme=dark" />

</div>

<div align="center">

<img src="https://img.shields.io/badge/RAG-9FFF6E?style=for-the-badge&labelColor=101210"/>
<img src="https://img.shields.io/badge/Vector_Embeddings-9FFF6E?style=for-the-badge&labelColor=101210"/>
<img src="https://img.shields.io/badge/LLM_Integration-9FFF6E?style=for-the-badge&labelColor=101210"/>
<img src="https://img.shields.io/badge/AI_Agents-9FFF6E?style=for-the-badge&labelColor=101210"/>
<img src="https://img.shields.io/badge/Resilience4j-9FFF6E?style=for-the-badge&labelColor=101210"/>
<img src="https://img.shields.io/badge/SAGA-9FFF6E?style=for-the-badge&labelColor=101210"/>
<img src="https://img.shields.io/badge/Redisson-9FFF6E?style=for-the-badge&labelColor=101210"/>

</div>

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
