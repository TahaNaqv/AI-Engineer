# 03 · Body of knowledge

What an AI engineer has to know, arranged as eight layers in priority order. The ordering is
based on job data (chapter 02) and on the practitioner sources that define the field. Each layer
lists the concepts, the things you must be able to *do*, the common ways it goes wrong, and how
deep you need to go.

---

## How the canonical sources structure the field

| Source | Structure | What it tells us |
|---|---|---|
| **Chip Huyen, *AI Engineering*** (O'Reilly, 2025) | 10 chapters: foundation models → **evaluation (2 chapters)** → prompting → RAG and agents → fine-tuning → dataset engineering → inference optimisation → architecture and feedback | Evaluation gets more space than prompting. ML knowledge is "nice-to-have". The stack has three layers: application, model, infrastructure |
| **swyx, *The Rise of the AI Engineer*** (2023) | The role sits on the product side of the "API line". It can move left into fine-tuning or hosting | No research background required. The estimate is 100–1,000× more people building with models than training them |
| **Latent Space, 2025 reading list** | 50 papers across 10 fields: frontier LLMs, evals, prompting, RAG, agents, code generation, vision, voice, diffusion, fine-tuning | No 2026 edition exists, so the 2025 list is still current |
| **roadmap.sh, AI Engineer** (197 nodes) and **AI Agents** (101 nodes) | A large *context-engineering* cluster; MCP split into host/client/server/transport; evals, observability, prompt injection | Context engineering is now a top-level topic of its own |
| **Grigorev, *AI Engineering Field Guide*** | Learning path: APIs and structured output → RAG → agents and MCP → testing → observability → **evaluation** → production | For backend engineers: 2–3 months to productivity. Evaluation is "where most engineers struggle" |
| **Anthropic engineering posts** | Workflows vs agents; context as a finite "attention budget"; tool design; agent evals (pass@k vs pass^k) | Start simple. Tools are a contract. Read transcripts |
| **OpenAI, *A practical guide to building agents*** | Agent = model + tools + instructions. Single-agent loop vs multi-agent. Layered guardrails | Prototype with the strongest model, set evals, then move down to cheaper ones |
| **Yan, Bischof, Frye, Husain, Liu, Shankar, *What We Learned from a Year of Building with LLMs*** | Tactical / operational / strategic lessons | BM25 as the baseline. RAG before fine-tuning. Workflows before agents. "The model isn't the moat" |

Grigorev's tally of responsibilities across 4,894 postings supports the same priorities:
building AI systems 98.1%, deployment 78.3%, **evaluation and quality 68.5%**, monitoring
64.3%, performance 57.2%, agents 48.4%, RAG 42.0%, security 40.1%, **fine-tuning 13.8%**,
self-hosting models 2.5%.

---

## The eight layers

| # | Layer | Why it's in this position |
|---|---|---|
| 1 | Software engineering and production Python | Python in 70.8% of postings; 86.8% need non-GenAI skills; deployment is a responsibility in 78.3% |
| 2 | LLM fundamentals | Named in 62.2% of postings; the most common source of interview theory questions |
| 3 | Prompting and context engineering | 34.7% of postings, but a standalone responsibility in only 10%. It's absorbed into everything else |
| 4 | **Evaluation and observability** | Eval skills in 59.7% of AI-first roles; responsibility in 68.5%; two chapters in Huyen. Practitioners spend 60–80% of their time here |
| 5 | Retrieval and RAG | About 54% of AI-first roles; the most common take-home brief (40%+) |
| 6 | Agents, tools and MCP | 71.6% of AI-first roles; the fastest-growing area (+13pp) |
| 7 | Production: cost, latency, caching, security | Performance 57.2%; security 40.1% and rising (+9.4pp) |
| 8 | Model adaptation and serving, plus ML/DL foundations | Fine-tuning core to only 3.6% of roles; self-hosting 2.5%. Depth, not the entry point |

**Agents rank sixth even though they appear in the most postings.** An agent is an LLM with
retrieval, tools and memory running in a loop, so it is built from layers 3–5. Every source
warns against starting with agents. Evals come before agents because reliability over repeated
runs (pass^k) is the hard part of agent work.

> **Learn layers 4–6 as a spiral, not in a straight line.** Build a simple RAG system, evaluate
> it, wrap it in an agent, then evaluate the agent. Each pass through the loop makes the
> previous layer clearer.

---

## Layer 1 · Software engineering and production Python

**Concepts:**
- asyncio and httpx
- Pydantic for typing and validation
- FastAPI
- Background jobs and queues
- Idempotency; retries with backoff and jitter
- Streaming over SSE
- Postgres with pgvector, and Redis
- Docker, CI/CD, one cloud platform
- Data wrangling: pandas or Polars, notebooks

**You must be able to:**
- Ship a typed, tested Python service that streams LLM output.
- Handle 429s and timeouts gracefully.
- Batch-process thousands of documents with concurrency limits.
- Version prompts and configs as code.
- Account for cost on every request.

**Common failures:**
- Code that only runs in a notebook.
- No timeouts on a dependency that is both non-deterministic and rate-limited.
- Blocking calls inside async handlers.
- No per-request cost tracking.

**Depth: fluency.** For a TypeScript engineer the gap is mostly Python idiom: Pydantic,
asyncio, packaging with `uv`, plus the data tools. Your TypeScript transfers directly to the
Vercel AI SDK side of the work.

---

## Layer 2 · LLM fundamentals

**Concepts:**
- Tokenisation (BPE) and how it shapes cost and quirks
- Next-token prediction
- The training pipeline: pretraining → SFT → preference tuning (RLHF/DPO) → RL with verifiable
  rewards. The last step is how reasoning models are made
- Sampling: temperature, top-p, top-k, logprobs
- Context windows and degradation over long contexts
- Embeddings
- Attention, at the level of intuition
- Reasoning models and the effort/latency/cost trade-off
- Mixture of experts
- Hallucination as a structural property of the models
- Knowledge cutoffs; multimodal input

**You must be able to:**
- Estimate the token cost and latency of a design.
- Pick a model tier (frontier, small, reasoning, open-weight) for a task.
- Explain why output varies even at temperature 0.
- Read a model card and a pricing page.
- Use schema-constrained structured output.

**Common failures:**
- Treating the LLM as a database.
- Assuming the output is deterministic.
- Ignoring tokenisation for numbers and non-English text (this matters for Urdu).
- Using a reasoning model where a small fast one would do, or the reverse.

**Depth: concept and mechanism, not derivation.** Be able to sketch attention as
`softmax(QKᵀ/√d)·V` and explain why a KV cache exists. You don't need to derive backpropagation
here. Stanford CME295 lectures 1–3 are the right ceiling.

---

## Layer 3 · Prompting and context engineering

**Concepts:**
- System prompts pitched "at the right altitude": neither micro-rules nor vague
- Few-shot examples (applied-llms suggests at least 5)
- Chain of thought and self-consistency
- XML- and JSON-structured inputs and outputs
- Decomposition and chaining
- Templates and prompt versioning
- **Context engineering**, Karpathy's phrase for "filling the context window with just the
  right information for the next step":
  - what goes in: instructions, tools, retrieved data, memory, history
  - compaction
  - external notes
  - sub-agent isolation
  - just-in-time retrieval
- Context failure modes: rot, distraction, poisoning, clash
- Ordering for cache hits: stable prefix first

**You must be able to:**
- Turn an eval failure into a targeted prompt change.
- Design how context is assembled for a multi-turn agent within a token budget.
- Keep prompts portable across models.
- Know when automated prompt optimisation (DSPy) is worth it. It appears in only 0.8% of
  postings, so it's optional.

**Common failures:**
- Prompt bloat from stacking rule after rule.
- Business logic hard-coded into prompts.
- Stuffing the whole context window instead of retrieving.
- Prompts that break silently on a model upgrade. The fix is to pin versions and re-run evals.

**Depth: practical craft.** No theory beyond layer 2.

---

## Layer 4 · Evaluation and observability (the core skill)

**Concepts:**
- **Error analysis:** open-code about 100 real traces, then group them into a failure taxonomy.
- Grader types: code assertions, LLM-as-judge, human grading. Prefer binary pass/fail over
  1–5 scales.
- **Judge validation:**
  - one judge per failure mode
  - measure TPR and TNR against human labels, with train/dev/test splits
  - check for judge biases: position, length, self-preference
- Pairwise comparison.
- Golden datasets; synthetic data along defined dimensions.
- **Criteria drift:** you learn what "good" means by looking at outputs, so you cannot fully
  specify evals up front.
- Capability suites vs regression suites.
- **pass@k vs pass^k**: at 75% per-trial success, the chance all 3 trials pass is about 42%.
- Offline vs online evals; A/B tests; user-feedback signals.
- **Tracing:** spans for LLM calls, tool calls and retrievals, using OpenTelemetry GenAI
  conventions with Langfuse, Phoenix, LangSmith or Braintrust.
- Cost and latency dashboards; drift monitoring.

**You must be able to:**
- Build a trace viewer or annotation loop.
- Label about 100 traces and derive a failure taxonomy from them.
- Write and validate a judge for each failure mode.
- Wire evals into CI as a regression gate.
- Evaluate retrieval separately from generation.
- Evaluate an agent on both its final state and its trajectory.
- Explain results to product stakeholders.

**Common failures:**
- Generic metrics (ROUGE, "helpfulness 1–5") that don't track product quality.
- Judges nobody has checked against human labels.
- Chasing 100% pass rates, which usually means the evals are too easy.
- Synthetic data that doesn't look like production.
- No trace logging.
- Skipping error analysis entirely.

**Depth: deep, practical, plus basic statistics.** You need confidence intervals, sample size,
inter-annotator agreement (Cohen's κ), and precision/recall. This is the highest-value use of
the MS Data Science statistics. It is the layer that separates "built a demo" from "AI
engineer".

---

## Layer 5 · Retrieval and RAG

**Concepts:**
- Ingestion and parsing: PDFs, tables, OCR
- Chunking strategies
- Embedding models (MTEB leaderboard)
- Approximate nearest-neighbour indexes (HNSW) and the recall/latency trade-off
- **BM25 + dense hybrid search** merged with reciprocal rank fusion
- **Cross-encoder rerankers**
- Query rewriting and HyDE
- Metadata filters and access control
- Contextual retrieval
- Agentic RAG: retrieval as a tool the model calls
- GraphRAG (a niche technique)
- Trade-offs: RAG vs long context vs fine-tuning
- Citations and grounding

**You must be able to:**
- Build a synthetic question→chunk eval and measure recall@k and MRR.
- Tune chunking and hybrid weights against that eval.
- Add a reranker and measure how much it helps.
- Enforce per-tenant access in retrieval.
- Handle "the answer is not in the context" correctly.

**Common failures:**
- Embeddings-only search that misses exact terms such as SKUs and names.
- Bad parsing silently corrupting the index.
- Tuning generation before measuring retrieval.
- Stale indexes.
- Poisoned documents and cross-tenant leaks (OWASP LLM08).

**Depth: practical, plus information-retrieval basics** (precision, recall, MRR, nDCG).
Jason Liu's finding is worth remembering: on essays, full-text search matched embeddings and ran
about 10× faster. Measure before you reach for a vector database.

---

## Layer 6 · Agents, tools and MCP

**Concepts:**
- **The workflow-vs-agent spectrum.** Anthropic's patterns: augmented LLM, prompt chaining,
  routing, parallelisation, orchestrator-workers, evaluator-optimiser, autonomous agent.
- The ReAct tool loop. OpenAI's manager-vs-handoff orchestration.
- **Tool design** (the "agent-computer interface"):
  - namespacing
  - token-efficient outputs
  - "poka-yoke" tools that make misuse hard
  - error messages the model can act on
- Planning and reflection.
- Memory: short-term, episodic, semantic.
- Stopping criteria and loop detection.
- Human approval for high-risk actions.
- Durable, resumable execution with checkpoints.
- Sandboxed code execution.
- **Cost:** agents use about 4× the tokens of chat; multi-agent systems about 15×.
- **MCP** (the 2026-07-28 stateless spec): tools, resources and prompts, streamable HTTP,
  OAuth with client metadata documents. Agent skills. Computer use.

**You must be able to:**
- Write a tool loop from scratch.
- Build and secure an MCP server.
- Justify choosing a workflow or an agent.
- Make tool calls idempotent and safe to retry.
- Evaluate an agent on task success and pass^k.
- Cap an agent's steps and spend.

**Common failures** (from Huyen):
- Invalid tools or parameters.
- Goal failure.
- A false "done" from faulty self-reflection.
- Infinite loops.
- Runaway step counts and cost.
- Errors that compound across steps.
- Bloated tool sets with overlapping tools.
- Excessive agency (OWASP).

**Depth: deep and practical.** This is the fastest-growing area of demand. Learn one framework
well (LangGraph, Pydantic AI or the Vercel AI SDK), but be able to build the loop without one.

---

## Layer 7 · Production: cost, latency, caching, security

**Cost and latency:**
- Time to first token (TTFT) vs tokens per second
- Streaming
- Model routing and cascades: try a small model first
- Batch APIs, typically about 50% off
- **Provider prompt caching.** Anthropic reads cost about 0.1× the input price, writes 1.25×.
  The cache order is tools → system → messages, and any change invalidates everything after it.
- Semantic caching, used carefully: similar is not the same as identical
- Provider fallbacks
- Per-user token budgets
- Unbounded consumption (OWASP)

**Security:**
- Direct and indirect prompt injection.
- **Simon Willison's "lethal trifecta":** private data, untrusted content and an outbound channel
  in the same session lead to exfiltration.
- Hidden context and system prompt exposure.
- Improper output handling: model output is untrusted input, so never build `eval`, SQL or HTML
  from it unescaped.
- PII redaction.
- Least-privilege tool credentials and risk-tiered tools.
- Supply chain: models, packages and MCP servers.

**Guardrails and defensive UX:**
- Layered input and output classifiers
- Schema validation
- Relevance filters
- Human escalation
- Attribution, easy dismissal, honest expectation-setting

**You must be able to:**
- Build a per-feature cost model.
- Cut p95 latency with caching, routing and parallelism.
- Threat-model an agent against the OWASP LLM and Agentic Top 10.
- Design so that no session ever holds all three legs of the trifecta.

**Common failures:**
- Exploding reasoning-token bills.
- Cache misses caused by an unstable prompt prefix.
- "Ignore injected instructions" in the prompt as the only defence.
- Secrets in prompts.

**Depth: practical.** This is where a senior backend engineer's instincts transfer most
directly, so it's your biggest leverage point.

---

## Layer 8 · Model adaptation and serving, plus ML/DL foundations

**Concepts:**
- **When to fine-tune:** for style, format and distilling to lower latency or cost. Never to add
  knowledge.
- SFT, LoRA/QLoRA, DPO, and awareness of RL fine-tuning (GRPO).
- Dataset engineering: curation, deduplication, synthetic data.
- Distillation. Open-weight model families.
- **Inference mechanics:**
  - prefill vs decode
  - the KV cache and PagedAttention
  - continuous batching
  - speculative decoding
  - quantisation (FP8, INT4, GGUF, AWQ)
  - VRAM arithmetic: params × bytes per param + KV cache
- **Classical ML basics:**
  - train/validation/test splits
  - overfitting
  - precision, recall, F1, AUC
  - cross-entropy loss
  - gradient descent
- PyTorch basics (18–19% of postings).

**You must be able to:**
- Run one LoRA fine-tune, with an eval showing it beats prompting.
- Serve an open model with vLLM and benchmark it.
- Estimate VRAM for a given model and quantisation.
- Answer interview questions on all of the above.

**Common failures:**
- Fine-tuning to inject facts.
- Fine-tuning before you have evals.
- Catastrophic forgetting.
- Self-hosting without the volume to justify GPUs ("no GPUs before product-market fit").
- Quantising without measuring the quality loss.

**Depth: vocabulary and concepts, plus one hands-on project of each kind.** Going further,
e.g. Stanford CS336, is for inference-specialist or research-engineer tracks. Your MS will cover
the classical ML and statistics in depth. [ROADMAP.md](ROADMAP.md) phases 4–7 go beyond this
floor on purpose, because they aim at AI/ML depth rather than the minimum.

---

## ML vocabulary for interviews

One line each. If you can explain all of these out loud, the theory round holds no surprises.

| Term | Meaning |
|---|---|
| **Token / BPE** | Subword units made by merging frequent byte pairs. Models price, limit and "see" text in tokens |
| **Embedding** | A dense vector representing text. Semantic similarity ≈ cosine similarity |
| **Self-attention** | Each token takes a weighted mix of the others' values: `softmax(QKᵀ/√d)·V` |
| **Multi-head / GQA / MQA** | Parallel attention heads. Grouped- and multi-query variants share K/V across heads to shrink the KV cache |
| **RoPE** | Rotary positional encoding: rotates Q and K by position, which allows context extension |
| **Decoder-only / encoder / encoder-decoder** | GPT-style generation / BERT-style encoding (embeddings, classification) / T5-style, both |
| **Context window** | Maximum input plus output tokens per call. Quality degrades with length ("context rot", "lost in the middle") |
| **Temperature** | Scales logits before softmax. Lower is more deterministic |
| **Top-p / top-k** | Sample from the smallest set with cumulative probability ≥ p, or from the k most likely tokens |
| **Logprobs** | Log probabilities of tokens. Useful as a confidence signal, but poorly calibrated for correctness |
| **Perplexity** | exp(mean negative log-likelihood). A pretraining metric, not a product metric |
| **Cross-entropy** | The training loss for next-token prediction |
| **Pretraining → SFT → RLHF/DPO → RLVR** | Web-scale next-token learning → instruction tuning → preference optimisation → RL with verifiable rewards (how reasoning models are trained, e.g. GRPO) |
| **Reasoning model / test-time compute** | Spends extra "thinking" tokens before answering. Trades latency and cost for accuracy |
| **In-context learning** | Learning a task from examples in the prompt, with no weight update |
| **Chain of thought / self-consistency** | Eliciting intermediate reasoning; sampling several answers and majority-voting |
| **Hallucination** | Fluent but unsupported output. Reduced by grounding and checks, never eliminated |
| **PEFT / LoRA** | Train a small set of parameters. LoRA adds low-rank matrices A·B to frozen weights, often under 1% of parameters |
| **QLoRA** | LoRA on a 4-bit quantised base model, so large models fit on one GPU |
| **Quantisation** | Lower-precision weights or activations (FP8/INT8/INT4). Less memory and more speed, at some quality cost |
| **Distillation** | Training a small "student" model on a larger "teacher" model's outputs |
| **Mixture of experts** | A router activates a few expert networks per token. Many total parameters, low active compute |
| **KV cache** | Stored keys and values for past tokens so decoding doesn't recompute them. Grows with sequence length × batch size |
| **Prefill vs decode** | Prefill processes the prompt in parallel and is compute-bound (sets TTFT). Decode generates token by token and is memory-bandwidth-bound (sets tokens/s) |
| **PagedAttention / continuous batching** | vLLM's paged KV memory, plus scheduling that swaps finished requests out each step |
| **Speculative decoding** | A small draft model proposes tokens and the big model verifies them in one pass. Same output distribution, faster |
| **FlashAttention** | An IO-aware fused attention kernel that never materialises the N×N matrix |
| **Prompt caching** | The provider reuses computation for a repeated prompt prefix |
| **Scaling laws (Chinchilla)** | Loss falls predictably with parameters, data and compute. Compute-optimal is about 20 tokens per parameter |
| **HNSW / ANN** | Approximate nearest-neighbour search. Trades some recall for speed |
| **BM25 / hybrid / RRF** | Lexical ranking, combined with dense retrieval through reciprocal rank fusion |
| **Reranker (cross-encoder)** | Scores query–document pairs jointly. More accurate than embeddings, slower |
| **Recall@k / MRR / nDCG** | Share of relevant items in the top k / reciprocal rank of the first hit / graded ranking quality |
| **TPR / TNR** | True positive and true negative rates, used to validate LLM judges |
| **LLM-as-judge** | One LLM grading another's outputs. Must be validated against humans. Biased by position, length and self-preference |
| **pass@k vs pass^k** | At least one of k tries succeeds, vs all k tries succeed. The second is the agent reliability measure |
| **Tool / function calling** | The model emits schema-shaped calls and the host executes them |
| **Constrained decoding** | Forcing output to match a schema or grammar |
| **ReAct** | An interleaved loop: reason → act → observe |
| **MCP** | An open JSON-RPC protocol for hosts to reach servers that expose tools, resources and prompts. Stateless since 2026-07-28 |
| **Prompt injection** | Untrusted input or retrieved content that overrides instructions. OWASP LLM01 |
| **Overfitting / data leakage** | Classical ML hygiene. It applies just as much to eval sets and judge calibration |
