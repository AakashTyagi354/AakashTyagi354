# Aakash Tyagi

**Specialist Programmer @ Infosys** · Building distributed systems and AI-powered products · Pune, India

I build backend-heavy full stack systems. Currently deep in microservices, LLM engineering, and Spring Cloud. My projects are production-grade, not tutorial clones.

---

## What I'm building

### [Delma — AI-Powered Healthcare Platform](https://github.com/AakashTyagi354/delma2.0_spring_microservice)

13 Spring Boot microservices + Next.js 14 frontend. Built everything from scratch.

**Backend highlights:**
- Spring Cloud Gateway (WebFlux) with JWT auth filter + downstream header injection
- Eureka service discovery + OpenFeign with Resilience4j circuit breakers
- Apache Kafka for async messaging (notification events, RAG indexing, AI report generation)
- Redis for cache-aside (doctor listings) + OTP storage with TTL
- `@Version` optimistic locking on slot booking — prevents double-booking race condition
- ZEGOCLOUD video calls with AES-256 encryption
- Razorpay payment integration with HMAC-SHA256 signature verification
- GitHub Actions CI/CD — multi-arch Docker builds (amd64 + arm64) → Docker Hub

**AI features I engineered:**
- **RAG Document Summarizer** — Voyage AI embeddings (512-dim) + pgvector cosine similarity + Apache PDFBox + Kafka async indexing. Doctors get AI-powered clinical summaries of patient documents before consultations
- **MCP Booking Agent (ReAct pattern)** — Groq qwen3-32b + 5 tools (search doctors, get slots, book, pay). Solved LLM statelessness with Redis slot session injection — prevents hallucinated IDs
- **AI Symptom Checker** — Groq Llama 3.1 + fixed specialization list + JSON fallback to General Medicine
- **Post-Consultation AI Notes** — Kafka pipeline: doctor writes notes → Groq generates 7-section medical report → saved back via Feign

**Tech:** Java 21 · Spring Boot 4 · Spring Cloud Gateway 5 · Kafka · Redis · PostgreSQL · pgvector · Next.js 14 · TypeScript · Redux · Tailwind · Docker · AWS S3

---

## Skills

```
Backend      Java · Spring Boot · Spring Cloud Gateway · Eureka · OpenFeign
             Resilience4j · Apache Kafka · Redis · Hibernate · JPA · REST APIs
             Node.js · Express

Frontend     Next.js 14 · React · TypeScript · Redux Toolkit · Tailwind CSS

AI & LLM     Groq · Voyage AI · pgvector · RAG pipelines · MCP Agent (ReAct)
             Agentic workflows · Spring AI · Prompt engineering

Database     PostgreSQL · Oracle DB · pgvector · Redis

DevOps       Docker · Docker Compose · GitHub Actions CI/CD · AWS S3
             Multi-arch builds (amd64 + arm64) · Kubernetes (learning)
```

---

## Engineering decisions I've made (and why)

**Why optimistic locking over pessimistic for slot booking?**  
Pessimistic (SELECT FOR UPDATE) holds a row lock for the entire transaction — under concurrent load, all booking requests queue. Optimistic (`@Version`) only checks at write time. For a slot booking system where true contention on a single slot is rare, optimistic is the right trade-off.

**Why fixed-size chunking (500 chars, 100 overlap) for RAG?**  
Medical documents in Delma are 1-5 pages. Agentic chunking would add an extra LLM call per document during indexing — tripling API usage against Voyage AI's 3 RPM free tier limit for zero measurable quality improvement on short files. Engineering judgment: pick the right-sized tool.

**Why Kafka for notifications instead of a direct Feign call?**  
If notificationservice is down, a Feign call from appointmentservice fails → booking fails. These shouldn't share failure surfaces. Kafka decouples them — booking returns immediately, notifications eventually consistent.

**Why Redis for OTP storage instead of PostgreSQL?**  
OTPs are ephemeral: short-lived (10 min), read-heavy during verification, deleted on use. Redis `EXPIRE` handles TTL natively. No schema, no cron job, sub-millisecond reads. PostgreSQL would be the wrong tool.

---


## Connect

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/aakash-tyagi-274228206/)
[![LeetCode](https://img.shields.io/badge/LeetCode-FFA116?style=flat&logo=leetcode&logoColor=white)](https://leetcode.com/aakash_tyagi/)
[![Email](https://img.shields.io/badge/Email-D14836?style=flat&logo=gmail&logoColor=white)](mailto:aakashtyagi354@gmail.com)

---

<details>
<summary><b>GitHub Stats</b></summary>
<br>
<img src="https://github-readme-stats.vercel.app/api?username=aakashtyagi354&show_icons=true&theme=default&hide_border=true&count_private=true" />
<img src="https://github-readme-stats.vercel.app/api/top-langs?username=aakashtyagi354&layout=compact&hide_border=true&theme=default" />
</details>
