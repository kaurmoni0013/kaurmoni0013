<div align="center">

# Hi 👋, I'm Moni Kaur

**Computer Science & Artificial Intelligence undergraduate building full-stack and backend systems with the MERN stack.**

B.Tech CSE & AI · Class of 2028 · CGPA 9.4/10

[![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/kaurmoni0013)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/kaurmoni0013)
[![LeetCode](https://img.shields.io/badge/LeetCode-FFA116?style=flat-square&logo=leetcode&logoColor=black)](https://leetcode.com/u/kaurmoni0013/)
[![GeeksforGeeks](https://img.shields.io/badge/GeeksforGeeks-2F8D46?style=flat-square&logo=geeksforgeeks&logoColor=white)](https://www.geeksforgeeks.org/user/kaurmoni0013/)
[![Portfolio](https://img.shields.io/badge/Portfolio-161b22?style=flat-square&logo=github&logoColor=white)](https://kaurmoni0013.github.io/Portfolio/)
[![Email](https://img.shields.io/badge/Email-EA4335?style=flat-square&logo=gmail&logoColor=white)](mailto:kaurmoni0013@gmail.com)

</div>

---

## About

I'm a B.Tech Computer Science & AI undergraduate (2028) who works mostly in C++ and the MERN stack. What I care about is the part of a web app that's hard to fake: concurrent writes, states that can't be reached illegally, authentication that fails closed, and cost control when a third-party API sits in the request path.

Two full-stack products so far — a clinic appointment system and an AI conversation workspace — both with real auth, real persistence, and CI that runs an end-to-end suite on every push. Right now I'm building projects and closing gaps in my software engineering fundamentals: testing, system design, and deployment.

---

## What I'm Working On

- **MERN full-stack development** — React SPAs on a Node/Express API, React Query for server state
- **Backend engineering** — REST APIs, JWT auth with server-side session revocation, SSE streaming
- **Redis** — rate limiting, token quotas, atomic reservations, short-lived locks
- **Authentication & authorization** — role-based access control, per-record ownership checks
- **DSA in C++** — daily practice, mostly arrays, strings, trees, graphs and DP
- **AI API integration** — OpenRouter, streaming, retry and timeout handling, usage accounting
- **Docker & deployment** — Compose stacks, single-origin images, Render blueprints
- **System design fundamentals** — state machines, indexes, transactions, consistency

---

## Tech Stack

| Area | |
|:--|:--|
| **Languages** | ![](https://skillicons.dev/icons?i=cpp,java,js,html,css) `SQL` |
| **Frontend** | ![](https://skillicons.dev/icons?i=react) `React Query` |
| **Backend** | ![](https://skillicons.dev/icons?i=nodejs,express) `REST APIs` · `JWT` · `Server-Sent Events` |
| **Databases** | ![](https://skillicons.dev/icons?i=mongodb,redis) `Mongoose` |
| **AI / APIs** | `OpenRouter` |
| **Tools** | ![](https://skillicons.dev/icons?i=git,github,docker,linux,postman,vscode) |

---

## Featured Projects

### MediQueue

**Clinic Appointment & Queue Management System** · MERN

A MERN application that replaces a small clinic's paper register with appointment booking, a live patient queue, and wait-time estimates, split across four role-specific portals. Every rule — slot conflicts, who may transition an appointment, who may read a consultation — is enforced on the server rather than in the UI.

`MERN` `MongoDB` `Mongoose` `React` `React Query` `Node.js` `Express` `JWT` `Vite`

[![Source](https://img.shields.io/badge/Source-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/kaurmoni0013/MediQueue)
[![Live Demo](https://img.shields.io/badge/Live%20Demo-2ea44f?style=flat-square&logo=render&logoColor=white)](https://mediqueue-1cu4.onrender.com/login)

**Engineering highlights**

- **Race-safe booking** — slots are re-verified at booking time *and* protected by a partial unique index on `(doctor, date, startTime)` scoped to active statuses, so two patients can never hold the same slot even under simultaneous requests
- **Appointment state machine** — `SCHEDULED → WAITING → IN_CONSULT → COMPLETED` (plus `CANCELLED`) with actor rules per transition; illegal moves return a machine-readable `409` code instead of a generic error
- **Queue as a view, not a table** — position and ETA are derived on read from active appointments, so they can't drift out of sync with the database
- **RBAC enforced twice** — client-side route guards *and* server middleware, backed by per-record ownership checks so a patient can't open someone else's visit
- **JWT session revocation** — signing out bumps a per-user token version, immediately invalidating every token previously issued to that user
- **Hardened by default** — bcrypt, `helmet`, global and auth-scoped rate limits, centralized error mapping with no stack-trace leaks, and a production boot that refuses to run on the default JWT secret
- **Verified continuously** — 67/67 end-to-end API checks covering auth, role guards, the status machine, rate limits, revocation and slot conflicts, run on every push against a real MongoDB service container

---

### Orbit AI

**Full-Stack AI Conversation Workspace** · MERN + Redis

An AI chat workspace built for sustained use rather than one-off prompts: persistent conversations with bounded context and rolling summaries, streaming responses, and a usage model that can't be overrun. Redis handles coordination — atomic token reservations, quota windows and locks — while MongoDB transactions keep paired messages and usage totals consistent.

`React` `Node.js` `Express` `MongoDB` `Redis` `OpenRouter` `SSE` `JWT` `Docker`

[![Source](https://img.shields.io/badge/Source-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/kaurmoni0013/Orbit-AI)
[![Live Demo](https://img.shields.io/badge/Live%20Demo-2ea44f?style=flat-square&logo=render&logoColor=white)](https://orbit-ai-k1m5.onrender.com)

**Engineering highlights**

- **Streaming that fails safely** — Server-Sent Events with first-byte and idle timeouts, bounded retries on transient provider errors, and provider requests aborted when the client disconnects
- **Atomic quota reservations** — Redis reserves a token window *before* the provider call and reconciles it against real usage afterwards; reservations are released on failure, so quota is never double-charged
- **Idempotent retries** — an `x-idempotency-key` replays a completed response from the database instead of calling the provider and billing usage a second time
- **Concurrency locks** — short-lived Redis locks stop duplicate summary jobs when a conversation crosses its summarization threshold
- **Transactional persistence** — the message pair and usage totals are written in a single MongoDB transaction, and only after a stream finishes successfully
- **Session security** — HttpOnly JWT cookies, bcrypt hashing, session-version invalidation, Redis-backed logout revocation, and one-time password reset that stores only a SHA-256 token hash
- **Bounded AI integration** — server-side model allowlist, capped message size, a character budget for assembled context, and provider-reported usage recorded rather than estimated

---

### Portfolio

**Personal developer portfolio** · HTML · CSS · JavaScript

A small static site that collects my projects, certifications and contact links in one place.

[![Source](https://img.shields.io/badge/Source-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/kaurmoni0013/Portfolio)
[![Live Site](https://img.shields.io/badge/Live%20Site-2ea44f?style=flat-square&logo=github&logoColor=white)](https://kaurmoni0013.github.io/Portfolio/)

---

## Hackathons & Activities

- **Smart India Hackathon** — *RailQR-Mark*: AI-assisted laser QR track fitting traceability and predictive maintenance for Indian Railways. React + TypeScript frontend, Python FastAPI + SQLAlchemy backend, scikit-learn risk scoring. [Repository](https://github.com/kaurmoni0013/railqr-mark)
- **HackNexus 2026** — Participant

---

## Certifications

- NPTEL — Programming in C++ — **Elite**
- NPTEL — Programming in Java — **Silver**
- NPTEL — Object-Oriented Programming — **Silver**
- NPTEL — Data Structures & Algorithms — Completed

---

## DSA & Practice

C++ DSA practice, mostly arrays, strings, trees, graphs and dynamic programming. Notes and problem write-ups live in [`dsa-cpp`](https://github.com/kaurmoni0013/dsa-cpp).

[![LeetCode](https://img.shields.io/badge/LeetCode-FFA116?style=flat-square&logo=leetcode&logoColor=black)](https://leetcode.com/u/kaurmoni0013/) [![GeeksforGeeks](https://img.shields.io/badge/GeeksforGeeks-2F8D46?style=flat-square&logo=geeksforgeeks&logoColor=white)](https://www.geeksforgeeks.org/user/kaurmoni0013/)

---

## GitHub Activity

<div align="center">

[![Contribution Streak](https://streak-stats.demolab.com?user=kaurmoni0013&theme=dark&hide_border=true)](https://git.io/streak-stats)

</div>

---

## Let's Connect

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/kaurmoni0013) [![Email](https://img.shields.io/badge/kaurmoni0013@gmail.com-EA4335?style=flat-square&logo=gmail&logoColor=white)](mailto:kaurmoni0013@gmail.com) [![Portfolio](https://img.shields.io/badge/Portfolio-161b22?style=flat-square&logo=github&logoColor=white)](https://kaurmoni0013.github.io/Portfolio/) [![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/kaurmoni0013)
