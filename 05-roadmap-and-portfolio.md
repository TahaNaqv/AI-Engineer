# 05 · Roadmap and portfolio

Two plans for getting hired, plus the portfolio that gets you through the door. The full
50-week course in [ROADMAP.md](ROADMAP.md) builds AI/ML depth. This chapter is narrower: the
fastest credible path to an **AI engineer offer** for an experienced full-stack engineer.

---

## How this relates to ROADMAP.md

| Plan | Length | Goal | Maps to |
|---|---|---|---|
| **Six-month plan** (below) | 26 weeks at 10–12 hrs/week | Job-ready for AI-engineer and full-stack-AI roles, with a portfolio | ROADMAP.md phases 0–3, then a portfolio and job-search block |
| **90-day plan** (below) | 13 weeks at 15–20 hrs/week | Applications going out as early as possible | The same content, compressed, with depth deferred |
| **Full course** | ~50 weeks | AI/ML engineer with fine-tuning, serving and DL depth | ROADMAP.md phases 0–8 |

The two shorter plans are the first stretch of the full course, not a different curriculum.
After you're hired, phases 4–8 continue as depth work.

Grigorev estimates **2–3 months** for a backend engineer to become a productive AI engineer.
That's his professional judgement, not measured data, but it fits what transition write-ups
report. Six months gives room for a full-time job and an MS at the same time.

---

## Six-month plan

| Weeks | Focus | Build | Done when |
|---|---|---|---|
| 1 | Setup and orientation | uv/ruff/FastAPI skeleton; Anthropic + OpenAI keys; Langfuse running locally | You stream a structured-output response through FastAPI and see the trace in Langfuse |
| 2–6 | **LLM application engineering** (layers 1–3) | Flagship v0: a FastAPI service plus a Next.js UI with streaming, tools, structured output and measured prompt caching | A cost/latency dashboard exists; you can quote the cost per conversation |
| 7–11 | **Evals and retrieval** (layers 4–5) | Flagship v1: hybrid RAG (pgvector + BM25 + reranker), a 50–100-case golden set, a calibrated judge, a CI eval gate | A table of recall@5 and answer quality for vector-only vs hybrid vs hybrid + rerank |
| 12–16 | **Agents, MCP and security** (layers 6–7) | Flagship v2: an agent with 2+ MCP servers you wrote, approval before writes, cost and step caps, an injection test suite | Task-success and pass^k numbers; a short red-team report |
| 17–19 | **Portfolio project #2**: chosen to contrast with the flagship (see the ranked list) | One project with its own eval table | README written in the format below |
| 20–21 | **Public proof** | 1–2 merged open-source PRs (an eval or agent framework, or an MCP server); one technical blog post from the flagship's results | Links in the CV |
| 22–26 | **Interview preparation and applications** (chapter 06) | 2 timed take-home simulations; mock system design; a CV focused on impact | 30+ targeted applications; first loops under way |

**Start applying around week 16.** Waiting for a perfect portfolio is the most common way to
lose months. Internal moves come even sooner: if your current employer ships AI features,
volunteer for them in month 1. Shipping one real AI feature at work beats any side project. Janvi
Kalra moved from software engineer to AI engineer this way, and is now at OpenAI.

---

## 90-day compressed plan

Use this when you need offers quickly. It assumes 15–20 hrs/week, and it defers depth on
purpose.

| Weeks | Do | Cut |
|---|---|---|
| 1–3 | APIs, tool calling, structured output, streaming, caching. One FastAPI + Next.js service | Model-internals theory |
| 4–6 | Hybrid RAG + reranker + a 50-case golden set + a calibrated judge. Langfuse tracing | GraphRAG, agentic RAG |
| 7–9 | A single-agent loop from scratch, then one framework. One MCP server. Approval gates and an injection test suite | Multi-agent systems, A2A |
| 10–11 | README, eval table, Loom walkthrough, blog post. Re-do one public take-home under time pressure | A second large project |
| 12–13 | Applications, system-design drills, a project deep-dive rehearsal | — |

The result is one strong flagship plus one timed take-home on GitHub. That is enough to
interview. It is not enough for frontier-lab research roles, which aren't the target anyway.

---

## What a portfolio has to prove

Hiring managers describe it the same way: **"ship, measure, defend."**

| Source | What they look for | What they reject |
|---|---|---|
| **Louis-François Bouchard** (hiring for AI engineers) | 1–3 finished projects. A narrow scope, a running baseline, a small verified test set, **at least two approaches compared on quality and cost**, error analysis, a reproducible setup, an honest README | No baseline. Calling prompting "fine-tuning". Dead links. Tutorial datasets. Fine-tunes with no benchmark. "The agent chose it" as an explanation |
| **Ash Tilawat** (CTO, Gauntlet AI) | Judgement over tool use. Knowing the purpose of every major file. Being explicit about where AI coding tools helped, where they failed and how you caught it | Surface-level demos. Being unable to explain your own code |
| **Grigorev field guide** | 20–50 eval examples (easy, messy, out-of-scope, refusal, citation cases). Metrics that fit the task. Per-request logs. CI that runs a small eval | Choosing the technology first. Generic chat-with-docs. Multi-agent setups the problem doesn't need. No eval plan |
| **Anthropic careers page** | Open-source work, blog posts or independent research **at the top of the CV**. About half of its technical staff had no prior ML experience | — |

> **"Evals are the unit tests of AI engineering"** (Bouchard). If a project has no eval table, a
> reviewer will treat it as a demo, however polished it looks.

### Project README template

```
1. Problem: one paragraph, for whom, why it matters
2. Demo: live URL + 2-minute video + screenshots (in case the URL is down)
3. Architecture: one diagram
4. Evaluation: dataset (size, how built), metrics, results table
      approach            | quality | p95 latency | cost / 1k requests
      vector only         |  0.62   |   1.1 s     |   $0.40
      hybrid + rerank     |  0.81   |   1.6 s     |   $0.55
5. Error analysis: what still fails, with examples
6. Trade-offs and what I rejected
7. Security: threat model, what an attacker could do, mitigations
8. Run it: one command, .env.example, seed data
```

### Repository layout

```
README.md  src/  tests/  evals/  data/  .env.example  .github/workflows/  (CI runs tests + a small eval)
```

### The 60-second pitch

Problem → what you built → **evidence** → what still fails → what you'd do next. For example:
*"Beat keyword search on 34 of 50 labelled examples, still failed on billing edge cases, so I
added refusal rules and regression tests."* End on the evidence, not on the tech stack.

### How many projects

**Two or three polished projects.** Every source agrees on this. One should be the flagship that
grows through the course. One should contrast with it, for example extraction against RAG, or
a classical ML model against an LLM. Add open-source PRs on top.

### Presenting work from your current job

- **Lead with impact, not model names.** "Cut support response time 40%" beats
  "LangChain + GPT-4". One reported case: a candidate's before/after showing a 70% cut in
  OpenAI spend led to an offer the next day. That's a vendor anecdote.
- **Write a one-page case study** with no proprietary code: problem → architecture diagram →
  how you evaluated it → metrics → what broke.
- **Rebuild the pattern in public** on synthetic or public data.
- **Rehearse a deep-dive.** OpenAI FDE loops, Mistral and most startup loops include a round
  where you defend decisions on a past project.

Zencore AI (GPT-4o function calling, Whisper, non-custodial transaction preparation) and AliHelp
(RAG WhatsApp SaaS) are good candidates. Both lack published evals. Retrofitting an eval story
onto them is cheap and changes how they read to a reviewer.

---

## Project ideas, ranked by signal

Ranked by four tests: it matches a real take-home archetype, it can be evaluated objectively,
it's hard to fake, and it uses your background.

| # | Project | Why it ranks here |
|---|---|---|
| 1 | **Eval-first domain RAG**, e.g. FBR tax or SECP regulation Q&A in English and Urdu. Citations, an "I don't know" path, a 50-case golden set (answerable / partial / unanswerable), and a vector vs hybrid vs reranked comparison on quality, cost and p95 | Mirrors the most common take-home brief (40%+). Local domain knowledge is hard to copy |
| 2 | **Tool-using operations agent with safety rails**: refunds or support policy, human approval for writes, an injection test suite, structured decision logs, tool-selection and refusal-correctness metrics | Mirrors the RefundPilot, Cohere and Curling take-homes. Shows layer 7 |
| 3 | **Smart-contract audit or exploit-triage agent, scored on EVMbench** (OpenAI + Paradigm, 2026: ~120 vulnerabilities from 40 audits; detect / patch / exploit modes in a sandboxed chain). Report scores on a subset, plus cost per finding | **This is your unique advantage.** Objective scoring, Web3 depth, very few competitors |
| 4 | **LLM gateway / router**: exact and semantic caching, provider failover, OTel tracing, a cost dashboard, load-test numbers (p95, cache-hit rate) | Mirrors the Zuneko brief. Plays straight to backend strength |
| 5 | **Urdu and Roman-Urdu LLM eval harness**: benchmark 5–8 models on UrBLiMP, UrduBench and Roman-Urdu idiom translation, plus a hand-built support set. Publish a leaderboard | A rare and credible low-resource niche. Fits the MS and a possible thesis |
| 6 | **Document extraction pipeline**: invoices, bills or marksheets → validated JSON, with confidence scores and a review UI. Field-level accuracy and schema-validity rate | Extraction is about 15% of take-homes, and it is a real enterprise use case |
| 7 | **Open-source contributions**: 2–3 merged PRs to DeepEval, RAGAS, promptfoo, LangGraph, the AI SDK or an MCP server | Anthropic explicitly asks for this |
| 8 | **On-chain analytics agent**: natural language → SQL over indexed chain data, with SQL validation, text-to-SQL accuracy and token accounting | Combines Web3 and data skills. Text-to-SQL is a common brief |
| 9 | **Urdu voice or WhatsApp assistant** for a local small business: speech-to-text → LLM → text-to-speech, latency budgets, word-error rate, real user logs | Real users beat synthetic demos |
| 10 | **Fine-tune vs prompt comparison**: QLoRA on a narrow task against a frontier model, on accuracy, latency and cost per 1k requests | Shows the judgement of *when not* to fine-tune |
| 11 | **Agent trace viewer** that ingests OTel GenAI spans and flags loops, cost spikes and tool errors | Observability is a growing specialisation |
| 12 | **Wallet-transaction risk explainer**: a classical anomaly model plus an LLM explanation, with precision and recall | Shows classical ML alongside LLM work |
| 13 | **Re-do 2–3 public official take-homes** (Go Fig inbox triage, Jaseci, Bloom) under time pressure, each with a write-up and video | Direct rehearsal for real loops |

**Low signal, avoid:**
- a generic chat-with-PDF app
- Titanic or sentiment notebooks
- a multi-agent "content factory" with no evals
- anything whose README lists frameworks before results

### Recommended combination

**#3 or #1 as the flagship**, **#4 or #6 as the contrast project**, and **#7 running alongside**.
#3 is the most distinctive story: *"I build evaluated AI agents for smart-contract security."*
It turns two specialities into one.
