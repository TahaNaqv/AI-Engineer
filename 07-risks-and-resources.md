# 07 · Risks and resources

The open debates worth having a position on, the risks to plan around, the specialisation
tracks after the generalist role, and the books, courses, people and communities worth your
time. Checked on 19 October 2026.

---

## Part 1 · Open debates

### Is "AI engineer" a durable role or a passing title?

| Durable | Transitional |
|---|---|
| LinkedIn ranks AI Engineer the #1 fastest-growing US job for 2026 | If every engineer integrates LLMs, the title dissolves back into "engineer", the way "web developer" did |
| Gusto's 2026 new-grad data shows AI Engineer growing as a share of graduate hires while Software Engineer shrinks | Boris Cherny, who created Claude Code, predicts the "software engineer" title itself will fade (reported second-hand) |
| The role has its own conference (the World's Fair, 6,000+ attendees), tooling and interview loop | LinkedIn ranks by growth rate, not volume |

**Position:** the *skills* will last: evals, context and retrieval design, agent reliability,
and inference cost and latency. The *title* may well merge back into "engineer" around
2028–2030. Build skills that survive the rename.

### How much maths do you need?

Practitioners agree on a tiered answer:

| Track | Maths needed |
|---|---|
| Application-layer AI engineering | Conceptual linear algebra and probability: vectors, similarity, distributions |
| ML engineering, post-training, inference | Real calculus, optimisation, statistics |
| Research | Much more |

**For you, the highest-return maths is statistics for evals:** sampling, confidence intervals,
inter-rater agreement, κ. It's also what your MS will teach first. Gradient-level maths matters
only on the post-training or inference tracks. Don't let a maths prerequisite turn into a reason
to wait.

### Fine-tuning vs prompting and RAG

- **The consensus heuristic:** RAG for *knowledge*, fine-tuning for *behaviour, format and
  style*. Most production systems use both.
- **A rough cost crossover:** RAG is usually cheaper below about 100k requests a month. A
  fine-tuned small model often wins above about 1M a month on narrow tasks. This is vendor
  analysis.
- **The major 2026 change: OpenAI is reportedly winding down its fine-tuning platform.**
  - A May 2026 update reportedly closed it to new sign-ups and gave existing customers "a few
    more months" of training.
  - This was seen in a search snippet of OpenAI's page and couldn't be fetched directly, so
    check the deprecations page.
- **Meanwhile, fine-tuning is moving to open weights:** Thinking Machines' **Tinker** (GA Dec
  2025), TRL, Unsloth.
- **What follows:** fine-tuning is becoming an open-weight specialist skill, not a checkbox on
  a closed API.

### Long context vs RAG

- Chroma's **"Context Rot"** study (July 2025, 18 frontier models) found that performance
  degrades unevenly as input grows, well before the advertised window is full.
- Needle-in-a-haystack benchmarks overstate real ability, because finding a planted sentence is
  close to lexical matching.
- Some providers also charge more per token above a length threshold.
- **The consensus is a hybrid**, which is exactly what "context engineering" means.
- Claims that 2026 models have solved context rot are unverified.

### Agents vs workflows

- **The case against the hype:**
  - Anthropic's *Building Effective Agents* says to start simple, and that the most successful
    teams used composable patterns, not frameworks.
  - **Gartner (June 2025)** predicts more than 40% of agentic AI projects will be cancelled by
    the end of 2027. It counts only about 130 of thousands of "agentic" vendors as real.
    Caveat: the data comes from a webinar poll.
- **The counter-evidence:** coding agents went mainstream in 2025–26, so "agents don't work" no
  longer holds for coding.
- **METR's productivity studies:**
  - The July 2025 randomised trial found experienced developers were **19% slower** with AI
    tools.
  - The 2026 follow-up called its own data unreliable, because developers refused to work
    without AI. That refusal is itself evidence of adoption.

### Framework lock-in

- **The criticism:** Octomind dropped LangChain because its abstractions made low-level changes
  "hard or impossible" and hid agent state.
- **What changed:** LangChain 1.0 stabilised the API but didn't flatten the abstractions.
- **The other side:** LangGraph is widely used for stateful agents, and frameworks make
  prototyping faster.
- **Position:** learn the raw SDKs plus one orchestration layer, and keep your provider adapters
  thin.

### AI coding agents and the entry-level squeeze

This is the best-evidenced debate in the chapter.

- **Stanford "Canaries in the Coal Mine"** (August 2026 revision, ADP payroll data through June
  2026):
  - Employment of 22–25-year-olds in the most AI-exposed jobs is **19% below** counterfactual,
    up from 15% a year earlier.
  - Experienced workers show no comparable gap.
  - The effect comes from reduced hiring, not layoffs, and is concentrated where AI *automates*
    rather than augments.
  - The authors call it descriptive, not causal.
- **Yale Budget Lab and Brookings** (Oct 2025) found "no discernible disruption" in the overall
  labour market.
- **Indeed** (Jul 2026): **71%** of the rebound in developer postings came from senior roles.
- **SignalFire** reportedly finds big-tech new-grad hiring down about 65% from 2019. This is
  second-hand.

**What follows for you:** with 4+ years of shipped production work, you're on the side of this
split that is being hired.

### Commoditised LLM wrappers

When everyone has the same APIs, model access isn't a moat. What defends a product is
proprietary data, feedback loops, deep workflow integration, distribution and trust.

**Test for any project:** *if OpenAI, Google or Anthropic shipped this tomorrow, would users
stay?*

### Eval reliability and LLM-as-judge

- A June 2026 study of 21 judge models (about 541k judgements) found that exact-match agreement
  overstates reliability compared with chance-corrected κ. It also found that judges can be
  consistent on retest while showing severe position bias.
- Other papers document recency, provenance and length bias.
- **The practitioner answer** (Husain and Shankar):
  - error analysis first
  - binary pass/fail judges
  - every judge calibrated against human labels

### Prompt injection is still unsolved

- **Simon Willison's "lethal trifecta":** an agent with access to private data, exposure to
  untrusted content and an outbound channel can almost certainly be exploited.
- **Infosecurity Europe 2026** (OWASP, Pillar): the problem is not solved at a fundamental level.
  Meta's "Rule of Two" only limits the damage.
- **"Design Patterns for Securing LLM Agents"** (IBM, ETH, Google, Microsoft and others)
  proposes constraining agents after they read untrusted input:
  - Dual LLM
  - Code-Then-Execute (CaMeL)
  - context minimisation

  The authors say general-purpose agents are unlikely to get reliable guarantees with current
  models.
- **OWASP Top 10 for LLM Applications 2026** keeps prompt injection at #1. The **OWASP Agentic
  Top 10** was published December 2025.

### Regulation: the EU AI Act after the Digital Omnibus

The Digital Omnibus on AI is **Regulation (EU) 2026/1744**. It was published 24 Jul 2026 and has
been in force since 27 Jul 2026.

| Date | What applies |
|---|---|
| 2 Feb 2025 | Prohibited practices; AI literacy |
| 2 Aug 2025 | General-purpose model obligations, governance, penalties |
| **2 Aug 2026** | General application, including **Article 50 transparency**: disclosure for chatbots and generated content. *Not delayed* |
| 2 Dec 2026 | New ban on AI-generated CSAM and non-consensual intimate imagery. Grace period for machine-readable content marking ends; sources differ on its scope |
| 2 Aug 2027 | General-purpose models placed on the market before Aug 2025 must comply. Each Member State must have a regulatory sandbox |
| **2 Dec 2027** | Stand-alone high-risk obligations (Annex III), delayed from Aug 2026 |
| **2 Aug 2028** | High-risk AI embedded in regulated products (Annex I) |

**In practice, from August 2026:** if your product serves EU users, it must disclose that
users are talking to AI and mark generated content. Pakistan's **National AI Policy 2025** (July
2025) targets 1M AI professionals by 2030, plus scholarships and AI funds. It is a policy, not a
regulatory regime.

---

## Part 2 · The risks to plan around

| Cluster | Risk | Defence |
|---|---|---|
| **Labour market** | The junior squeeze; titles merging back into "engineer" | Seniority you already have, plus skills that survive a rename: evals, architecture, security |
| **Platform** | Price changes (the cost of a fixed capability level falls 9–900× a year per Epoch AI, while frontier list prices reportedly rose); deprecations (chatgpt-4o-latest retired Feb 2026; legacy OpenAI snapshots end 23 Oct 2026); the reported fine-tuning wind-down | **A model-agnostic gateway, an eval suite that makes model swaps cheap, and an open-weight fallback** |
| **Reliability and security** | Judge bias; unsolved injection; supply-chain attacks (the LiteLLM compromise); EU transparency duties | Calibrated evals, architecture that avoids the lethal trifecta, pinned dependencies, disclosure by design |

---

## Part 3 · Specialisation tracks

| Track | The work | Demand signal | Suits |
|---|---|---|---|
| **Forward-deployed / solutions** | Embed with customers and ship AI deployments | US FDE postings reportedly ~1,200 (2025) → 7,300+ (first 9 months of 2026). India up ~19×. OpenAI's deployment unit; Anthropic's programme to train FDEs. Recruiter-relayed figures | Senior generalists who communicate well. **The best immediate fit for you** |
| **Agent infrastructure** | Durable execution, MCP servers, sandboxes, memory, observability, agent auth | Heavy platform investment (Vercel, Cloudflare, AWS AgentCore). No title-level counts | Backend and platform engineers. **The closest transfer from full-stack work** |
| **Evals and quality** | Error analysis, judge design, regression suites, production monitoring | Nearly half of a sample of AI PM openings asked for eval experience. Humanloop joined Anthropic. A new O'Reilly book. No counts for the title itself | Data-minded engineers. **Pairs with the MS** |
| **AI security** | Red-teaming, injection defence, agent permissions, AI supply chain | AI Security Engineer postings +268% (CyberSN). Amazon AI red-team roles at $178–227k | Security-curious engineers. **Smart-contract security instincts transfer** |
| **AI + Web3** | Agent payments (x402, AP2), wallets for agents, on-chain verification, AI-assisted auditing | x402 moved to the Linux Foundation with Google, Visa, Stripe, AWS and Cloudflare. Volumes are contested. EVMbench exists for auditing agents | **Your unfair advantage.** Small but real niche |
| **Inference and serving** | vLLM/SGLang, KV caching, quantisation, GPU cost | Inferact (from the vLLM creators) $200–400k + equity; Red Hat vLLM roles $136–287k. Often requires upstream contributions | Performance-minded systems engineers. Steep but defensible |
| **Applied ML / post-training** | SFT, DPO and RL on open weights; data curation; distillation | Shifting to open weights; Tinker GA | People with ML depth. Fits after ROADMAP phases 5–6 |
| **AI product engineering** | Streaming and generative UI, human-in-the-loop UX, trust and error UX | Part of every AI product; no discrete data | Frontend-leaning full-stack engineers |
| **Voice / realtime** | STT → LLM → TTS pipelines, speech-to-speech, sub-500 ms time to first audio, telephony | Vendor data only | Realtime and backend engineers |
| **Data engineering for AI** | Parsing, chunking, embeddings, hybrid search, data contracts | Steady; overlaps with context engineering | Data and backend engineers |
| **Multimodal / vision** | Document AI, vision-language pipelines, OCR + LLM | Weak direct data | Applied ML people |

**Suggested path for you:** stay a generalist first, then lean toward **agent infrastructure**
or **forward-deployed** work, with **evals** as the constant. Keep **AI + Web3** as the
differentiator in your story.

---

## Part 4 · Books

| Book | Status (Oct 2026) | Best for |
|---|---|---|
| **Chip Huyen, *AI Engineering*** (O'Reilly) | 1st edition, Dec 2024 | **The core text**: evals, RAG, agents, fine-tuning decisions, inference |
| **Shreya Shankar & Hamel Husain, *Evals for AI Engineers*** (O'Reilly) | **New, Oct 2026** | The evals track; the book version of their course |
| Chip Huyen, *Designing Machine Learning Systems* | 2022; no 2nd edition | Classical ML systems: data, monitoring, drift. The principles still hold |
| **Aurélien Géron, *Hands-On ML with Scikit-Learn and PyTorch*** | Late 2025. A new title, not a new edition of the TensorFlow book | The best single ML foundations book, now in PyTorch |
| Sebastian Raschka, *Build a Large Language Model (From Scratch)* | Sep 2024 | Internals, by building a GPT |
| Sebastian Raschka, *Build a Reasoning Model (From Scratch)* | Early access; print around Nov 2026 (dates conflict) | Inference-time scaling, RL with verifiable rewards |
| Simon Prince, *Understanding Deep Learning* | 2023; **free PDF** | Rigorous deep-learning theory |
| Jay Alammar & Maarten Grootendorst, *Hands-On Large Language Models* | 2024 | Visual intuition for embeddings, RAG, fine-tuning |
| Paul Iusztin & Maxime Labonne, *LLM Engineer's Handbook* | Oct 2024 | An end-to-end LLMOps project. The tooling is ageing |
| John Berryman & Albert Ziegler, *Prompt Engineering for LLMs* | 2024 | Prompt and context design, from the Copilot authors |
| Nathan Lambert, *The RLHF Book* | Free at rlhfbook.com | The post-training track |
| Amidi & Amidi, *Super Study Guide: Transformers & LLMs* | Companion to CME295 | Fast illustrated review before interviews |

Be careful with the wave of 2026 "agent" books. Reviewers warn that many are filler.

---

## Part 5 · Courses

| Course | Cost | Status (Oct 2026) |
|---|---|---|
| **Karpathy, *Neural Networks: Zero to Hero*** | Free | Evergreen. Karpathy **joined Anthropic's pre-training team in May 2026**; Eureka Labs and LLM101n are reportedly on hold |
| **nanochat** (Oct 2025) / **microgpt** (Feb 2026) | Free code; about $100 for a full nanochat run | A complete ChatGPT-style pipeline in ~8k lines / a GPT in ~200 dependency-free lines |
| **Stanford CS336**, Language Modeling from Scratch | Free on YouTube | Spring 2026 lectures posted. Heavy assignments. For the inference and post-training tracks |
| **Stanford CME295**, Transformers & LLMs | Free videos | Autumn 2025. A survey through RAG, agents and evals; no homework. **The efficient bridge** |
| CS224N / CS229 | Free | Stanford Online playlists |
| **Hugging Face** LLM / Agents / MCP / smol courses | Free | Active |
| DeepLearning.AI short courses | Free videos; Pro tier paid | Active. Quality varies; many are vendor-sponsored |
| **Husain & Shankar, *AI Evals for Engineers & PMs*** (Maven) | ~$4,200 list; discounts seen | Current cohort 10 Oct – 21 Nov 2026; lifetime recordings. **The highest-value paid item for this track** |
| DataTalksClub **LLM Zoomcamp** / MLOps Zoomcamp | Free | LLM Zoomcamp 2026 ran June–August, now self-paced. MLOps: next cohort to be announced |
| **Anthropic Academy** | Free, with certificates | About 13–17 courses on the Claude API, Claude Code, MCP and Agent Skills |
| OpenAI Academy | Free courses and badges | Badges are not formal certifications |
| fast.ai Practical Deep Learning | Free | No new version since 2022. Effort has moved to Answer.AI's paid SolveIt |
| Made With ML / Full Stack Deep Learning | Free | **Probably stale**: no updates since 2024 and 2023 |

---

## Part 6 · People, newsletters and communities

### People

| Person | Best for |
|---|---|
| **Simon Willison** (simonwillison.net) | The best daily signal on LLM tooling and **prompt-injection security** |
| **Hamel Husain** (hamel.dev) & **Shreya Shankar** | **Evals** and error analysis |
| **Andrej Karpathy** | Intuition for model internals; from-scratch code. Now at Anthropic |
| **Eugene Yan** (eugeneyan.com) | Patterns, evals, recommenders with LLMs. Now at Anthropic |
| **Chip Huyen** (huyenchip.com) | Systems-level framing |
| **swyx & Alessio**, Latent Space | A map of the industry; runs the AI Engineer conference |
| **Jason Liu** (jxnl.co) | Structured output (Instructor), improving RAG, the business of AI consulting |
| **Sebastian Raschka** (*Ahead of AI*) | Clear explainers on architectures and reasoning models |
| **Lilian Weng** (Lil'Log) | Deep survey posts on agents, hallucination and RL |
| **Nathan Lambert** (*Interconnects*) | Open models, post-training, RLHF |
| **Philipp Schmid** (philschmid.de) | Hands-on Gemini, Gemma and agent posts; at Google DeepMind |
| **Maxime Labonne** | His free *llm-course* roadmap on GitHub; head of post-training at Liquid AI |
| **Jeremy Howard** (fast.ai, Answer.AI) | Pragmatic teaching; "dialog engineering" |
| **Omar Khattab** (DSPy) | "Programming, not prompting" |
| Jerry Liu / Harrison Chase | Direction for document agents (LlamaIndex) / agent frameworks (LangChain) |

### Engineering blogs

- **Anthropic Engineering**: agents, context engineering, tool design, evals
- OpenAI Cookbook and Developers blog
- Google DeepMind and Hugging Face blogs
- Chroma Research: retrieval and context rot

### Newsletters and podcasts

- Latent Space
- Interconnects
- *The Batch* (DeepLearning.AI)
- Simon Willison's blog
- *Ahead of AI*
- the MLOps Community podcast
- ThursdAI

### Conferences

- **AI Engineer World's Fair**: 29 Jun – 2 Jul 2026, San Francisco, about 300 speakers. **Talks
  are free on YouTube**, and the most efficient way to see what practitioners are actually
  shipping.
- **AGNTCon + MCPCon North America**: 22–23 Oct 2026.

### Communities

**Global:**
- DataTalksClub Slack
- Hugging Face Discord
- MLOps Community Slack
- Latent Space Discord
- AI Tinkerers

**Pakistan:**

| Community | Notes |
|---|---|
| **AI Tinkerers Islamabad–Rawalpindi** | Launched June 2026. Builder demos on agents, RAG and evals. **Your best-fit local community** |
| GDG Cloud Lahore / GDG Live Pakistan | "AI Seekho" and "Build with AI" events |
| National AI Policy 2025 programmes | Scholarships, the AI Innovation Fund. Watch for announcements |

---

## Unverified or conflicting claims in this chapter

- The OpenAI fine-tuning wind-down and its dates.
- The scope of the Article 50(2) grace period.
- Print dates for Raschka's *Reasoning* book and the Géron PyTorch book.
- Pricing for the Maven evals course.
- The BenchLM frontier price rise.
- SignalFire's new-grad numbers.
- The FDE posting and compensation figures.
- Lilian Weng's 2026 move.
- Eureka Labs being on hold.
- Course counts at Anthropic Academy.
- The status of Made With ML, Full Stack Deep Learning and fast.ai.
- x402 volumes.
- Salary figures for the security, voice and evals tracks.
