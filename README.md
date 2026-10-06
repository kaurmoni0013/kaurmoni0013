<div align="center">
  <img src="./assets/profile-header.svg" alt="Moni Kaur — Computer Science and AI student building thoughtful software" width="100%" />

  <br />

  <img src="https://readme-typing-svg.demolab.com?font=DM+Serif+Display&weight=400&size=23&duration=3200&pause=1000&color=87547F&center=true&vCenter=true&width=820&height=48&lines=Full-stack+craft%2C+backend+care;Products+built+for+the+real-world+details;Learning+by+shipping%2C+testing%2C+and+improving" alt="Full-stack craft, backend care; products built for real-world details; learning by shipping, testing, and improving" />

  <br />

  <a href="https://www.linkedin.com/in/kaurmoni0013"><img src="https://img.shields.io/badge/LinkedIn-Let's_connect-0A66C2?style=flat-square&logo=linkedin&logoColor=white" alt="Connect on LinkedIn" /></a>
  <a href="mailto:kaurmoni0013@gmail.com"><img src="https://img.shields.io/badge/Email-Say_hello-EA4335?style=flat-square&logo=gmail&logoColor=white" alt="Email Moni" /></a>
  <a href="https://kaurmoni0013.github.io/Portfolio/"><img src="https://img.shields.io/badge/Portfolio-Take_a_look-7357E8?style=flat-square&logo=googlechrome&logoColor=white" alt="Visit my portfolio" /></a>
  <a href="https://github.com/kaurmoni0013"><img src="https://img.shields.io/github/followers/kaurmoni0013?style=flat-square&label=GitHub%20followers&logo=github" alt="GitHub followers" /></a>
</div>

<br />

> **I like the details you don't see in a screenshot:** two people can't book the same appointment, a retry can't charge twice, and one user's data stays theirs.

I'm **Moni Kaur**, a B.Tech Computer Science & AI undergraduate (Class of 2028, CGPA **9.4/10**) at Arya College of Engineering & IT. I build full-stack products and enjoy working through the backend decisions that make them reliable. My main toolkit is **React, Node.js, MongoDB, Redis, and C++**.

I like taking a product from a rough idea to a working interface, then asking the less glamorous questions: What happens when two requests arrive together? What if a stream fails halfway through? Can someone recover without losing context?

**Currently:** building projects, practicing C++ DSA, and strengthening my foundations in testing, system design, and deployment.

## Find your way around

| Want to see… | Start here |
|:--|:--|
| The products I spend the most time on | [MediQueue](#1-mediqueue--make-the-waiting-room-make-sense) · [Orbit AI](#2-orbit-ai--a-workspace-for-the-whole-conversation) |
| What I build with | [Tools & technologies](#the-toolkit) |
| How I think through engineering problems | [The details behind the UI](#the-details-behind-the-ui) |
| My learning projects and DSA practice | [Learning in public](#learning-in-public) |
| Current GitHub activity | [Activity](#activity-not-a-trophy-case) |

## Two products, two different problems

### 1. MediQueue — make the waiting room make sense

**A clinic appointment and queue system** · [Source code](https://github.com/kaurmoni0013/MediQueue) · [Try the demo](https://mediqueue-1cu4.onrender.com/login)

<a href="https://mediqueue-1cu4.onrender.com/login"><img src="https://raw.githubusercontent.com/kaurmoni0013/MediQueue/main/docs/screens/patient-dashboard.svg" alt="MediQueue patient portal with a live queue and next appointment" width="100%" /></a>

MediQueue replaces a small clinic's paper register with one connected workflow. Patients book appointments and follow their queue; staff manage check-ins; doctors handle consultations; admins manage the clinic. Four portals, one source of truth.

The central challenge is not making a booking form. It is keeping the appointment, queue, and permissions correct when real requests hit the server.

| The product decision | Why it matters |
|:--|:--|
| **Treat a time slot as a shared resource.** Re-check availability when booking, then back it with a partial unique database index. | Two simultaneous requests cannot claim the same active slot. |
| **Derive queue position instead of storing it.** Calculate position and estimated wait from active appointments when needed. | Queue numbers do not go stale when an appointment changes. |
| **Make appointment transitions explicit.** `SCHEDULED → WAITING → IN_CONSULT → COMPLETED`, with `CANCELLED` as a separate path. | Each action has an allowed actor and invalid transitions return a meaningful conflict. |
| **Enforce access at the API.** Role middleware and record ownership checks sit behind the UI route guards. | A hidden button is not an authorization check. |

**Built with:** React · React Query · Node.js · Express · MongoDB · Mongoose · JWT · Vite<br />
**Verification:** a 67-check end-to-end API suite for auth, role guards, appointment transitions, rate limits, revocation, and conflicting bookings.

<details>
<summary><strong>More about the engineering</strong></summary>
<br />

- Four role-specific portals share server-side rules rather than trusting the client to enforce clinic policy.
- The active-slot constraint is a database guarantee as well as an application check; the database remains the final arbiter under concurrency.
- Queue position and wait time are computed from the current appointment list, rather than maintained as a second piece of state.
- Consultation notes and prescriptions follow the appointment lifecycle, with access controlled by role and record ownership.
- JWT session revocation, password hashing, rate limits, centralized error mapping, and production-secret checks are part of the application—not just a future checklist.

</details>

---

### 2. Orbit AI — a workspace for the whole conversation

**A persistent AI conversation workspace** · [Source code](https://github.com/kaurmoni0013/Orbit-AI) · [Open the live demo](https://orbit-ai-k1m5.onrender.com)

<a href="https://orbit-ai-k1m5.onrender.com"><img src="https://raw.githubusercontent.com/kaurmoni0013/Orbit-AI/main/docs/assets/orbit-workspace-preview.svg" alt="Orbit AI conversation workspace preview" width="100%" /></a>

Orbit AI is built for conversations that continue beyond one prompt. Chats, messages, summaries, and usage persist; responses stream as they are generated; and the application keeps usage and retries under control.

| Problem to solve | How Orbit handles it |
|:--|:--|
| A response should feel immediate | Server-Sent Events stream provider output, with timeouts and cancellation when the client disconnects. |
| Long conversations need useful context | A bounded context builder combines a rolling summary with recent unsummarized messages. |
| A retry must not mean a second charge | An idempotency key replays an already-completed response instead of calling the AI provider again. |
| Usage must be controlled before a provider call | Redis reserves quota atomically, then reconciles it with actual provider usage. |
| Related records should not drift apart | MongoDB transactions persist the completed message pair and usage together. |

**Built with:** React · Node.js · Express · MongoDB · Redis · OpenRouter · SSE · Docker

<details>
<summary><strong>More about the engineering</strong></summary>
<br />

- HttpOnly JWT cookies, bcrypt password hashing, session-version invalidation, logout revocation, and one-time password recovery.
- Redis-backed rate limits, atomic token-window reservations, short-lived locks for summarization, and quota reconciliation.
- Provider model allowlists, bounded message/context sizes, request timeouts, and recorded provider-reported usage.
- If a response fails or the browser disconnects, the provider request is aborted and its reservation is released.
- Search, pinning, renaming, deleting, dark/light themes, and responsive navigation make it a workspace rather than a bare chat box.

</details>

---

## The details behind the UI

These are the engineering questions I tend to follow past the first working demo:

| Area | What I pay attention to |
|:--|:--|
| **Concurrency** | Is a check-then-write safe if two requests pass the check at once? Can the database enforce the invariant? |
| **State** | Are valid transitions explicit? Can computed data be derived instead of copied and allowed to drift? |
| **Identity & access** | Does every resource query verify ownership on the server? Can a session be revoked before its token expires? |
| **Streaming & external APIs** | Are there timeouts, cancellation, bounded retries, and a clean response to provider failures? |
| **Persistence** | Which writes belong in a transaction? Could an idempotency key make a retry safe? |
| **Verification** | Do tests exercise role boundaries, invalid transitions, concurrent conflicts, and unhappy paths—not only the happy path? |

## The toolkit

I use technologies to solve the product problem, not as a checklist. These are the tools appearing in my projects and practice:

<table>
  <tr>
    <td width="50%" valign="top">
      <strong>Languages</strong><br /><br />
      <code>C++</code> <code>Java</code> <code>JavaScript</code> <code>TypeScript</code> <code>SQL</code>
    </td>
    <td width="50%" valign="top">
      <strong>Frontend</strong><br /><br />
      <code>React</code> <code>React Query</code> <code>Vite</code> <code>HTML</code> <code>CSS</code>
    </td>
  </tr>
  <tr>
    <td width="50%" valign="top">
      <strong>Backend & data</strong><br /><br />
      <code>Node.js</code> <code>Express</code> <code>MongoDB</code> <code>Mongoose</code> <code>Redis</code> <code>REST</code> <code>SSE</code>
    </td>
    <td width="50%" valign="top">
      <strong>Building & debugging</strong><br /><br />
      <code>Git</code> <code>GitHub Actions</code> <code>Docker</code> <code>Linux</code> <code>Postman</code> <code>API testing</code>
    </td>
  </tr>
</table>

## Learning in public

Not every repository needs to be a flagship product. I also keep smaller work visible as a record of practice and experimentation.

| Repository | What you will find |
|:--|:--|
| [dsa-cpp](https://github.com/kaurmoni0013/dsa-cpp) | C++ problem solving organized by topic, with approaches and complexity analysis. |
| [cpp-code](https://github.com/kaurmoni0013/cpp-code) · [oops-code](https://github.com/kaurmoni0013/oops-code) | C++ practice and object-oriented programming exercises. |
| [Portfolio](https://github.com/kaurmoni0013/Portfolio) | My personal portfolio: projects, background, and contact links. |
| [Solar System](https://github.com/kaurmoni0013/Solar-System) | A visual web project made while exploring CSS and the browser. |
| [Random Quote Generator](https://github.com/kaurmoni0013/Random-Quote-Generator) · [Tic Tac Toe](https://github.com/kaurmoni0013/tic-tac-toe-javascript) | Smaller JavaScript projects exploring APIs, interaction, and game logic. |

### A little outside the editor

- **Education:** B.Tech Computer Science & AI, Class of 2028 · CGPA **9.4/10**
- **NPTEL:** Programming in C++ (**Elite**); Programming in Java (**Silver**); Object-Oriented Programming (**Silver**); Data Structures & Algorithms (**completed**)
- **Current learning:** system design fundamentals, better testing strategies, and deployment
- **Problem solving:** C++ arrays, strings, linked lists, stacks, trees, graphs, recursion, and dynamic programming

## Activity, not a trophy case

The cards below are live summaries of my public GitHub activity. The repositories above tell you more about what I actually build.

<div align="center">
  <img height="170" src="https://github-readme-stats.vercel.app/api?username=kaurmoni0013&show_icons=true&hide_border=true&rank_icon=github&theme=transparent" alt="GitHub overview for Moni Kaur" />
  <img height="170" src="https://github-readme-stats.vercel.app/api/top-langs/?username=kaurmoni0013&layout=compact&langs_count=6&hide_border=true&theme=transparent" alt="Languages used across Moni Kaur's public repositories" />
  <br />
  <img src="https://streak-stats.demolab.com?user=kaurmoni0013&hide_border=true&theme=transparent" alt="GitHub contribution streak" />
  <br />
  <img src="https://github-readme-activity-graph.vercel.app/graph?username=kaurmoni0013&theme=github-compact&hide_border=true&area=true" alt="GitHub contribution activity over time" width="95%" />
</div>

## Say hello

I'm always glad to meet people who enjoy making useful software and sweating the details. If you're building something interesting—or want to talk about a project—find me here:

<div align="center">
  <a href="mailto:kaurmoni0013@gmail.com"><img src="https://img.shields.io/badge/Email-kaurmoni0013%40gmail.com-EA4335?style=flat-square&logo=gmail&logoColor=white" alt="Email Moni Kaur" /></a>
  <a href="https://www.linkedin.com/in/kaurmoni0013"><img src="https://img.shields.io/badge/LinkedIn-Moni_Kaur-0A66C2?style=flat-square&logo=linkedin&logoColor=white" alt="Moni Kaur on LinkedIn" /></a>
  <a href="https://kaurmoni0013.github.io/Portfolio/"><img src="https://img.shields.io/badge/Portfolio-Explore-7357E8?style=flat-square&logo=googlechrome&logoColor=white" alt="Moni Kaur's portfolio" /></a>
</div>

<div align="center">
  <br />
  <sub>Thoughtful products. Reliable systems. A little better with every build.</sub>
</div>
