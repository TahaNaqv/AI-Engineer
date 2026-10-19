# 02 · Market data

What the job postings ask for, what employers are building, how big the market is, and what
it pays. Everything here was re-checked on 19 October 2026. Every number names its corpus and
date, because one well-known source has two snapshots that disagree with each other.

---

## How to read these numbers

Most AI-engineer skill statistics trace back to **one author, Alexey Grigorev** (AI Shipping
Labs). He published **two separate snapshots**. Quoting a number without saying which snapshot
it came from is the most common error in this field, and earlier drafts of this dossier made it
too.

| Snapshot | Size | Window | Source |
|---|---|---|---|
| **v1** | 889 unique postings | Built In, January 2026: Berlin, Amsterdam, London, LA, NY | AI Shipping Labs blog, 4 Mar 2026 |
| **v2** | 6,964 postings from 2,499 companies | Built In, 8 monthly scrapes, Feb–Aug 2026, **India added** | *AI Engineering Field Guide* (GitHub). Code and data are public |

Four caveats on v2:

- **About 38% of v2 is Indian postings.** Approximate breakdown: US 3,014, India 2,646, UK 646,
  Germany 244, Netherlands 92.
- **Built In skews toward tech-forward employers.**
- **Skill shares are a floor, not an estimate.** A posting counts for a skill only if the text
  names it.
- Grigorev used an LLM to extract the skills (a fixed prompt). Some figures in the same document
  disagree slightly with each other, e.g. RAG at 53.9% vs 54.8% of AI-first roles.

> **Reliability rule for this chapter.** Skill frequencies from large corpora are reliable.
> Volume trends from the Indeed and Lightcast trackers are reliable. Salary data from Levels.fyi
> is reliable for big-tech-style employers and thin everywhere else. Anything from recruiter or
> course-seller content is marked as low reliability.

---

## The role mix

| | v1 (Jan 2026) | v2 (Feb–Aug 2026) |
|---|---|---|
| AI-first: building LLM systems directly | ~70% | **70.0%** |
| AI-support: platform, infra, data, tooling | ~28.5% | **24.2%** |
| Rebranded classical ML | <2% | **4.9%** |
| Applied / production (vs research) | 95.6% | **97.1%** |

The AI-first share stayed between 68% and 71% in every monthly scrape. **86.8% of postings ask
for skills beyond GenAI**, 60.2% for backend skills and 30.7% for frontend skills. The job is
full-stack whether or not the title says so.

---

## Skill frequencies

| Skill | v2 (all) | v2 (AI-first) | v1 |
|---|---|---|---|
| Python | **70.8%** | 75.6% | 82.5% |
| TypeScript | **19.3%** | 20.5% | 23.4% |
| Java / SQL / Go / JavaScript | 17.7 / 14.4 / 11.5 / 11.6% | – | – |
| AWS / Azure / GCP | **40.3 / 29.6 / 27.4%** | 45.2% (AWS) | 40.1 / 23.9 / 23.0% |
| Any agent skill | 55.4% | **71.6%** | 14.4% |
| RAG | **39.8%** | ~54% | 35.9% |
| Prompt engineering | 34.7% | 46.5% | 29.1% |
| Evaluation-related (any) | – | **59.7%** | 4.5% |
| — LLM evaluation specifically | – | 30.9% | – |
| — Guardrails | 10.2% → 15.2% | 17.9% | – |
| CI/CD / Docker / Kubernetes | 36.8 / 24.4 / 24.0% | – | 29.3 / 31.0 / 29.1% |
| Vector DBs (generic) / PostgreSQL / Pinecone | ~23.6 / 11.1 / 7.3% | – | 10.8 / 9.3 / 5.9% |
| LangChain / LangGraph / LlamaIndex | 22.0 / 13.8 / 8.3% | – | 18.8 / 8.0 / 5.8% |
| CrewAI / AutoGen / DSPy | 6.7 / 5.3 / 0.8% | – | – |
| OpenAI API / Anthropic API | 15.2 / 14.4% | – | 8.7 / 5.5% |
| **MCP** | **14.1%** (9.9% Feb → 17.6% Aug) | – | not tracked |
| PyTorch | 18.2% | 19.5% | 22.0% |
| Fine-tuning | see below | 24.8% (tagged) | 8.5% |
| AI coding tools (Claude Code, Cursor, Copilot) | 3.5% → 8.9% | 11.1% | – |

**About fine-tuning.** It is mentioned somewhere in 27.3% of v2 postings and tagged as a skill in
24.8% of AI-first roles. It is the **primary responsibility in only 3.6%**, and 84.6% of postings
never list it as a responsibility. The accurate summary is *mentioned in 15–27%, core to under 5%*.

### Other corpora

| Source | Sample | Headline | Reliability |
|---|---|---|---|
| 365 Data Science, Apr 2026 | 903 Glassdoor US postings | Python 71%, PyTorch 37.7%, TensorFlow 32.9%, fine-tuning 14.8%, RAG 13.6%. More ML-heavy mix | Medium: internal inconsistencies |
| agentic-engineering-jobs.com | 1,135 listings, Mar–May 2026 | LangChain 34.5%, LangGraph ~22.6%, MCP in 17–24% of framework postings, Python 91–96% | Medium–low: a job board analysing its own listings |
| Axial Search, updated 13 Oct 2026 | 43,480 US postings | Python 62%, cloud 55%, foundation models 51% | Medium |
| Lightcast, via Stanford AI Index 2026 | All US postings | AI skills in 2.5% of all US postings in 2025 (+55% YoY). Agentic-AI skills 0.06% → 0.23% | High |
| Dice, Jul 2026 | 7M US tech postings | AI skills in **73%** of tech postings, up from 15% in Jan 2024. AI-titled postings +173% YoY (Q1 2026) | Medium: vendor report |

---

## What is rising and what is falling

v2 trends between February and August 2026, all within the same corpus:

| Signal | Feb → Aug |
|---|---|
| Integrator stack (building on APIs) within AI-first | 80.0% → **88.0%** |
| Trainer stack (training models) within AI-first | 37.5% → 30.4% |
| Postings asking for **both** RAG and agents | 33.1% → **50.5%** |
| LangGraph | 7.4% → 17.2% |
| MCP | 9.9% → 17.6% |
| Function calling | 9.6% → 14.3% |
| PyTorch | 20.8% → 15.3% |
| Fine-tuning | 17.1% → 12.7% |
| Inference/serving work | 19.8% → 9.9% |
| AI coding tools | 3.5% → 8.9% |

Across postings, responsibilities moved the same way between February and June: agents +13.1pp,
security +9.4pp, monitoring +9.0pp, fine-tuning −3.4pp, research −13.1pp.

> **The direction is unambiguous.** Employers want people who integrate, evaluate, secure and
> operate model-based systems. Fewer of them want people who train models. Both kinds of work
> exist, but the first is where the hiring volume is.

---

## What companies are actually building

These are use cases from v2: 24,502 use-case mentions across 4,894 postings, Feb–Jun 2026. The
categories overlap.

| Use case | % of postings | Trend |
|---|---|---|
| Automating manual workflows | 69.0% | ↑ (62 → 73) |
| Internal operations: risk, compliance, fraud, claims, revops | 60.6% | ↑ |
| Agentic systems | 49.4% | ↑ |
| Finding information in company data (RAG/search) | 43.8% | ↑ (39 → 49) |
| Decisions from data / analytics | 43.0% | – |
| Customer support / Q&A at scale | 36.4% | ↓ (40 → 32) |
| Content generation | 33.4% | – |
| AI quality and safety | 20.0% | – |
| Personalisation | 12.0% | ↓ (18 → 9) |
| Developer / coding tools | 9.5% | – |
| Fine-tuned domain models | 5.0% | – |

**Internal automation is ahead of customer-facing chat.** Coding tools are a niche for
employers, even though developers use them every day.

### Who hires

- **Industries mentioned in v2:** finance 9.5%, healthcare 7.3%, legal/regulatory 4.5%,
  cybersecurity 4.2%.
- **The biggest hirers are banks and insurers, not AI labs:** Capital One (120 postings), Citi
  (98), Optum (90), NVIDIA (63), Thomson Reuters (49), Wells Fargo (43), JPMorgan (34),
  OpenAI (29). No employer accounts for more than 1.7% of the corpus.
- **Dice:** finance and banking tech postings are up 47% YoY, against 23% for tech overall.
- **CyberSN:** *AI Security Engineer* postings are up **268%** (Jan–Sep 2026), while overall US
  cybersecurity postings fell 26%.

### Company size

| Employees | Share of v2 postings that state a size (n=5,431) |
|---|---|
| < 200 | 24.9% |
| 200–999 | 19.5% |
| 1,000–9,999 | 22.7% |
| 10,000+ | 32.9% |

Axial puts 10,000+ employers at **47%** of US AI-engineering postings. Seed and Series A
companies over-index on AI-first work and fine-tuning. Public companies over-index on RAG.

### Forward-deployed engineers

In v2, live forward-deployed engineer (FDE) listings grew from 28 to 118 between February and
July, a 4.2× increase. Their share peaked at 4.4% and eased to 2.9% in August. 89% are
customer-facing. Recruiter sources relaying Lightcast data report more than 7,300 US FDE
postings in the first nine months of 2026. That figure is not verified.

---

## Volume and trends through Q3 2026

| Indicator | Figure | Reliability |
|---|---|---|
| Indeed: share of US postings mentioning AI | 3.71% (Sep 2025) → 4.77% (Jan 2026) → **7.34% (30 Sep 2026)**, roughly double in a year | High: keyword-based, so it measures AI *mentions*, not AI roles |
| Same metric, 30 Sep 2026 | UK **9.92%**, Germany 5.74%, Australia 7.12% | High |
| US software-developer postings | **+~15%** since Feb 2025 while all postings fell 7%. Still **27.5% below** Feb 2020 | High (Indeed Hiring Lab, Jul 2026) |
| Where that recovery came from | **71% senior roles**; 37% AI-titled roles | High |
| US AI-engineering weekly volume | ~1,550/week on average. Low ~927 (early March), peak **2,327 (late June)** | Medium (Axial) |
| Live dev and data listings, 16 Oct 2026 | 16.7% have an AI/ML title. US 19.9%, UK 20.4%, **UAE 24.4%**, India 13.5% | Medium (JobRise) |

### Remote work: smaller than it looks

| Source | What it measures | Remote share |
|---|---|---|
| Axial | Postings that state a work model | 32% remote, 48% hybrid |
| LinkedIn *Jobs on the Rise* | Member job starts | 26% remote, 27% hybrid |
| JobRise | All sources | 30.6% |
| JobRise | **Employer career sites only** | **8.4%** |
| 365 Data Science | Glassdoor US | 5.9% fully remote |

78% of "remote" listings come from remote-only job boards. When companies post on their own
career sites, about 1 in 12 roles is remote. Many of those are open to US residents only. Chapter
06 covers how to find the ones that aren't.

### Seniority and the entry-level squeeze

| Level (v2) | Feb | Aug |
|---|---|---|
| Junior / entry | 1.5% | **1.2%** |
| Mid | 43.9% | 48.4% |
| Senior | 30.8% | 30.3% |
| Lead | 4.6% | 8.1% |
| Staff+ | 18.5% | 11.0% |

- **365 Data Science:** 0–2 years of experience is 2.5% of all postings. Only a third of
  postings state experience at all.
- **LinkedIn:** the median AI engineer had **3.7 years** of prior experience.
- **Stanford Digital Economy Lab ("Canaries", Aug 2026 revision, ADP payroll data):**
  employment of 22–25-year-olds in the most AI-exposed occupations is **19% below**
  counterfactual. Experienced workers show no comparable gap. The effect comes from reduced
  hiring, not layoffs.
- **Pakistan:** press reports of P@SHA findings put entry-level hiring at major tech firms down
  ~25%. Entry-level freelance listings fell from ~15% to under 9%. Medium reliability.

> **For an engineer with 4+ years of experience, this is good news.** The squeeze hits people
> who have never shipped anything. You sit in the 2–6-year band that most postings target.

---

## Compensation

Salary data is the softest data in this dossier. Use the levels below as directional.

### United States

| Source | Figure | Reliability |
|---|---|---|
| Levels.fyi, ML/AI software engineer (n=5,937, 19 Oct 2026) | **Median TC $250k.** P25 $170k, P75 $370k, P90 $510k | High; skews to big tech |
| Axial, top of posted range (43k postings) | Junior $170k, mid $200k, senior $213k, principal $270k. Overall median $176k. Finance $240k | Medium; top-of-band overstates offers |
| 365 Data Science (Glassdoor) | Average ~$206k. 0–1 yr $143k, 4–6 yrs $199k, 10+ yrs $269k | Medium |
| Agentic-role postings | Median ~$213k (n=428) | Medium–low |

**Frontier labs** (Levels.fyi, equity-heavy, private valuations):

| Lab | Median TC | Range by level |
|---|---|---|
| Anthropic | ~$880k | SWE $482k → Staff $1.41M |
| OpenAI | ~$875k | L3 $346k → L6 $1.28M |

### UK, Europe, Gulf, India

Levels.fyi, ML/AI software engineer, total compensation, 19 Oct 2026:

| Market | Median | P25–P75 | n | Reliability |
|---|---|---|---|---|
| UK | **£104k** | £70k–£148k | 500 | High |
| Germany | **€88k** | €70k–€112k | 316 | High |
| UAE | **AED 360k** (~$98k, tax-free) | AED 240k–470k | 32 | Medium |
| Saudi Arabia | SAR 144k | SAR 96k–396k | 12 | Low: sample too small |
| India | **₹28.2 lakh** | ₹14.3L–₹49.3L | 1,348 | High |

Gulf ranges published by blogs are usually higher than these, e.g. AED 40–65k/month for seniors.
Those blogs cite Hays and Cooper Fitch reports that could not be checked. Treat them as asking
prices, not medians.

### Pakistan: local salaries

| Source | Figure | Reliability |
|---|---|---|
| Levels.fyi, ML/AI SWE, Pakistan (n=16) | Median PKR 1.56M/yr (~130k/mo); P90 PKR 5.35M | Medium–low: tiny sample |
| Levels.fyi, all SWE, Pakistan (n=135) | Median **PKR 3.25M/yr** (~271k/mo); **Islamabad median PKR 2.95M**; P90 7.59M | Medium–high; skews to top employers |
| Indeed PK, ML Engineer (n=34) | Average Rs 193k/mo; **Islamabad Rs 296k/mo**, Lahore 144k | Medium |
| Glassdoor PK (snippets) | AI Engineer, Lahore median ~PKR 117k/mo (n=43) | Medium–low |
| Real Islamabad postings, mid-2026 | AI/LLM backend engineer, 2+ yrs: **PKR 150–400k/mo** | Medium: real offers, anecdotal |
| Course-seller guides | "PKR 300k–1.5M/mo" | Low: ignore the upper bound |

No public P@SHA salary survey for 2025–26 could be found.

**Triangulated bands for Islamabad and Lahore.** These are an estimate built from the sources
above, not a published figure:

| Level | PKR / month |
|---|---|
| Junior (0–2 yrs) | 80k–200k |
| Mid (3–5 yrs) | 200k–450k |
| Senior / lead (top product or export firms) | 450k–900k+ |

### Pakistan: remote, for foreign employers

There is no high-quality data. The best available framing:

- Contractor or EOR roles at US/EU startups typically pay **$3–7k/month** for mid-to-senior
  engineers.
- Direct senior contracts can reach $8–12k+.
- Vendor rate cards: mid $25–40/h, senior $35–50/h, principal $50–80/h. Agencies mark these up
  50–100%.

All of this is medium-to-low reliability. Remote USD roles are widely reported at **3–5× local
pay**.

Context: Pakistan's IT and IT-enabled services exports reached **$4.6B in FY2025-26 (+21%)**, of
which about $1.6B came from freelancers. The PKR/USD conversions here assume about 280 and should
be checked against current State Bank figures.

---

## Corrections to earlier claims

| Earlier claim | Status | Use instead |
|---|---|---|
| 95.6% of postings are production roles | Outdated (v1, Jan 2026) | **97.1%** (v2, Feb–Aug 2026) |
| RAG in 36–40% | Correct | 35.9% (v1), 39.8% (v2), ~54% of AI-first roles |
| Fine-tuning in only 8.5% | Misleading | **Mentioned in 15–27%; core to under 5%** |
| Python 71–83% | Correct | 70.8% (v2), 82.5% (v1) |
| TypeScript 19–23% | Correct | 19.3% (v2), 23.4% (v1) |
| ~2.5% target 0–2 years | Correct | 2.5% (365DS); 1.2% junior in v2 by August |
| Demand outruns supply ~3:1 | **No primary source** | Drop it. A recruiter estimate with conflicting attributions |
| AI-engineer postings +74% vs ML-engineer +33% | **Unsupported; likely a garbled LinkedIn 2020 statistic** | LinkedIn ranks AI Engineer #1 in the US for 2026; Dice: AI-titled postings +173% YoY |
| Agentic workflows make 50–200 calls per task | **No source** | Typical pipelines make ~5 LLM calls per request; coding agents run 20–50+ steps |
| AWS in 40% | Correct | 40.3% (v2) |
| Two independent corpora agree | **Incorrect** | Same author, two snapshots |

---

## What this means for you

1. **Your background matches the market.** Python is required. TypeScript is the strong second
   language. The job is full-stack in 87% of postings. CI/CD, Docker and cloud appear in a third
   or more.
2. **The gaps to close are evals, agents and MCP.** Evaluation appears in 60% of AI-first roles.
   Postings asking for both RAG and agents are now at 50%. MCP doubled in six months.
3. **Treat fine-tuning and training as depth, not a door.** They are worth learning (the
   roadmap does), but very few roles are built around them.
4. **Target finance, healthcare, legal and enterprise operations, and look at Gulf markets.**
   That is where volume is growing. The UAE has the highest share of AI-titled listings measured.
5. **Remote is a small, contested slice.** Chapter 06 covers how to compete for it from Pakistan.
