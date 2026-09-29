## Nikita Satsiuk

**Full-stack developer — TypeScript · Next.js · PostgreSQL.** Brest, Belarus · remote · UTC+3

I build web products end to end, from the database schema to production. I am 20 and I have no formal employment history, so everything below is work you can open and check rather than a claim you have to trust.

---

### [bloomly.by](https://bloomly.by) — flower-subscription marketplace

Designed and shipped alone: database, backend, web, mobile and deployment. Public launch is being prepared; the payment layer is written and smoke-tested but card acquiring is not enabled yet, and I would rather say that here than have you find it out later.

| | |
|---|---|
| PostgreSQL | 65 tables · 83 idempotent migrations · 70 PL/pgSQL functions · 162 row-level security policies · 136 indexes |
| Web | Next.js 16 App Router, React 19 — 84 pages, 184 Server Actions, three isolated dashboards |
| Mobile | Expo / React Native — 47 screens |
| Payments | Alfa-Bank card acquiring (RBS API) and ERIP — integration written end to end and covered by invariants; **live keys are not switched on yet** (they turn on in Q4 together with the company's tax-regime change) |

The payment core is a PL/pgSQL state machine with row locking, so a replayed bank webhook cannot settle an order twice. The charged amount is reconciled against a computed view rather than trusted from the request body. Money logic lives in the database, not in application code.

### [digital-card](https://github.com/Nikich196/digital-card) — GraphQL API · [live](https://digital-card-eight-ochre.vercel.app)

NestJS · Prisma · GraphQL · PostgreSQL · Docker.

DataLoader eliminates N+1 across two levels of nesting, so the full nested query costs exactly six SQL statements — one per table. CI brings up the whole stack with `docker compose` and runs eighteen smoke tests against it, rather than only building the image.

### [gorodki](https://github.com/Nikich196/gorodki) — iOS game about capturing Brest · in progress

A university team project with a classmate; demo in December 2026. Native iOS (Swift, SwiftUI, Live Activities): run or ride around a block and your GPS trace claims exactly that shape — plus fog-of-war exploration, clans, duels and a cycling league. Backend: ASP.NET Core 10 with PostgreSQL/PostGIS on free tiers. Run like a real team repo — issues, milestones, a contributing guide, CI — with **106 merged pull requests** so far. iOS builds now run locally on a Mac (Xcode 27) as well as in CI.

---

### How I work

I am AI-assisted, and I treat that as a discipline rather than a shortcut. I set the architecture, the data schema and the module boundaries myself. Implementation runs through AI agents on frontier models. Every significant result is verified by a **separate script that computes the same thing a different way** — I trust the convergence of two independent methods, not the model.

Two things that habit caught in my own already-shipped code:

**A safeguard that was the attack.** I had written a GraphQL query-depth rule and described it in the README as a security measure. Re-reading it later, I saw that it re-expanded every fragment spread from scratch — so nesting fragments doubles the traversals per level. I did not reason about it, I measured it: a completely valid one-kilobyte document, no cycles, occupied the event loop for **48 seconds** on a public endpoint. The rule written to protect the service was the cheapest available way to take it down. Fixed by memoising each fragment's contribution — 48,000 ms became 2 ms — and I rewrote the README claim, which had justified the rule with a danger that does not exist in this schema.

**A green build over a dead container.** The CI only built the Docker image. When I made it actually start the stack, the container turned out never to have started: Prisma could not detect the OpenSSL version inside Alpine and fell back to an engine for a library absent from the image. Two more layers underneath — the seed needed `ts-node`, missing at runtime, and the Prisma CLI was downloaded from the registry on every container start, so the image required internet access to boot. The README had been telling people to run one command that had never worked. Startup went from over a minute to three seconds.

A green build, a written safeguard and a clean server log are all equally good at producing the feeling that everything is fine.

---

### Stack

`TypeScript (strict)` `JavaScript` `Swift` `C#` `Python` `SQL` `PL/pgSQL`
`Next.js` `React` `React Native` `Expo` `SwiftUI` `ASP.NET Core` `Node.js` `NestJS` `Prisma` `GraphQL`
`PostgreSQL` `PostGIS` `Supabase` `Docker` `GitHub Actions` `Xcode` `Git` `Linux` `macOS`

Studied at Brest State Technical University: C++, C#, Java, Pascal, assembly.

**Not in my toolkit** — stated so you do not have to find out later: Kubernetes, Terraform, Grafana/Prometheus in production, PHP, Vue, down-migrations, and work at large scale.

### Contact

[nikich.2018.s@gmail.com](mailto:nikich.2018.s@gmail.com) · Telegram [@Nikich1405](https://t.me/Nikich1405) · [bloomly.by](https://bloomly.by)

Available for remote work now. English: fluent written, limited spoken — better over text than over a call.
