# Ilya Klimenko

Automation engineer — internal tools. I find the bottleneck in a business process and build the tool that removes it: solo, end-to-end, from problem analysis to production.

Currently at DocsInBox, a B2B EDI platform for the restaurant industry (18,000 client accounts). Before that — restaurant operations and support: I automate an industry I know from the inside.

**Stack:** Python · JavaScript (Alpine.js) · SQL (PostgreSQL) · n8n · Supabase · Claude Code for routine generation (architecture, review, and tests stay mine)

📫 Telegram: [@mathcardinal](https://t.me/mathcardinal) · klimenko.ilya.rb@gmail.com

---

## Selected work

### Support Training Sandbox — *code private (employer IP)*

A pixel-accurate replica of the company's production platform running on synthetic data — the onboarding and certification environment for a 100-person support team. Built solo in one month, without access to the production codebase (UI reverse-engineered from the running product).

**The problem.** Training cases lived in a shared environment owned by other teams: setting up 4 cases took a month of cross-team approvals (trainers, developers, product managers), and twice the cases were lost to database outages — 200+ hours of restoration work.

**The architectural call.** Isolate training from production dependencies entirely: a standalone environment with synthetic data, owned by the training team, reproducible from git migrations. A database loss went from a 100-hour incident to a 10-minute restore.

**Results.** New-hire certification scores rose from 7.4 to 8.8/10 · case setup went from 4 cases/month across four teams to 12 cases in 4 hours by one trainer · certification prep time cut in half.

**Stack.** Alpine.js (interactivity without a build step — speed over framework ceremony) · self-hosted Supabase · git-based deployment.

*The code belongs to my employer and isn't public — happy to walk through the architecture in as much detail as you like.*

### Assessment Bot \& Dashboard → [github.com/mathcardinal/assessment-bot](https://github.com/mathcardinal/assessment-bot)

Monthly certification for 200 employees, run in parallel by a messenger bot. Replaced a twice-a-year manual process that occupied three trainers for two months per cycle — 6× assessment frequency, \~0.8 FTE freed. n8n + self-hosted Supabase.

