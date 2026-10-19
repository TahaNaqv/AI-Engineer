# 06 · Hiring process

How AI-engineer interviews actually run in 2026: the loops, the policies on using AI tools,
take-home assignments, the question themes, and the practicalities of getting hired from
Pakistan.

> **About the evidence.** Fewer than 5% of postings describe their interview process: about 80
> of 1,765 in Grigorev's analysis. Most loop details come from company policy pages, candidate
> write-ups and prep sites. Prep sites are the least reliable of these and are labelled
> wherever they're used. Loop structures change quickly, so confirm the format with your
> recruiter every time.

---

## The typical loop

From Grigorev's field guide (51 companies that disclosed their process):

| Round | Length | Notes |
|---|---|---|
| Recruiter screen | 15–30 min | Motivation, logistics, compensation |
| Technical / coding | 45–60 min | Increasingly practical rather than LeetCode |
| AI/ML deep dive | 45–90 min | Your projects plus LLM fundamentals |
| Take-home | 1–7 days elapsed, 2–4 h of real work | Used by a third of companies. A defence call usually follows |
| System design | 60 min | AI system design: cost, latency, evals, failure modes |
| Behavioural | 30–60 min | Failure stories, stakeholder communication |
| Founder / CEO chat | 15–30 min | At startups |

- **Median:** 4 steps, range 2–7.
- **Total:** 3–6 rounds over 2–6 weeks.

### Trends

- **About 70% of senior interviews had no LeetCode** (from about 130 rounds reported by
  practitioners). When coding does appear, it's practical.
- **System design has moved** from "design Dropbox" to "scale this LLM feature": cost, latency,
  caching, streaming, failure modes.
- **Code-reading, debugging and "review this AI-generated code" rounds** are growing.
- **More rounds are in person:** reportedly 24% in 2022 and 38% in 2025 (prep-site data).
  Google brought back at least one in-person round in Aug 2025 because of concerns about AI
  cheating.
- **AI-run first screens** are appearing (Eightfold, Coinbase).
- **Framework bias is real.** One candidate who worked at the PyTorch/CUDA level was rejected
  for not knowing LangGraph. Match the abstraction level the company works at.

---

## Loops by employer type

### Frontier labs

| Lab | Loop | Reliability |
|---|---|---|
| **Anthropic** (engineering) | Recruiter → **90-min CodeSignal**: build a class to a spec across 4 progressive levels, each unlocked by passing tests, with refactoring → hiring manager → virtual onsite of 4–5 sessions: coding, system design in a Google Doc, values, a project deep dive. Takes 3 weeks to months. No feedback. References are checked thoroughly | Prep-site consensus, plus one first-hand account |
| **Anthropic** (Applied AI, the FDE equivalent) | Recruiter → technical use-case screen built on Claude and MCP → coding → hiring manager → final panel: solution design, values, and a **customer-conversation simulation** | Prep sites |
| **OpenAI** (Forward-Deployed Engineer) | Recruiter → **take-home case study, about 1 week** (e.g. semantic search over a product catalogue that ChatGPT can query, justifying what you rejected) → **AI-enabled coding**: share your screen and narrate → system design (retrieval over a private knowledge base; LLM batching; evals that catch failures before the customer does; a 10× traffic spike) → project deep dive → behavioural | Prep sites. OpenAI's official guide could not be fetched |
| **Google DeepMind** (Research Engineer) | 5–7-round onsite: rapid ML/statistics quizzes, LeetCode medium to hard, implementing attention or a training loop **without AI help**, sometimes a paper presentation. Takes 6–7+ weeks | Prep sites, Blind |

Anthropic's careers page says **about half its technical staff had no prior ML experience**. It
tells engineers to apply as engineers, with open-source work, writing or independent research
at the top of the CV. For a full-stack engineer, the realistic lab targets are **applied and
product teams**, not research.

### Big tech and enterprises

- **Meta:** "AI-enabled coding" since Oct 2025. A multi-file IDE with a terminal and an AI
  panel, alongside one traditional algorithm round. You're graded on how you critique the AI's
  output. You can pass without using it.
- **Amazon:** GenAI use during interviews disqualifies you. The phone screen for one GenAI
  role was LeetCode plus cosine similarity in NumPy. Leadership Principles questions run
  through every round.
- **Microsoft:** no outside help unless explicitly permitted. One Applied AI loop had one
  AI-assisted round and one round without AI.
- **Databricks:** LeetCode, multi-level OOP (build a toy key-value store), ML-infrastructure
  design, 2–3 references.
- **Enterprises and banks** (the biggest hirers by volume, see chapter 02): expect standard
  software-engineering loops with a GenAI module added, and heavier compliance and security
  questions.

### AI startups

- Take-home or **paid work trial**, then a defence call, a founder chat and practical coding.
- Many publish "no LeetCode" policies: Clarium, Column Tax, Phare Health, TensorOps.
- PostHog runs a paid "SuperDay" of real work.
- One line from a YC founder thread captures the bar: **"red flag if the candidate doesn't
  start with evals."**

### Forward-deployed and customer-facing roles

The interviewer plays a stakeholder whose demands keep shifting. Example prompts:

- *"A logistics company wants to know why deliveries are late. Where do you start?"*
- *"A hospital has records in six systems. Give a nurse one view."*
- *"The customer says their dashboard is wrong but can't say which number."*

**Scoring:** a structured breakdown, empathy for the end user, reasoning about data, scoping
judgement, and iterating under pushback.

**Failure modes:**
- jumping to a database or architecture before understanding the user
- proposing the full system instead of the smallest valuable slice
- failing to defend scope

Palantir weights **decomposition** most: turn a vague problem into inputs, a data model, logic
and outputs.

### Pakistan and the Gulf

There is little data on either.

**Pakistani product companies:**
- **Arbisoft** (one Glassdoor report, n=1): a ~90-min online test, an 8-hour on-site
  LeetCode-style coding test, then DSA/OOP/software-engineering interviews. About 25 days to
  hire.
- The general pattern across Pakistani firms appears to be an online DSA/MCQ test → technical
  interview → HR. That's an inference from limited reports.
- Expect GenAI-specific rounds mainly at AI-product companies and at service firms with US
  clients.

**Gulf employers** (G42/Core42, HUMAIN, Careem, ADNOC Digital):
- **No reliable loop data was found.** Ask recruiters, or find alumni on LinkedIn who've been
  through it.

---

## Policies on using AI tools

| Company | Take-home | Live coding | Source |
|---|---|---|---|
| **Anthropic** | Without Claude, unless told otherwise | "This is all you", no AI unless told otherwise. Applications: write your own first draft, then refine with Claude | Official policy page |
| **OpenAI** | Allowed | AI-enabled in FDE coding rounds, with narration. Reports conflict on whether the onsite allows it | Prep sites; conflicting |
| **Meta** | — | AI-enabled round plus one traditional round | Press |
| **Amazon** | — | Banned; disqualifies you | Press (Business Insider) |
| **Microsoft** | — | Banned unless explicitly permitted | Official code of conduct |
| **Datadog** | AI fine for structure, but you must defend every idea live | AI expected in the rounds that say so; banned in the others | Official guidelines |
| **Zapier** | "AI as your collaborator, not your creator". Be ready to say what it contributed | — | Official |
| **Hudson River Trading, Wolters Kluwer** | Banned | Banned | Field guide |

> **The 2026 norm:** take-homes allow AI; nobody explicitly bans it there. Live rounds are
> either *no AI* or *AI expected, with narration*. Either way you are graded on judgement:
> prompting, verifying, and **rejecting bad AI output out loud**. Practise both modes. Never
> hide AI use: undisclosed use disqualifies you at several companies.

---

## Take-home assignments

### What they ask for

From 100+ public GitHub repositories of real take-home submissions (Q4 2025 – Q2 2026), by
assignment type. A brief can count under more than one type:

| Type | Share of briefs |
|---|---|
| RAG with citations | 40%+ |
| Agents and tool calling | 30%+ |
| Conversational AI | 20%+ |
| Document extraction | ~15% |
| LLM-as-judge evaluation | 10%+ |

### Real briefs

| # | Brief | What it tests |
|---|---|---|
| 1 | **Policy-document RAG assistant** (Neura Dynamics): mandatory citations, a safe fallback, a 7-question eval set in 3 classes (answerable / partially answerable / unanswerable) | Grounding, refusal, eval design |
| 2 | **RAG chatbot** (several companies): answer "I don't have that information" when the context lacks it | Grounding discipline |
| 3 | **Refactor a messy RAG app** (Bithealth): keep the exact endpoints, remove global state, make it testable without services | Software engineering quality |
| 4 | **Sales-insights agent**: refuse PII requests, send only aggregates to the LLM, graded on accuracy and refusal correctness | Data protection |
| 5 | **Agent with database, document search and bash**: bash requires explicit user approval | Human-in-the-loop |
| 6 | **Minimal workflow/graph engine** (Tredence): branching, loops, a 50-step cap, cycle protection, mandatory unit tests | Agent infrastructure |
| 7 | **Four-stage story pipeline** (Hippocratic AI): spec → writer → LLM judge → rewriter, at most 2 revisions | Evaluator-optimiser pattern |
| 8 | **LLM router/gateway** (Zuneko Labs): exact and semantic caching, failover, tracing. Targets: 100+ req/s, p95 < 2 s, cache hit rate > 40% | Production performance |
| 9 | **Markdown-to-slides app**: Next.js + OpenAI, 150k-token documents, a single API call | Context handling, full-stack |
| 10 | **Multi-agent D&D simulation in LangGraph**: graded 30% functionality / 30% challenges / 25% context engineering / 15% code quality | Context engineering |
| 11 | **Question deduplication and clustering** (Krisp): graded with ARI, NMI, homogeneity | Classical ML evaluation |
| 12 | **Agentic RAG over government documents**: fully open source, scored with RAGAS | Open stack, RAG metrics |
| 13 | **Refund-policy agent**: must resist prompt injection, with structured decision logs | Security |
| 14 | **Inbox-triage agent** (Go Fig AI): human-in-the-loop, **2-hour cap**. The official repo is public | Scoping under time pressure |
| 15 | **Real-time earnings-call transcription**: Whisper streaming, financial-signal extraction, delivered over SSE | Streaming, realtime |
| 16 | **OpenAI FDE**: semantic search over a product catalogue that ChatGPT can query, about 1 week | Retrieval and judgement |
| 17 | **Anthropic Fellows**: 5-hour notebook exploring the API as a black box | Experimental method |

**Official public challenge repositories to practise on:** ML6, Jaseci Labs, Jitera, AuxoAI,
Coginis, Future Research, Cerebras, Bloom, Go Fig AI.

### How they're graded

**Graders look for:**
- functional correctness
- architecture and modularity
- **an eval methodology** (a harness and defined metrics)
- production readiness: caching, monitoring, cost, PII handling, rate limits
- tests
- a README that explains trade-offs

**The defence call (45–90 min) often counts for more than the code.**

**Why candidates fail:**
- not asking clarifying questions
- too little effort
- over-engineering without explaining why
- **no evaluation of the AI's outputs**, which graders call the biggest single differentiator
- a weak defence call

> **Watch for exploitative take-homes.** Examples include a full financial-document agent the
> community valued at €6–10k of consulting work, and vague end-to-end features with 2-hour
> limits. Decline briefs that amount to a deployable product, or that arrive before you've
> spoken to a human.

---

## Question themes

### LLM system design

Format: clarify (~5 min) → high-level design (10–15) → deep dive (15–20) → trade-offs.

**Example prompts:**
- Design ChatGPT-style chat
- RAG over 10M articles
- GitHub Copilot
- Perplexity-style search
- Cross-conversation memory
- A hospital voice assistant (noise, privacy, latency)
- Contract generation with compliance
- Processing 10k ID/payslip uploads a month
- Turning doctor notes into insurer billing
- Detecting policy violations
- One query layer over email, calendar, documents and chat
- Scaling an AI chat feature to 1M daily users
- "1M queries a day, cut the cost"

**The depth expected:**
- **Back-of-envelope cost:** 100k users × 10 interactions × 2k tokens = 2B tokens a day.
- Model routing, semantic and prefix caching, batching vs p99 latency.
- Guardrails before the model (PII redaction, injection defence) and after it (schema
  enforcement, grounding checks).
- Treat all retrieved and tool content as untrusted. Least privilege. Human approval for writes.
- Offline versioned eval sets plus online sampling.

**How seniority shows:**
- Juniors talk about the prompt.
- Mid-level candidates explain embeddings and RAG.
- **Seniors design the feedback loop** and argue the trade-offs between chunking and context.

### ML system design (classical)

- **Prompts:** recommendations, fraud, spam, search ranking, ad click-through prediction.
- **Framework:** problem and metrics → data pipeline → model → training and evaluation →
  deployment and A/B testing → monitoring.
- **Infrastructure rounds** at Databricks-type companies: feature stores, distributed training,
  serving.

### LLM fundamentals

These are the most frequently cited questions, with the number of sources citing each:

| Question | Sources |
|---|---|
| What makes a system agentic? | 7 |
| How do you detect and reduce hallucination? | 7 |
| Fine-tuning vs prompting vs RAG? | 6 |
| How do you reduce token cost? | 5 |

Also common:
- context-window overflow
- tool failures, retries, idempotency
- temperature and top-p
- transformer architecture, the KV cache, LoRA/QLoRA
- encoder vs decoder
- when *not* to use RAG

**Frontier-lab ML coding:** implement multi-head attention, LoRA or a KV cache from scratch.
Practise on Deep-ML. The glossary in [chapter 03](03-body-of-knowledge.md) covers the
vocabulary.

### RAG debugging

- *"Your RAG bot gives confident wrong answers. How do you debug it?"* Separate retrieval misses
  from generation misses from a stale index.
- Text vs vector search; hybrid plus reranker.
- Citations and attribution.
- The "no information found" behaviour.
- Chunking huge PDFs; semantic caching.

### Agent design

- When is an agent the wrong answer?
- How does tool selection work?
- How do you detect and stop planning loops? What are your termination conditions?
- How do you sandbox tool execution?
- What are the security risks of tool-using agents?
- Which decisions belong to the orchestrator and which to the LLM?

Senior interviewers go 3–5 questions deep into failure modes.

### Evals

- How do you evaluate a chatbot?
- How do you build a golden set?
- How do you measure hallucination rate in production?
- How do you test a new model before rollout?
- Which agent metrics matter?
- How do you calibrate an LLM judge?

Hamel Husain's framing is the safe answer: **error analysis first, look at your data, binary
pass/fail.**

### Coding

- **Progressive implementation, 45–90 min.** This dominates at Anthropic and OpenAI:
  - a key-value store (set/get/delete → TTL → persistence)
  - a web crawler
  - in-memory SQL
  - `cd` with symlinks
  - a credit ledger with expiry
  - refactoring 100–120 lines of nested code
- **LLM-adjacent:**
  - cosine similarity in NumPy
  - debugging embedding code
  - logistic regression with SGD, L2 and early stopping, in NumPy
- **LeetCode still appears**, especially at big tech, in Pakistani loops and in Anthropic's
  CodeSignal round. 75–150 NeetCode problems is the usual recommendation.
- **AI roles are often "full-stack in disguise":** the JS event loop, async and the GIL, queues.

### Behavioural

- *"Describe a project where your AI solution failed."*
- *"Explain a complex concept to a non-technical stakeholder."*
- *"What would you do if the project proved infeasible halfway through?"*
- *"How do you stay current?"*

Use STAR or SAIL (situation, action, impact, learning), and don't reuse the same story across
rounds.

**Red flag: LLM hype.** One senior candidate got a soft no for pushing an LLM onto a regression
problem where it didn't fit.

---

## Interview preparation plan

From the field guide, 8–12 weeks:

| Weeks | Focus |
|---|---|
| 1–2 | DSA (NeetCode 75–150), practical progressive-implementation drills |
| 3–4 | ML/LLM implementation: attention, LoRA, cosine similarity, logistic regression from scratch |
| 5–6 | LLM and ML system design, out loud, against a timer |
| 7–8 | Portfolio polish, a rehearsed project deep dive, the 60-second pitch |
| 9–10 | Mock interviews, including one with AI and one without |
| 11–12 | Company-specific preparation: policies, products, the recruiter's stated format |

**One example:** Mimansa Jaiswal prepared 12 weeks at about 6 hours a day, solved 150+ NeetCode
problems, interviewed at 20+ companies and received multiple offers. Janvi Kalra interviewed at
46 companies over roughly 6 months before joining OpenAI.

---

## Getting hired from Pakistan

### "Remote" usually means country-restricted

- In one sample, **118 of 200** remote jobs were US-residents-only.
- Only about **8%** of AI-engineering listings on employer career sites are remote (chapter
  02).
- **Pakistan isn't on the usual no-hire lists.** Those are typically North Korea, Cuba, Iran,
  Syria, Sudan and Crimea. Exclusions are usually about payroll or EOR coverage and tax.
- **Target** postings that say *Worldwide*, *EMEA* or *APAC*, or ask the recruiter directly.
- **EU and Gulf time zones fit best.** PKT is UTC+5: 1 hour ahead of the UAE, 3–4 hours ahead of
  the UK/EU, 9–10 hours ahead of US East. Working with US Pacific means evening or night shifts,
  usually 7 pm–4 am, or a 3–4-hour overlap window.

### Employment vehicles

| Vehicle | Notes |
|---|---|
| **Contractor** via Deel or direct invoice | Most common. Watch for misclassification: Deel's contractor practices have been publicly questioned, and Pakistan was named |
| **EOR employee** via Remote, Oyster or Deel | All three run EOR in Pakistan. Employer on-costs are about 30–35%, including mandatory Eid bonuses |
| **Payments** | PayPal is still unavailable. Payoneer (links to JazzCash) and Wise work. The FBR has looked at Payoneer inflows, and the export-vs-business-income classification is ambiguous. **Get a tax adviser.** The IT-export tax treatment and PSEB registration benefits could not be verified |

### Platforms

| Platform | Process | Notes |
|---|---|---|
| **Turing** | Profile → experience survey → stack MCQs → live coding. Retake after 3 months | Claims the top 1% are accepted |
| **Toptal** | Language → timed test → live interview → paid test project, over 2–5 weeks | Claims 3% acceptance |
| **Arc.dev** | Has Pakistan-specific pages | — |
| **YC Work at a Startup** | Filter for remote/worldwide | Many listings are still US-only |
| **Mercor-style AI-training contracts** | AI interview + ID check. SWE projects pay $100–250/h; generalist work $15–20/h | Good bridge income. **Weak portfolio signal** |

### Gulf relocation

| Route | Requirements | Reliability |
|---|---|---|
| **UAE Green Visa** (5-year, renewable) | Skilled employee: a valid contract, MoHRE occupational level 1–3, a bachelor's degree, **at least AED 15,000/month** | Official (u.ae) |
| **UAE Golden Visa** (10-year) | Skilled route: about AED 30,000/month *basic* salary, MoHRE level 1–2, a degree. A separate coders/AI route by nomination | Commercial guides; verify with ICP or the UAE AI Office |
| **KSA Premium Residency, "Special Talent"** | Degree, 3+ years' experience, employer endorsement. SAR 35k/month for the science and health track. SAR 4,000 fee | Secondary |
| **Ordinary employer-sponsored work visa** | The route most people actually take | — |

---

## Realistic timeline for this profile

| Months | Milestone |
|---|---|
| 0–3 | Skills (layers 1–5) and flagship v1 with an eval table. Volunteer for AI work at your current job |
| 3–6 | Flagship v2 (agent + MCP), contrast project, open-source PRs. **Start applying from month 4** to EU, Gulf, worldwide-remote and Pakistani AI-product roles |
| 6–9 | Loops and offers. Use AI-training contracts as bridge income if needed |

Most company loops take 2–6 weeks. Allow for months at frontier labs.

## Unverified or low-confidence claims in this chapter

- OpenAI's official interview format and its policy on AI tools.
- The order of Anthropic's rounds.
- Pass rates quoted by prep sites, e.g. "4 in 10 pass".
- The in-person-round percentages.
- The take-home success anecdotes from vendor blogs.
- All rate, salary and visa-threshold figures not marked official.
- Gulf interview loops, for which no data was found.
- The general pattern across Pakistani companies, which is inferred.
