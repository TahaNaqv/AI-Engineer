# AI Engineer Roadmap — Fresh Graduate Edition

**For:** a fresh graduate (BS in CS, SE, or a related field) starting an MS in Data Science, who wants to become an AI Engineer
**Drafted:** 2026-10-09 · **Length:** about 20 months at 12–15 hrs/week of self-study on top of MS coursework (Oct 2026 → Jun 2028)
**Cost:** free. Every core resource below is free. Paid items are marked as optional.

---

## 1. The honest picture first

### The market you're entering (as of late 2026)

| Signal | What it means for you |
|---|---|
| Entry-level software developer employment is down about 20% from its 2024 peak (Stanford AI Index 2026). Young workers in AI-exposed jobs are about 19% below the expected trend (Stanford Digital Economy Lab, ADP payroll data). | The generic "junior developer" route is narrower. A degree plus tutorials is no longer enough. |
| The share of early-career job postings asking for AI skills **nearly doubled** in a year (Handshake, Apr 2026). NACE still projects Class-of-2026 hiring **up 5.6%**. | Entry-level jobs aren't disappearing. They're **shifting toward people who can build with AI**. |
| Hiring managers judge juniors on **3–5 deployed, well-documented projects with measured results**, not certificates. | Your portfolio and GitHub matter more than your GPA. |
| In Pakistan, AI fresher listings exist, mostly at startups and service companies in Islamabad, Lahore and Karachi. Pay is roughly PKR 35k–75k/month at fresher level, and many "fresher" postings still ask for about 1 year of experience. | Internships and freelance or open-source work *are* that "1 year of experience". Start early. |
| Industry **applied-scientist and research-engineer internships** often *require* being enrolled in a Master's or PhD. | Your MS gives you access to roles that BS graduates can't apply for. Use it. |

### What "AI Engineer" means here
You build **production software around AI models**: LLM apps, RAG systems, agents, classical ML models, plus the evals, deployment and monitoring they need. You understand the models well enough to choose, fine-tune and debug them. This is *not* an AI research scientist (that's a PhD route), and it's broader than prompt engineering.

### What separates a fresh grad who gets hired

| Typical fresh grad has | You need to add |
|---|---|
| Python from university assignments | Python you can **ship**: packages, tests, typing, APIs, Docker, Git workflow |
| ML theory from lectures | ML you've **applied** to messy real data, end to end, with metrics |
| Notebooks | **Deployed** apps with a URL, a README and a demo video |
| "I used ChatGPT's API once" | RAG, agents and, most importantly, **evals**: proving your AI system works, with numbers |
| A CV listing courses | A GitHub profile, a few write-ups, and an internship or real users |

---

## 2. How this roadmap works

**Three tracks run in parallel the whole time:**

1. **Main track (about 9–11 hrs/week):** the current phase below.
2. **Coding interview track (about 2 hrs/week):** DSA (data structures and algorithms) on LeetCode or NeetCode, easy to medium level. Pakistani companies and most large firms still screen freshers this way. Steady, not obsessive.
3. **Public work track (about 1–2 hrs/week):** push to GitHub, write a short post per project (LinkedIn, Medium or a personal blog), answer questions in communities. This is how recruiters find you.

**Use your MS, don't duplicate it.** When an MS course covers a topic (statistics, ML, data mining, big data), take the course seriously and use this roadmap for the *applied* half: implement it, ship it, put it on GitHub. Pick electives, assignments and especially your **thesis** so they feed your portfolio (see Phase 8).

**Every phase ends with the same three things:**
- **Build:** a project with acceptance criteria. No throwaway notebooks.
- **Explain:** write a short README or post explaining it as if to a classmate.
- **Checkpoint:** answer the interview-style questions listed, out loud, without notes.

**Rule for AI coding assistants (Copilot, Claude, Cursor):** use them, since employers expect it, but **write the from-scratch exercises by hand**. Interviews test whether *you* understand it, and a junior who can only prompt is the profile the market is cutting.

---

## 3. The roadmap

### Phase 0 — Setup & Habits · 2 weeks
- Set up a laptop for development: Linux or WSL2, VS Code, Git, `uv` for Python environments, Jupyter.
- Sign up for the free accounts: GitHub (**apply for the Student Developer Pack** with your university email for free Copilot and other tools), Kaggle (verify your phone to get free GPU), Hugging Face, Google AI Studio (free Gemini API key).
- Watch Karpathy's *Intro to Large Language Models* (1 hr) and *Deep Dive into LLMs like ChatGPT* (3.5 hrs) for the big picture.
- Read roadmap.sh/ai-engineer once, to see the whole landscape.
- Set up a **learning log**: one GitHub repo where you commit notes and code every week. The commit graph is your evidence of consistency.

---

### Phase 1 — Programming & Software Engineering Foundations · 8 weeks
*This is the most-skipped phase and the most common reason fresh grads fail technical interviews and take-homes.*

- **Python, properly:** functions, OOP, comprehensions, generators, typing, error handling, virtual environments, packaging, `pytest`.
- **Tooling:** the command line, Bash basics, Git branching, pull requests, merge conflicts (MIT *Missing Semester*).
- **SQL:** joins, group by, window functions, indexes. Postgres locally. Most AI jobs touch a database.
- **APIs:** HTTP, REST, JSON, async basics. Build APIs with **FastAPI**. Call other APIs with `httpx`.
- **Docker:** write a Dockerfile, use docker compose.
- **A small amount of frontend:** a Streamlit or Gradio UI is enough for now.
- **First taste of LLMs (week 7–8):** call the Gemini or Groq API (both have free tiers), stream responses, get structured JSON output.
- Resources:
  - CS50P (Harvard, free)
  - MIT Missing Semester
  - FastAPI official tutorial
  - SQLBolt and Mode's SQL tutorial
  - Corey Schafer's YouTube channel for Python topics

**Project:** a **"Study Buddy" API**: FastAPI + Postgres + Docker. It stores your notes and uses a free LLM API to make flashcards or quizzes from them. Include tests, a README and a Streamlit front end.
**Checkpoint:** explain what happens between typing a URL and getting a JSON response. Explain what a Docker image is vs. a container. Write a SQL query using a window function.

---

### Phase 2 — Math, Data & Classical Machine Learning · 10 weeks
*Runs alongside your first-semester MS courses. Lean on them for theory and use this phase for application.*

- **Math, applied rather than proof-heavy:**
  - linear algebra: vectors, matrices as transformations, dot products, eigenvectors, SVD/PCA
  - calculus: derivatives, the chain rule, gradients
  - probability and statistics: distributions, Bayes, expectation, MLE, hypothesis tests, confidence intervals
- **Data work:** NumPy, pandas, and then **Polars and DuckDB** (faster, increasingly common). Matplotlib and Seaborn. EDA (exploratory data analysis) and data cleaning.
- **The ML workflow:** problem framing, train/val/test splits, **data leakage**, cross-validation, bias/variance, regularization.
- **Algorithms**, each implemented once from scratch in NumPy and then used through scikit-learn:
  - linear and logistic regression with gradient descent
  - decision trees, random forests, **gradient boosting (XGBoost/LightGBM, still the best choice for tabular data)**
  - k-means, PCA
- **Metrics:** precision, recall, F1, ROC-AUC, confusion matrices, and choosing the metric that matches the business cost.
- Resources:
  - 3Blue1Brown (*Essence of Linear Algebra*, *Essence of Calculus*)
  - StatQuest for every ML algorithm
  - *Mathematics for Machine Learning* (free book)
  - *ISLP — Introduction to Statistical Learning with Python* (free book, excellent for an MS DS student)
  - Kaggle Learn (Intro + Intermediate ML, Pandas, Feature Engineering)
  - Google's ML Crash Course
  - CampusX *100 Days of ML* (Hindi/Urdu explanations)

**Project:** take **one Kaggle competition** end to end (tabular data, e.g. a Playground Series one): EDA → baseline → feature engineering → boosting → write-up. Then deploy the model behind your Phase 1 FastAPI skeleton.
**Checkpoint:** explain the bias/variance trade-off, why we need a validation set, precision vs. recall with a real example, and how gradient boosting works, to a non-expert.

> 🎯 **Internship milestone:** by the end of Phase 2 (about Mar 2027) you'll have 2 solid projects, which is enough to apply for **summer 2027 internships**. Big companies open applications in Sep–Jan, so apply to those *during* this phase with whatever you have. Local companies hire through Mar–May.

---

### Phase 3 — Deep Learning · 10 weeks
- **PyTorch fundamentals:** tensors, autograd, `nn.Module`, the training loop, datasets and dataloaders, using a GPU (free on Kaggle and Colab).
- **Neural nets from first principles:** forward/backward pass, activation functions, loss functions, optimizers (SGD, Adam), initialization, BatchNorm/LayerNorm, dropout, residual connections.
- **Karpathy's *Neural Networks: Zero to Hero*:** code along with micrograd → makemore → *Let's build GPT* → the tokenizer video. This is the most valuable free resource on this whole list.
- **CNNs** for images (enough to fine-tune a pretrained ResNet or ViT) and **sequence models**, as background for the next step.
- **Attention and transformers:** derive them yourself, then read *Attention Is All You Need*.
- **Embeddings:** what they represent and why similar meanings end up close together. This is the foundation of RAG in Phase 4.
- **Experiment tracking:** Weights & Biases (free for students) or MLflow.
- Resources:
  - fast.ai *Practical Deep Learning* (top-down; good if you learn by doing first)
  - MIT 6.S191 (lectures + Colab labs)
  - *Understanding Deep Learning* by Simon Prince (free book)
  - Umar Jamil's YouTube (transformers explained in code)
  - CampusX *100 Days of Deep Learning*
  - 3Blue1Brown's neural network series

**Project:** two parts.
1. Fine-tune a pretrained image or text model on a dataset you collected yourself (for example Urdu text classification or a local-domain image task), and publish it to Hugging Face with a **model card that includes evaluation numbers**.
2. Your own small GPT trained on a text corpus you choose, following Karpathy.

**Checkpoint:** explain backpropagation through a 2-layer network on paper. Why do transformers need positional information? What is overfitting, and list 4 ways to fight it.

---

### Phase 4 — LLM Application Engineering, RAG & Evals · 8 weeks
*This is the core of the AI Engineer job in 2026. It may run during your summer internship. If so, take on fewer side projects and spend that time on the internship.*

- **LLM fundamentals for builders:** tokens, context windows, temperature and sampling, why hallucinations happen, cost per token.
- **Working with providers:** Claude, OpenAI and Gemini APIs. Strict **structured outputs** (JSON schema). **Tool/function calling**. Streaming. Prompt caching. Multimodal input (PDFs, images).
- **Prompt and context engineering:** clear instructions, examples, deciding what goes into the context window and what stays out.
- **RAG, built properly:**
  - embeddings, chunking strategies
  - a vector DB: **pgvector** (you already know Postgres) or Qdrant
  - **hybrid search** (BM25 + vectors) **plus a reranker** as the baseline
  - metadata filtering
- **Evals (the skill that sets you apart):**
  - read your system's outputs first (error analysis)
  - build a **golden test set** (50–100+ cases)
  - code-based checks
  - **LLM-as-judge** checked against your own labels
  - retrieval metrics: recall@k, MRR
  - run the evals in CI so a change can't silently make things worse
- **Observability:** trace every LLM call with Langfuse (open source, has a free tier).
- Resources:
  - Hugging Face **LLM Course**
  - DeepLearning.AI short courses (free)
  - Anthropic's and OpenAI's official docs and cookbooks
  - DataTalksClub **LLM Zoomcamp** (free, project-based)
  - Microsoft *Generative AI for Beginners* (GitHub)
  - Hamel Husain's blog posts and evals FAQ (hamel.dev)
  - Chip Huyen's *AI Engineering* (paid book, optional, the best single book for this role; check your university library)

**Project — your flagship, version 1:** a **RAG assistant over a real document collection** that people actually use. For example: your university's course handbooks and regulations, Pakistani tax or legal documents, or a company's support docs. Deployed, with an eval report in the README (for example: "recall@5 went from 0.62 to 0.81 after adding hybrid search + reranking").
**Checkpoint:** walk through your RAG pipeline and say where it fails and how you measured that. When would you *not* use RAG?

---

### Phase 5 — Agents, MCP & AI Safety Basics · 6 weeks
- **The agent loop from scratch, with no framework:** the LLM decides → calls a tool → reads the result → repeats until done. Stop conditions, step limits, cost limits.
- **Tool design:** clear names and schemas, error messages the model can act on, idempotent actions.
- **Workflows vs. agents:** most production "agents" are mostly fixed workflows with a few LLM decisions. Learn to tell when you actually need autonomy.
- **Frameworks**, after you've built the loop yourself:
  - LangGraph or Pydantic AI (Python)
  - OpenAI Agents SDK or Claude Agent SDK
- **MCP (Model Context Protocol):** write your own MCP server. Use current docs (the spec changed in July 2026, so avoid older tutorials).
- **Human-in-the-loop:** require approval before any action that changes something.
- **Security basics:** the OWASP Top 10 for LLMs.
  - Prompt injection can't be fully prevented, so design for it: least-privilege tools, approvals, sandboxing.
  - Red-team your own agent with promptfoo (free, open source).
- **Agent evals:** task success rate and tool-call accuracy.
- Resources:
  - Anthropic's *Building Effective Agents* (essay)
  - Hugging Face **Agents Course** and **MCP Course**
  - Microsoft *AI Agents for Beginners* and *MCP for Beginners* (GitHub)
  - DeepLearning.AI agent short courses

**Project — flagship v2:** add an agent to your RAG assistant. It uses 2+ tools, including one MCP server you wrote, needs approval before any write action, has cost and step caps, and comes with an eval suite and a short red-team report.
**Checkpoint:** design a customer-support agent on a whiteboard. What tools does it need, what can go wrong, and how do you stop it from being tricked?

---

### Phase 6 — Deployment & MLOps · 6 weeks
- **Shipping:** Docker images, a cloud deploy (Render, Railway or Fly.io free tiers; AWS, GCP or Azure student credits), environment variables and secrets, CI with GitHub Actions.
- **Serving models:** FastAPI model servers, batching, latency vs. throughput, caching.
- **Open models locally:** Ollama or llama.cpp. Quantization at the intuition level (why a 4-bit model fits on your laptop). **vLLM** concepts, since it's the industry default for self-hosting.
- **MLOps:**
  - MLflow (experiment tracking + model registry)
  - versioning data and models
  - **monitoring:** latency, cost, errors, data drift
  - why models degrade in production
- **Cost thinking:** API vs. self-hosted, worked out with real numbers.
- Resources:
  - **Made With ML** (Goku Mohandas, free)
  - DataTalksClub **MLOps Zoomcamp** and **ML Zoomcamp**
  - Chip Huyen's *Designing ML Systems* (paid, optional; the lifecycle and monitoring chapters)

**Project:** make your flagship production-shaped: CI pipeline, monitoring dashboard, load test, a cost-per-request breakdown, and a 3–5 minute demo video.
**Checkpoint:** "Your model's accuracy dropped 10% in production. Walk me through how you'd investigate."

---

### Phase 7 — Fine-Tuning & Your Specialization · 8 weeks
*Go deeper in one direction. Choose based on your thesis, your interests and the jobs you're seeing.*

- **Core for everyone: fine-tuning basics.**
  - When to fine-tune: only after prompting and RAG have hit their limit. It's for format, tone, cost and narrow tasks, *not* for adding knowledge.
  - **LoRA/QLoRA** with Hugging Face TRL or **Unsloth** (fits on free Colab and Kaggle GPUs for small models).
  - Building a dataset, including synthetic data from a bigger model (distillation).
  - Evaluating the fine-tune against the base model with *your* eval suite.
  - Open models to try: Qwen and Gemma (small sizes).
- **Then choose one specialization track:**
  - **A. LLM/GenAI engineering (the most jobs):** deeper agents, multimodal, LLM internals (Raschka's *LLMs-from-scratch*, Stanford CS336 selected lectures).
  - **B. Data-heavy ML (fits an MS DS well):** recommender systems, time series, ranking, A/B testing, causal basics. Fits fintech, e-commerce and telco.
  - **C. Computer vision:** detection and segmentation (YOLO-style), vision-language models. Fits agritech, health and manufacturing.
  - **D. NLP for low-resource languages:** Urdu and Roman-Urdu. A real research gap, which makes a strong thesis and portfolio angle for Pakistan and the Gulf.
- Resources:
  - Hugging Face LLM Course (fine-tuning chapters)
  - Unsloth docs and notebooks
  - Maxime Labonne's *llm-course* (GitHub)
  - Sebastian Raschka's *LLMs-from-scratch* repo
  - Stanford CS224N (NLP) / CS231n (vision) / CS336 (LLMs) on Stanford Online YouTube

**Project — flagship v3:** fine-tune a small open model for one narrow task in your flagship and publish a **comparison table**: frontier API vs. your fine-tuned model on quality, cost and latency. Few fresh graduates have one of these, so it stands out.
**Checkpoint:** defend in writing whether your fine-tuned model should replace the API.

---

### Phase 8 — Thesis, Portfolio & Job Hunt · Jan → Jun 2028 (overlaps your final MS semester)
- **Thesis as a portfolio piece:**
  - Choose a topic in your specialization that produces something you can demo and measure.
  - Cold-email professors whose recent papers you've read, with a one-paragraph proposal.
  - Aim for at least a **workshop paper** or an arXiv preprint. It helps for research-engineer roles.
- **Portfolio polish:** 3–5 strong projects (flagship + Kaggle + fine-tune + 1–2 others). Each one has a live demo, a README covering problem → approach → results with numbers → trade-offs, and a short video.
- **CV:** one page. Projects with metrics come before coursework. Link GitHub, Hugging Face and your write-ups.
- **Interview preparation:**
  - DSA (keep the weekly habit going)
  - ML fundamentals Q&A (Chip Huyen's free *ML Interviews Book*)
  - from-scratch coding: implement linear regression, k-means, softmax, attention
  - LLM system design ("design a RAG chatbot for a bank": data, retrieval, evals, cost, security)
  - a deep-dive on one of your projects
  - take-home practice ("build a RAG app from this brief in 48 hours")
- **Where to apply:**
  - **Titles:** Junior AI Engineer, ML Engineer (Trainee/Associate), GenAI Developer, AI/ML Intern, Associate Data Scientist, Applied Scientist Intern (MS-only roles).
  - **Pakistan:** product companies and AI-focused startups. Use LinkedIn, Indeed PK and Rozee, and ask for referrals from alumni of your university.
  - **Remote:** US and EU startups (check that they hire outside the US), and UAE and KSA (strong AI hiring).
  - **Don't ignore adjacent entry points:** data analyst, AI QA/evals, AI annotator or trainer roles, and freelancing (Upwork) on AI automation. They count as experience.

---

## 4. Timeline at a glance

| Phase | Weeks | Approx. dates | Main output |
|---|---|---|---|
| 0 Setup & habits | 2 | Oct 2026 | Accounts, environment, learning-log repo |
| 1 Programming & SE | 8 | Late Oct – mid Dec 2026 | Study Buddy API (FastAPI + Postgres + Docker + LLM) |
| 2 Math + Classical ML | 10 | mid Dec 2026 – Mar 2027 | Kaggle competition + deployed model. **Internship applications go out** |
| 3 Deep Learning | 10 | Mar – mid May 2027 | Fine-tuned model on HF + your own small GPT |
| 4 LLM Apps, RAG, Evals | 8 | mid May – mid Jul 2027 (summer internship) | Flagship v1: RAG with an eval report |
| 5 Agents, MCP, Safety | 6 | mid Jul – Aug 2027 | Flagship v2: agent + MCP server + red-team report |
| 6 Deployment & MLOps | 6 | Sep – mid Oct 2027 | Production-shaped flagship + demo video |
| 7 Fine-tuning + Specialization | 8 | mid Oct – Dec 2027 | Flagship v3: API vs. fine-tuned comparison table |
| 8 Thesis + Job Hunt | ~24 | Jan – Jun 2028 | Thesis, polished portfolio, offers |

Leave a buffer around **midterms and finals**. Pause the main track during exam weeks and keep only the DSA habit going. This roadmap is sequenced by **milestones, not dates**: if a phase takes longer, stretch the dates rather than skip the project.

**When can you apply?** For internships, after Phase 2. For full-time "AI Engineer" roles, from Phase 5 onward. The later phases make you competitive for "ML Engineer" roles too.

---

## 5. Free resources

### YouTube channels

| Channel | Use it for |
|---|---|
| **Andrej Karpathy** | *Neural Networks: Zero to Hero*, *Deep Dive into LLMs*. The best free deep learning and LLM material available. |
| **3Blue1Brown** | Visual intuition for linear algebra, calculus, neural nets and transformers |
| **StatQuest with Josh Starmer** | Every statistics and ML algorithm explained simply. Use it when something doesn't click. |
| **Serrano.Academy** (Luis Serrano) | Friendly math-for-ML and transformer explanations |
| **Umar Jamil** | Transformers, LLaMA, diffusion and attention variants explained line by line in code |
| **Stanford Online** | Full university courses: CS229 (ML), CS224N (NLP), CS231n (vision), CS336 (LLMs from scratch) |
| **MIT 6.S191** (Alexander Amini) | A compact yearly intro to deep learning (introtodeeplearning.com) |
| **freeCodeCamp.org** | Long full-course videos: Python, SQL, PyTorch, ML, LLM apps |
| **Corey Schafer** | Clear Python fundamentals (Phase 1) |
| **Sebastian Raschka** | LLMs from scratch, fine-tuning, practical deep learning |
| **Welch Labs** | Beautiful explanations of how neural networks and AI actually work |
| **AI Engineer** (conference talks) | How practitioners build real AI systems: evals, agents, RAG in production |
| **Yannic Kilcher** | Paper walkthroughs, once you're reading research (Phase 7+) |
| **CampusX** *(Hindi/Urdu)* | *100 Days of ML*, *100 Days of Deep Learning*. Thorough, beginner-friendly. |
| **Codanics** *(Urdu)* | *Machine Learning ka Chilla* (40 days), math-for-DS crash course |
| **Krish Naik** *(Hindi/English)* | ML, DL and GenAI project tutorials, plus interview prep |

### Free courses & websites

| Resource | Phase | Notes |
|---|---|---|
| **roadmap.sh/ai-engineer** | 0 | An interactive map of the whole field |
| **CS50P** — cs50.harvard.edu/python | 1 | The best free Python course. Free certificate. |
| **MIT Missing Semester** — missing.csail.mit.edu | 1 | Shell, Git, editors, debugging: what universities forget to teach |
| **FastAPI tutorial** — fastapi.tiangolo.com | 1 | Official docs that work as a course |
| **SQLBolt** — sqlbolt.com | 1 | Interactive SQL |
| **Kaggle Learn** — kaggle.com/learn | 2 | Short hands-on micro-courses, nothing to install |
| **Google ML Crash Course** — developers.google.com/machine-learning/crash-course | 2 | A solid ML overview |
| **CS50 AI** — cs50.harvard.edu/ai | 2–3 | Search, probability, ML, neural nets, in Python |
| **Andrew Ng's ML Specialization** (Coursera) | 2 | Classic intro. Coursera has cut back free audit on many courses, so check whether "audit" is still offered. If not, apply for Coursera financial aid. |
| **fast.ai Practical Deep Learning** — course.fast.ai | 3 | Free, top-down, practical |
| **MIT 6.S191** — introtodeeplearning.com | 3 | Lectures + Colab labs |
| **Hugging Face Learn** — huggingface.co/learn | 4–7 | **LLM Course**, **Agents Course**, **MCP Course**, plus computer vision, audio and RL courses |
| **DeepLearning.AI short courses** — deeplearning.ai/short-courses | 4–5 | 1–2 hr courses on RAG, agents, evals, built with the companies that make the tools |
| **Microsoft "for Beginners" repos** — github.com/microsoft | 4–5 | *Generative AI for Beginners*, *AI Agents for Beginners*, *MCP for Beginners* |
| **Anthropic docs, courses and cookbook** — docs.claude.com, github.com/anthropics | 4–5 | Prompting, tool use, agents |
| **DataTalksClub Zoomcamps** — github.com/DataTalksClub | 4–6 | **LLM Zoomcamp**, **ML Zoomcamp**, **MLOps Zoomcamp**. Free, project-based, live cohorts with certificates. |
| **Made With ML** — madewithml.com | 6 | Production ML and MLOps, end to end |
| **Maxime Labonne's llm-course** — github.com/mlabonne/llm-course | 7 | A curated index of the LLM field with notebooks |
| **LLMs-from-scratch** — github.com/rasbt/LLMs-from-scratch | 7 | Raschka's code for building a GPT and fine-tuning it |
| **Hamel Husain's blog** — hamel.dev | 4+ | The best free writing on evals |
| **Chip Huyen's ML Interviews Book** — huyenchip.com/ml-interviews-book | 8 | 200+ ML interview questions. Free. Written in 2021, so add LLM topics yourself. |

### Free books (legally free online)

- ***Mathematics for Machine Learning*** (Deisenroth et al.) — mml-book.github.io
- ***ISLP: An Introduction to Statistical Learning with Python*** — statlearning.com (ideal for an MS DS student)
- ***Understanding Deep Learning*** (Simon Prince) — udlbook.github.io/udlbook
- ***Speech and Language Processing*** (Jurafsky & Martin, 3rd ed. draft) — web.stanford.edu/~jurafsky/slp3
- ***Dive into Deep Learning*** — d2l.ai (optional, as a reference)
- **Worth buying or borrowing later:** Chip Huyen's *AI Engineering* and *Designing ML Systems*. Géron's *Hands-On ML with Scikit-Learn and PyTorch* (2025 PyTorch edition, not the older TensorFlow one).

### Practice platforms

- **Kaggle:** competitions, datasets, notebooks. Use the Playground Series for low-pressure practice.
- **LeetCode / NeetCode (neetcode.io):** DSA. Use the NeetCode 150 list.
- **Deep-ML (deep-ml.com):** LeetCode-style problems for ML math and implementations.
- **Hugging Face Spaces:** host Gradio and Streamlit demos for free.

### Free compute & credits

| What | Notes |
|---|---|
| **Kaggle notebooks** | Free T4/P100 GPU, around 30 hrs/week (the quota varies; check your account settings), 12-hour sessions |
| **Google Colab (free)** | T4 GPU when available, with dynamic limits. Good for short experiments. |
| **GitHub Student Developer Pack** — education.github.com/pack | Free Copilot Student, cloud credits, JetBrains IDEs and 100+ tools, with a university email |
| **Free LLM APIs** | **Gemini API** (Flash models, free tier, no card), **Groq** (fast open models), **OpenRouter** `:free` models, **GitHub Models**. Free tiers may train on your prompts, so don't send private data. |
| **Ollama** | Run open models on your own laptop, offline and free |
| **Cloud student credits** | Azure for Students, AWS Educate, Google Cloud education credits (check what your university offers) |
| **W&B / MLflow** | W&B is free for academic use. MLflow is open source. |

### Pakistan-specific

- **Google × Government of Pakistan (MoU, Aug 2026):** free one-year Google AI Plus / Gemini access for students, Google Career Certificates scholarships, and the *AI Seekho 2026* initiative. Watch official announcements and your university for enrollment.
- **NAVTTC "Skills of Tomorrow"** (nsis.navttc.gov.pk): free, government-certified AI courses in batches. The June 2026 intake has closed, so watch for the next one.
- **NAVTTC–NETSOL scholarships:** fully funded AI, data science and cybersecurity training (check whether intake is open).
- **Communities:** your university's ACM/IEEE/GDG chapter, GDG Islamabad/Lahore/Karachi events, Kaggle Days and hackathons. The DataTalksClub Slack and Hugging Face Discord are global and free.

---

## 6. Mistakes to avoid

- **Tutorial hell:** watching more than you build. Rule: every week has a commit.
- **Collecting certificates:** hiring managers barely look at them. A deployed project beats ten certificates.
- **Skipping Phase 1** because "AI writes the code now". Take-homes and interviews show it quickly.
- **Projects that only call LangChain:** a chatbot tutorial copied from YouTube shows nothing. Show *your* decisions, *your* data and *your* eval numbers.
- **Paying for bootcamps early:** everything you need to start is free. Pay only for a specific gap, and only after Phase 4.
- **Learning outdated tools:** avoid the OpenAI Assistants API (shut down Aug 2026), TGI (archived), MCP tutorials from before July 2026, and Llama-only tutorials (Qwen and Gemma are the common open defaults now).
- **Applying too late:** big-company internship windows open about 6–9 months before summer. Note the dates in Sep.
- **Studying alone in silence:** post your projects. Recruiters search LinkedIn and GitHub, and opportunities come from people who've seen your work.

**What to expect to change:** model names, prices, free-tier limits and framework versions go out of date within months. Re-check them every semester. The fundamentals (Python, ML, deep learning, evals, deployment) won't change.

---

## 7. Research this roadmap is based on (Oct 2026)

- **Market:**
  - Stanford AI Index 2026 (via Pin's tech job market report)
  - Stanford Digital Economy Lab (ADP payroll study)
  - CNBC / Handshake on AI skills in entry-level postings (Apr 2026)
  - NACE Job Outlook 2026
  - Indeed PK, Glassdoor and Bayt listings for Pakistan AI fresher roles (Sep–Oct 2026)
- **Hiring and portfolio guidance:** letsdatascience.com, dataexpert.io and InterviewQuery portfolio guides (2026). The research-vs-engineering internship process guide on techinterview.org.
- **Roadmaps compared:** roadmap.sh AI Engineer, Scrimba, Codebasics, Futurense, and the companion experienced-engineer roadmap in this folder (ROADMAP.md).
- **Resources checked:**
  - Hugging Face Learn
  - fast.ai
  - MIT 6.S191 (2026 edition)
  - Stanford Online playlists
  - CS50 (2026)
  - DataTalksClub
  - Microsoft "for Beginners" repos
  - CampusX, Codanics
  - Chip Huyen's ML Interviews Book
- **Free tiers:** Kaggle and Colab GPU reports (Sep 2026), GitHub Education Copilot Student changes (Jun 2026), OpenRouter / KDnuggets free LLM API comparisons (2026).
- **Pakistan programs:** Express Tribune and ARY on the Google–Pakistan MoU (Aug–Sep 2026), NAVTTC and DUHS notices.
- **Could not verify:**
  - Coursera's exact 2026 audit policy (sources conflict)
  - DataTalksClub 2026–27 cohort dates
  - current DigiSkills/PIAIC offerings
  - exact Kaggle/Colab GPU quotas (not officially published)
  - reliable Pakistan salary data (only job-board ranges)
