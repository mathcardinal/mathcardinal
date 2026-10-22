# Ilya Klimenko

Automation / AI engineer, internal tools. I find the bottleneck in a business process and build the tool that removes it: solo, end to end, from problem analysis to production, with the effect measured in hours and money.

Currently at DocsInBox, an electronic document exchange platform for the restaurant industry (18,000 client accounts). Before that, restaurant operations and front-line support: I automate work I used to do by hand.

**Stack:** Python (FastAPI) · PostgreSQL · Redis · n8n · Supabase · Docker · nginx · Prometheus / Grafana / Loki · OpenClaw agents · Claude Code for routine generation (architecture, review and tests stay mine)

📫 Telegram: [@mathcardinal](https://t.me/mathcardinal) · klimenko.ilya.rb@gmail.com

---

## Selected work

### AI assistant for support agents, in production (code private, employer IP)

An OpenClaw agent embedded in the ticket system. For each customer request it gathers context from the customer's ticket history, the knowledge base, Grafana metrics, logs and outage news, then proposes a solution to the agent or asks clarifying questions.

**The problem.** A 3,000-page knowledge base whose built-in search either found nothing or took 5 to 10 minutes; agents escalated questions that already had written answers.

**The build.** Hybrid retrieval first: PostgreSQL with pgvector for dense search and built-in full-text search for BM25, fused with RRF, bge-m3 embeddings on CPU, incremental indexing through the knowledge-base API. Evaluation before launch: a gold set of real agent queries, recall@5 and MRR, latency budget, error analysis by category. The generative layer was added only after retrieval quality was measured.

**Results.** On about 1,500 requests a day, average resolution time dropped from 6 to 3.5 minutes and SLA metrics improved. About 60 hours of support work freed per day, roughly 6M RUB a year in working-time equivalent. Still evolving on support-team feedback.

### Support training environment (code private, employer IP)

A replica of the company's production interface on synthetic data: the hands-on part of onboarding and certification for a support team of 100+. Built solo in one month without access to the production codebase (UI rebuilt from the running product).

**The problem.** New hires learned from theory. Training cases lived in a shared environment owned by other teams: setting up 4 cases took a month of approvals, and twice the cases were lost to database outages, 200+ hours of restoration work.

**The call.** Isolate training from production dependencies: a standalone environment with synthetic data, owned by the training team, reproducible from git migrations.

**Results.** New-hire certification scores rose from 7.4 to 8.8 out of 10. Case setup time dropped from a month to 4 hours by one trainer. Certification prep time halved.

**Stack.** Alpine.js (interactivity without a build step), self-hosted Supabase, git-based deployment.

### Assessment bot and dashboard → [github.com/mathcardinal/assessment-bot](https://github.com/mathcardinal/assessment-bot)

Monthly certification for 200 employees, run in parallel by a messenger bot with a role-based FastAPI dashboard. Replaced a twice-a-year manual process that occupied three trainers for two months per cycle. About 860K RUB a year saved (10 person-months of manual work). n8n with node logic extracted into unit-tested modules, PostgreSQL, Redis, CI deploy.

### Production server behind all three

Ubuntu, 13 Docker containers, nginx as the only entry point. Monitoring and logging built from scratch: Prometheus, Grafana, Loki, 21 alert rules with runbooks, centralized logs with secret scrubbing. Security built from scratch: service isolation, key-only SSH, fail2ban, host audit with secret rotation. Backups with restore verification. Deploy pipeline with a forced-command SSH key, health check and rollback.
