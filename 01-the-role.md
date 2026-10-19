# 01 · What the role actually is

The title was coined in June 2023 by Shawn "swyx" Wang in *The Rise of the AI Engineer*,
arguing that work which used to need a research team and five years could now be done
with API docs and an afternoon. Three years on, that essay's prediction has hardened into
a job family with its own conference circuit, its own tooling, and its own interview loop.

The cleanest working definition, derived from job descriptions rather than opinion:

> **An engineer who owns the design, evaluation and production operation of systems built
> on foundation models.**

Every clause matters. *Owns* — not prototypes. *Evaluation* — the part that distinguishes
the role. *Foundation models* — someone else trained them.

---

## Three sub-populations hide under one title

| Bucket | Share | What the work looks like |
|---|---|---|
| **AI-first** | ~70% | Direct work on LLM systems: RAG pipelines, agents, prompt/context design, evals, shipping to production |
| **AI-support** | 24–28% | Platform and infrastructure: gateways, deployment tooling, data pipelines, GPU serving, internal AI platforms |
| **Rebranded ML** | 2–5% | Classical ML, computer vision, model training wearing an "AI Engineer" title. Read these postings carefully |

Two snapshots of postings from the same author agree on this split to within a few points.
The first is 889 postings from January 2026. The second is 6,964 postings from February to
August 2026, about 38% of them from India. The AI-first share held between 68% and 71% in every
monthly scrape. See [02-market-data.md](02-market-data.md) for how to read the two snapshots.

---

## How it differs from adjacent roles

| Role | Owns | Core artefact | Typical failure they debug |
|---|---|---|---|
| **AI engineer** | Systems on top of models | A pipeline + an eval suite | Agent breaks on step 4; retrieval returns the wrong chunk |
| **ML engineer** | Trained models in production | A training pipeline | Feature drift; recall dropped after retrain |
| **Research scientist** | New methods | A paper or a model | Loss curve; ablation didn't reproduce |
| **MLOps / platform** | The substrate others build on | Infra + CI/CD + serving | Throughput, cost, GPU utilisation |
| **Data engineer** | Data movement and quality | Pipelines and warehouses | Late partition, schema break |

The hiring data reflects the split. Among AI-first postings, the share asking for integrator
skills rose from 80% to 88% between February and August 2026, while the share asking for
training skills fell from 37.5% to 30.4%. LinkedIn ranks AI Engineer as the fastest-growing
US job for 2026. A commonly repeated figure of "+74% for AI engineers vs +33% for ML
engineers" has no primary source. It appears to be a garbled version of LinkedIn's 2020
Emerging Jobs report, so this dossier doesn't use it.

---

## What a day looks like

Practitioner accounts converge on something reassuringly ordinary. Standup, pull requests,
code review, ticket triage, integration work. The AI-specific slice is:

- Writing and versioning the prompts that shape behaviour
- Building a retrieval pipeline over internal documents
- Reading production traces to work out why an agent completes steps 1–3 and fails step 4
- Adding an output check that catches bad answers before users see them
- Arguing with product about whether a 4% quality gain justifies a 3× cost increase

> **The mental shift.** Full-stack work is deterministic: given input X, assert output Y.
> AI engineering is statistical: given a distribution of inputs, the system passes 92% of a
> golden set, and your job is to find out what lives in the other 8% and whether it matters.
> "It works" stops being a binary. Everything else in this dossier follows from that one change.

---

## Your starting position as a full-stack engineer

Grigorev's field guide estimates transition timelines by origin role: ML engineer is
easiest, data engineer 3–4 months, and **backend engineer 2–3 months** — the shortest
non-ML path, because it is "add AI on top of engineering" rather than "learn engineering
and AI". A full-stack engineer sits in that bucket with a frontend bonus.

### Transfers directly

- API design, versioning, error contracts
- Async, streaming, SSE/WebSockets — the exact primitives LLM responses need
- Postgres, indexing, query planning → **pgvector is the default vector store**
- Docker, CI/CD, cloud deploys (40% of postings name AWS)
- Queues, retries, idempotency, backpressure — agent orchestration is distributed systems wearing a hat
- Observability instincts: logs, traces, p95s
- Auth, tenancy, PII handling — now a security-critical surface
- TypeScript/React for chat UIs, token streaming, generated-content rendering
- Product judgement about what is worth building

### Genuine gaps to close

- **Python at production fluency** — not "I can read it". Type hints, async, packaging, FastAPI, pytest
- **Evaluation as a discipline** — the single biggest gap, and the biggest hiring signal
- **Non-determinism** — designing when `assertEqual` no longer applies
- **Embeddings and retrieval intuition** — why a query missed, and which of six knobs to turn
- **Token/latency/cost economics** as a first-class design constraint
- **Context engineering** — deciding what the model sees on every call
- **Enough ML vocabulary** to pass interviews: attention, tokenisation, temperature, perplexity, LoRA
- **Adversarial thinking about text** — every retrieved document is untrusted input

---

## How much maths do you need?

This is a live debate and the answer depends on which track you choose. For the applied
AI-engineer track that ~95% of postings describe: **very little.** You need to understand
what a vector similarity is, what temperature does to a distribution, and why a 4-bit
quantised model loses some quality — conceptual, not derivational.

Linear algebra and calculus become genuinely necessary only if you move into fine-tuning
at depth, inference optimisation, or research.

Do not let a maths prerequisite become your procrastination structure; it is the most
common way people spend six months and ship nothing.
