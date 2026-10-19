# AI Engineer — Research Dossier

What the AI engineer role actually is, what the hiring data says, what transfers from
full-stack work, what's missing, and the order to fix it in.

First compiled 7 September 2026. Fully re-researched and completed 19 October 2026.

## Contents

| File | Covers |
|---|---|
| [01-the-role.md](01-the-role.md) | Definition, sub-populations, adjacent roles, day-to-day reality |
| [02-market-data.md](02-market-data.md) | Skill frequencies, use cases, job market, compensation |
| [03-body-of-knowledge.md](03-body-of-knowledge.md) | The eight technical layers, in priority order |
| [04-tooling.md](04-tooling.md) | Frameworks, eval platforms, vector stores, serving — what to learn |
| [05-roadmap-and-portfolio.md](05-roadmap-and-portfolio.md) | Six-month plan, 90-day compressed version, portfolio projects |
| [06-hiring-process.md](06-hiring-process.md) | Interview loops, take-home assignments, question themes |
| [07-risks-and-resources.md](07-risks-and-resources.md) | Open debates, specialisation tracks, books, courses, people |
| [sources.md](sources.md) | Full source list, by chapter, with reliability grades |

**Course plans built on this dossier:**

| File | For |
|---|---|
| [ROADMAP.md](ROADMAP.md) | The full ~50-week course for an experienced full-stack engineer, built around one flagship project |
| [ROADMAP-FRESH-GRADUATE.md](ROADMAP-FRESH-GRADUATE.md) | A ~20-month version for a fresh graduate doing an MS in Data Science |

---

## The short version

An AI engineer in 2026 is a production software engineer who owns systems built on
foundation models they did not train. The job is roughly 70% ordinary software engineering
and 30% a new discipline. That 30% is almost entirely about *measuring* non-deterministic
systems, not about mathematics.

### Ten findings that shape everything else

1. **The role split from ML engineering.** ML engineers train models. AI engineers build
   systems on top of models. They use different stacks, face different interviews and sit in
   different hiring markets.
2. **97% of postings are production roles, not research.** About 5% are classical ML under a
   new title. Employers are moving further toward integration: the share of AI-first postings
   asking for integrator skills rose from 80% to 88% between February and August 2026.
3. **RAG, agents and evals are the core.** RAG appears in about 40% of all postings and 54% of
   AI-first ones. Agents appear in 72% of AI-first postings. Half of postings now want both.
   Fine-tuning is *mentioned* in 15–27% but is *core* to under 5%.
4. **Python is non-negotiable** (71–83% of postings). TypeScript is the strong second language
   (19–23%), which is where your existing skills land. 87% of postings are full-stack in
   practice.
5. **Evaluation is the 2026 differentiator.** It appears in 60% of AI-first roles and is a
   stated responsibility in 68%. It's the step most candidates skip, and every hiring source
   checks for it.
6. **The entry-level door is nearly shut.** Only 1–2.5% of AI-engineer postings target 0–2
   years of experience. The median new AI engineer had 3.7 years. The sweet spot is 2–6 years,
   and as an experienced engineer you're already inside it.
7. **Demand is growing fast but unevenly.** About 7.3% of US postings mention AI, double the
   level of a year earlier. AI-titled roles are up 173% YoY. The biggest hirers are banks and
   insurers, not AI labs. *Qualified* still means shipped to production, not certified.
8. **Your fastest route is your current job, not a course.** Shipping one real AI feature at
   work beats six months of tutorials on a CV.
9. **Security is now part of the job.** Prompt injection is #1 on the OWASP LLM Top 10.
   "Excessive agency" rose to #3 in the 2026 edition. AI-security postings are up 268%.
10. **Cost and latency are engineering constraints, not finance problems.** Agents use about 4×
    the tokens of chat, and multi-agent systems about 15×. A cheap price per token does not
    mean a cheap task.

### On the numbers in this dossier

Most skill statistics come from **one author, Alexey Grigorev, across two snapshots**: 889
postings from January 2026 (v1), and 6,964 postings from February–August 2026 (v2, about 38% of
them Indian). Chapter 02 names the snapshot behind every figure. Volume trends come from the
Indeed and Lightcast trackers, which are reliable. Salary figures are far softer: outside
Levels.fyi, they come from recruiter and vendor content that can disagree by 2×.

**Treat skill frequencies as reliable, compensation bands as directional, and anything an SEO
blog calls a "2026 trend" as a hypothesis.**

**Corrections in this revision:**
- "95.6% production" is now **97.1%**, the newer v2 figure.
- "Fine-tuning 8.5%" was misleading: the accurate figure is mentioned in 15–27%, core to
  under 5%.
- These claims had no primary source and have been removed:
  - "demand outruns supply 3:1"
  - "agents make 50–200 calls per task"
  - "+74% vs +33% YoY"

See the corrections table in [02-market-data.md](02-market-data.md#corrections-to-earlier-claims).
