# The Story of LLMs and Agents
### *From word vectors to autonomous agents — a readable journey through the ideas that shaped modern AI*

> *A narrative guide to understanding how we got from "computers that can't tell a noun from a verb" to "AI agents that run science experiments for weeks." Written for engineers who want the concepts — not just the jargon.*

---

## 📖 Table of Contents

- [Prologue — Why This Story Matters](#prologue--why-this-story-matters)
- [Chapter 1 — The World Before Transformers](#chapter-1--the-world-before-transformers)
- [Chapter 2 — Attention Is All You Need (2017)](#chapter-2--attention-is-all-you-need-2017)
- [Chapter 3 — The Pre-training Revolution (2018–2019)](#chapter-3--the-pre-training-revolution-20182019)
- [Chapter 4 — The Scale Awakening (2020)](#chapter-4--the-scale-awakening-2020)
- [Chapter 5 — Making AI Helpful: RLHF and ChatGPT (2022)](#chapter-5--making-ai-helpful-rlhf-and-chatgpt-2022)
- [Chapter 6 — The Cambrian Explosion (2023)](#chapter-6--the-cambrian-explosion-2023)
- [Chapter 7 — From Chatbots to Agents](#chapter-7--from-chatbots-to-agents)
- [Chapter 8 — The Knowledge Problem: RAG & Vector Search](#chapter-8--the-knowledge-problem-rag--vector-search)
- [Chapter 9 — Reasoning Models & Test-Time Compute (2024–2025)](#chapter-9--reasoning-models--test-time-compute-20242025)
- [Chapter 10 — The Agent Era Begins (2025)](#chapter-10--the-agent-era-begins-2025)
- [Chapter 11 — MCP and the Standardization Wave](#chapter-11--mcp-and-the-standardization-wave)
- [Chapter 12 — Where We Are Now (2026)](#chapter-12--where-we-are-now-2026)
- [Epilogue — What Comes Next](#epilogue--what-comes-next)

---

## Prologue — Why This Story Matters

Every engineer working with AI today uses concepts whose names sound obvious — *embeddings, attention, context window, tool use, agents* — but whose origins are surprisingly recent and whose shape was not at all inevitable. The field has been a sequence of unexpected unlocks, each enabling the next, often discovered by accident.

If you understand the progression — why one technique led to another, what problem each solved — the modern AI landscape stops looking like a random grab-bag of acronyms. It becomes a story with a clear arc. And importantly, it makes predicting *what comes next* much easier.

This document is that story, told in chapters you can read over a weekend. It's not a textbook. It's a guided tour through the ideas — with the technical depth of someone who needs to build with these tools, not train them.

We'll start in the 2010s, before any of this was possible. We'll end in 2026, with agents autonomously running multi-day scientific experiments. In between, you'll meet the handful of ideas that changed everything.

---

## Chapter 1 — The World Before Transformers

To understand why the transformer (2017) felt like such a lightning strike, you have to feel the ceiling that came before it.

In the early 2010s, making a computer understand language was considered genuinely hard. The best techniques processed text **one word at a time, sequentially**, using architectures called **Recurrent Neural Networks** (RNNs) and their more sophisticated cousin, **LSTMs** (Long Short-Term Memory networks). The metaphor is a reader moving left-to-right through a sentence, trying to remember what came before.

### The fundamental limitations

RNNs had two crippling problems:

**The vanishing gradient problem.** When an RNN processed a long sentence, information from early words would decay exponentially as it passed through each step. By the time the network reached word 50, it had effectively forgotten word 1. LSTMs helped — they added a kind of internal "memory gate" — but didn't solve it.

**Sequential computation.** Because each step depended on the previous one, RNNs couldn't be parallelized. You couldn't train them on modern GPUs efficiently. This capped how large you could make them.

### The one great idea from this era: word embeddings

Before transformers, one idea *did* survive the transition and still underlies everything today: **word embeddings**.

In 2013, a paper from Google called *word2vec* showed that you could represent every word as a vector of numbers (say, 300 dimensions) such that words with similar meanings had similar vectors. Famously: `vector("king") - vector("man") + vector("woman") ≈ vector("queen")`. Meaning had become arithmetic.

This was the conceptual seed that eventually grew into today's embedding models, vector databases, and semantic search. You cannot understand modern RAG without understanding that words — and later, sentences, paragraphs, and documents — can be converted into vectors where geometric proximity means semantic similarity.

### The "attention" prototype

The final important idea from the pre-transformer era came from **machine translation** research around 2014–2016. Researchers realized that when translating a long sentence, the model shouldn't try to compress the whole thing into a single memory vector (as RNNs did). Instead, when generating each word of the translation, the model should be allowed to **"attend" to specific relevant words in the source**. This was the primitive form of the **attention mechanism** — and it worked so well that researchers started asking: *do we even need the RNN part?*

### Further reading & watching

- 📹 [3Blue1Brown — Neural Networks series](https://www.youtube.com/playlist?list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi) — still the best visual intro to neural networks
- 📄 [word2vec original paper (2013)](https://arxiv.org/abs/1301.3781) — the paper that made word vectors famous
- 📄 [Understanding LSTM Networks — Chris Olah](https://colah.github.io/posts/2015-08-Understanding-LSTMs/) — classic, extremely clear explainer
- 📄 [The Illustrated word2vec — Jay Alammar](https://jalammar.github.io/illustrated-word2vec/) — visual walkthrough

---

## Chapter 2 — Attention Is All You Need (2017)

In June 2017, eight researchers at Google published a paper titled *Attention Is All You Need*. The title was provocative, and turned out to be almost literally true.

They proposed a new architecture — the **Transformer** — that threw out RNNs entirely. No more sequential processing. No more vanishing gradients. Just attention.

### What attention actually does

Imagine every word in a sentence as a tiny circle. The transformer draws lines between every pair of circles and measures how strongly each word should "pay attention" to each other word. These weights are learned during training. The output of attention is a new representation of each word that incorporates information from every *other* word — weighted by relevance.

The key insight: **every word can look at every other word, simultaneously, in parallel**. This is mathematically elegant (it's just matrix multiplication) and perfectly suited to GPUs.

### Why this mattered

Three immediate consequences, each of which would become a defining property of the modern AI world:

**1. Parallelism unlocked scale.** Because attention is parallel, you can train enormous models on enormous datasets using enormous amounts of compute. The "scaling race" that produced GPT-3, GPT-4, Claude, Gemini, and Llama would have been impossible without this.

**2. Long-range dependencies solved.** Attention's reach is uniform across the sequence. A transformer looking at word 50 can see word 1 as clearly as word 49.

**3. General-purpose architecture.** Originally designed for translation, transformers turned out to work — with minor modifications — for image recognition, audio, protein folding, code, video, and nearly everything else. The transformer wasn't a language model. It was a sequence-modeling primitive.

### The mental model to carry forward

When you hear the word "transformer" today, picture: **for every token in the input, look at every other token, decide how important each is to you, and mix their information into your representation.** Do this many times in stacked layers. Train it on trillions of tokens. That's the machine that makes LLMs work.

### Further reading & watching

- 📄 [Attention Is All You Need (original paper)](https://arxiv.org/abs/1706.03762) — surprisingly readable
- 📄 [The Illustrated Transformer — Jay Alammar](https://jalammar.github.io/illustrated-transformer/) ⭐ **the** explainer everyone recommends
- 📹 [3Blue1Brown — But what is a GPT? Visual intro to transformers](https://www.youtube.com/watch?v=wjZofJX0v4M) — best visual intuition
- 📹 [3Blue1Brown — Attention in transformers, visually explained](https://www.youtube.com/watch?v=eMlx5fFNoYc) — deeper on attention specifically
- 📹 [Andrej Karpathy — Let's build GPT from scratch](https://www.youtube.com/watch?v=kCc8FmEb1nY) — builds a transformer line by line

---

## Chapter 3 — The Pre-training Revolution (2018–2019)

With transformers in hand, two ideas transformed the field between 2018 and 2019, both centered around a single question: *what if we pre-trained the model on massive amounts of raw text, and only later fine-tuned it for specific tasks?*

### BERT — Bidirectional understanding

In late 2018, Google released **BERT** (Bidirectional Encoder Representations from Transformers). BERT was trained on a simple task: take a sentence, randomly mask 15% of the words, ask the model to predict what they were. That's it.

What emerged was a model with a deep, general understanding of English. You could take BERT and, with just a little fine-tuning, beat state-of-the-art on almost every NLP benchmark: sentiment analysis, question answering, named entity recognition, you name it.

BERT cemented the paradigm that still governs the field: **pre-train once on massive general data, fine-tune cheaply for specific tasks**. Everyone in industry adopted it within months.

### GPT — The quiet alternative

A smaller lab — OpenAI, at that point a nonprofit — was pursuing a subtly different idea. Instead of masking words in the middle of a sentence, they trained a transformer to predict the **next word** given all previous words. This is called **autoregressive language modeling**, or "causal" modeling — each word only attends to words that came before it, not after.

In 2018 they released **GPT-1**, which was decent but unremarkable. Then in February 2019 they released **GPT-2**, which was remarkable. It could write coherent paragraphs, complete stories, answer trivia. OpenAI famously delayed the release of the largest version out of concern it could be misused — a decision that now reads as either prophetic or theatrical, depending on your view.

### The deep split

BERT and GPT embodied two philosophies:

- **BERT (masked language modeling)** was better at *understanding* — classification, extraction, tagging.
- **GPT (next-token prediction)** was better at *generating* — writing, completing, creating.

For years, BERT-style models dominated industry NLP because generation seemed like a novelty. Then came 2020.

### Further reading & watching

- 📄 [The Illustrated BERT — Jay Alammar](https://jalammar.github.io/illustrated-bert/)
- 📄 [The Illustrated GPT-2 — Jay Alammar](https://jalammar.github.io/illustrated-gpt2/)
- 📄 [BERT original paper](https://arxiv.org/abs/1810.04805)
- 📄 [GPT-2 paper: Language Models are Unsupervised Multitask Learners](https://cdn.openai.com/better-language-models/language_models_are_unsupervised_multitask_learners.pdf)
- 📹 [Andrej Karpathy YouTube](https://www.youtube.com/@AndrejKarpathy) — deep lectures on GPT architecture

---

## Chapter 4 — The Scale Awakening (2020)

In May 2020, OpenAI published a paper introducing **GPT-3**. The paper itself was dense, 75 pages, with an unassuming title. What it contained reset every assumption the field had about language models.

GPT-3 was 175 billion parameters — about 100 times larger than GPT-2. But the shocking result wasn't just that it was better. It was how it was better.

### Emergent abilities

Previous models had to be **fine-tuned** for each task — you'd take BERT, add a small task-specific head, train it on a labeled dataset for sentiment analysis, and now you had a sentiment classifier. Each task required data, training, and deployment.

GPT-3, at 175 billion parameters, could do many of these tasks **with zero training examples** — just by describing the task in English. Show it two examples in the prompt and it would do translations. Ask a question and it would answer. Describe a style and it would mimic it. This was called **in-context learning**, and it had not been predicted. It seemed to *emerge* from scale.

Ability after ability appeared as models grew: arithmetic, multi-step reasoning, code completion. There was a paper later called *"Emergent Abilities of Large Language Models"* that plotted these abilities — each one looked like a phase transition, flat at smaller scales and suddenly present past some threshold. The lesson the field drew: **bigger models aren't just quantitatively better. They're qualitatively different.**

### The new primitive: prompting

GPT-3 introduced a new programming paradigm: instead of training a model, you *prompt* it. Your "program" is an English instruction. This was weird and uncomfortable for engineers used to deterministic APIs, but it was enormously powerful. You could build a translator, a summarizer, a code completer, and a chatbot from the same model, just by changing the prompt.

This is the moment "prompt engineering" became a thing — and the moment the gap between "AI researcher" and "software engineer using AI" started to close.

### Context windows

GPT-3 had a **context window** of 2,048 tokens — roughly 1,500 words. That felt luxurious at the time. Every model since has pushed the ceiling: GPT-4 (8k → 128k), Claude (100k → 200k → 1M with some variants), Gemini (1M, then 2M). Each expansion unlocked new applications — analyzing whole codebases, long documents, hours of video.

### Further reading & watching

- 📄 [GPT-3 paper: Language Models are Few-Shot Learners](https://arxiv.org/abs/2005.14165)
- 📄 [Emergent Abilities of Large Language Models](https://arxiv.org/abs/2206.07682)
- 📄 [The Illustrated GPT-3 — Jay Alammar](https://jalammar.github.io/how-gpt3-works-visualizations-animations/)
- 📹 [Andrej Karpathy — Intro to Large Language Models](https://www.youtube.com/watch?v=zjkBMFhNj_g) ⭐ **the** one-hour talk
- 📄 [Scaling Laws for Neural Language Models (Kaplan et al.)](https://arxiv.org/abs/2001.08361) — the paper that justified going big

---

## Chapter 5 — Making AI Helpful: RLHF and ChatGPT (2022)

GPT-3 was powerful but raw. Ask it a question and it might answer; it might also complete your question with a series of more questions, or produce confidently wrong information. It had no concept of being *helpful*. It was a text continuation engine.

Between 2021 and 2022, researchers at OpenAI and Anthropic (founded by ex-OpenAI researchers) worked on the problem of **alignment** — making models produce what humans actually wanted, rather than just statistically plausible next tokens.

### RLHF — Reinforcement Learning from Human Feedback

The technique that cracked this was called **RLHF**. The recipe:

1. Take a pre-trained base model (like GPT-3).
2. Have humans write example conversations: *"Here's how I'd ideally answer this prompt."* Fine-tune the model on these examples. This is called **supervised fine-tuning (SFT)**.
3. Generate multiple responses to the same prompt. Have humans rank them best-to-worst. Train a second model — the **reward model** — to predict these rankings.
4. Use reinforcement learning to nudge the original model toward producing responses the reward model scores highly.

The result was a model that didn't just continue text — it answered questions, followed instructions, refused harmful requests, and acknowledged uncertainty. This was the bridge from "interesting research demo" to "useful product."

### November 30, 2022 — ChatGPT

On November 30, 2022, OpenAI released **ChatGPT** — essentially GPT-3.5 with RLHF and a chat interface. It reached 100 million users in two months, the fastest consumer product adoption in history.

What made ChatGPT explosive wasn't a new capability. GPT-3 had been available for two years. The breakthrough was the *combination*: a model that followed instructions well, wrapped in a chat UI that anyone — including non-engineers — could use. Suddenly AI wasn't an API. It was a conversation partner.

The ripple effects:
- Every tech company scrambled for an AI strategy
- Venture capital flooded into AI startups
- Governments began drafting AI policy
- Schools debated whether students could use it
- "Prompt engineer" briefly became a viable job title

This was the moment AI went from technical curiosity to cultural event.

### Further reading & watching

- 📄 [Training language models to follow instructions (InstructGPT)](https://arxiv.org/abs/2203.02155) — the RLHF paper
- 📄 [Constitutional AI (Anthropic's approach)](https://arxiv.org/abs/2212.08073) — alternative to RLHF using AI feedback
- 📹 [Anthropic YouTube Channel](https://www.youtube.com/@anthropic-ai) — explainers on alignment
- 📄 [ChatGPT announcement blog](https://openai.com/index/chatgpt/)
- 📄 [RLHF explained — Chip Huyen](https://huyenchip.com/2023/05/02/rlhf.html) — extremely clear walkthrough

---

## Chapter 6 — The Cambrian Explosion (2023)

2023 was the year every assumption broke. A single year contained what, in most fields, would be a decade of progress.

### GPT-4 (March 2023)

In March, OpenAI released **GPT-4**. It was dramatically better at reasoning, much harder to jailbreak, and — for the first time — *multimodal*. It could see images.

The numbers are almost absurd in retrospect: GPT-4 passed the bar exam in the 90th percentile, scored 5s on multiple AP exams, performed at expert level on medical licensing. The "ceiling" the field thought existed kept moving up.

### Claude, LLaMA, and the open-source earthquake

Anthropic released **Claude** — a model trained with a novel alignment approach called **Constitutional AI**, where the model is taught to evaluate its own responses against a set of written principles instead of relying entirely on human feedback.

Meta released **LLaMA** — the first credibly frontier-quality open-source model. The weights were "accidentally" leaked within days and the open-source AI ecosystem exploded. Within months there were hundreds of fine-tuned LLaMA variants. Running capable AI on your own laptop went from impossible to ordinary.

Google renamed Bard to **Gemini**. Mistral (France) released competitive open models. The field stopped being a two-horse race.

### Multimodal becomes normal

By end of 2023, AI could see, hear, speak, and reason. Images, audio, and video could go in and out of models. The boundary between "language model" and "AI" blurred. "LLM" is still the term of art, but most frontier models are now general multimodal systems.

### The year of "holy crap"

If you weren't working in AI in 2023, it's hard to convey the vibe. Every week there was a new capability announcement, a new model release, a new demo that seemed to break expectations. The field, previously dominated by academic papers, shifted to a product-and-demo-driven culture. By the end of 2023, AI was everywhere — in IDEs, in Google Docs, in customer support, in search.

### Further reading & watching

- 📄 [GPT-4 Technical Report](https://arxiv.org/abs/2303.08774)
- 📄 [LLaMA paper](https://arxiv.org/abs/2302.13971)
- 📄 [Constitutional AI paper (Anthropic)](https://arxiv.org/abs/2212.08073)
- 📹 [Andrej Karpathy — State of GPT (2023)](https://www.youtube.com/watch?v=bZQun8Y4L2A) — fantastic overview talk
- 📄 [Sparks of Artificial General Intelligence (Microsoft's GPT-4 study)](https://arxiv.org/abs/2303.12712)

---

## Chapter 7 — From Chatbots to Agents

By 2023, LLMs could hold a conversation, write code, and answer questions. But they still lived in a box. They couldn't access the internet, query your database, or trigger a deploy. They could *talk about* actions but not *take* them.

This limitation was about to be solved.

### Function calling — the unlock

In mid-2023, OpenAI and Anthropic both introduced **function calling** (also called *tool use*). The idea was simple but transformative:

You describe, in a structured schema, a list of functions the model can invoke — their names, descriptions, and parameter types. When you send a user message, the model can choose to respond with text *or* with a structured call to one of your functions. Your code executes the function. You send the result back. The model continues reasoning.

Suddenly models could:
- Search the web (via a search function)
- Query databases (via SQL functions)
- Send emails (via email functions)
- Run code (via code-execution functions)
- Call other APIs (via HTTP functions)

This was the birth of the **agent** — an LLM that doesn't just talk but *does*.

### ReAct — Reason + Act

The thinking pattern that emerged was called **ReAct**. The model alternates between:
- **Thought:** "I need to find the user's order history."
- **Action:** `query_database("SELECT * FROM orders WHERE user_id = 123")`
- **Observation:** `[rows returned]`
- **Thought:** "The most recent order failed. Let me check the payment logs."
- **Action:** `search_logs("payment_service", "order_id=456")`
- ... and so on.

ReAct (introduced in a 2022 paper) became the backbone pattern for nearly every agent system. Modern frameworks — LangChain, LangGraph, CrewAI — all implement variants of it.

### What changed about software

Function calling didn't just add a feature. It changed what software could be. An engineer who previously had to choose between "deterministic code" and "clever heuristics" now had a third option: **an LLM orchestrating deterministic code**. You get the flexibility of natural-language reasoning with the reliability of typed functions. This is the architectural pattern behind most modern AI features: the AI isn't doing the work — it's deciding what work to do.

### Further reading & watching

- 📄 [ReAct: Synergizing Reasoning and Acting (2022)](https://arxiv.org/abs/2210.03629) — foundational paper
- 📄 [Toolformer: Language Models Can Teach Themselves to Use Tools](https://arxiv.org/abs/2302.04761)
- 📄 [Anthropic Tool Use Documentation](https://docs.anthropic.com/en/docs/build-with-claude/tool-use/overview)
- 📄 [OpenAI Function Calling Guide](https://platform.openai.com/docs/guides/function-calling)
- 📹 [LangChain YouTube Channel](https://www.youtube.com/@LangChain) — countless agent tutorials

---

## Chapter 8 — The Knowledge Problem: RAG & Vector Search

There was still a huge problem with LLMs: they only knew what was in their training data. They couldn't access your company's documents, today's news, or anything past their cutoff. Worse, they'd confidently *make things up* (hallucinate) when they didn't know.

The solution that emerged, with roots going back to a 2020 paper, was called **Retrieval-Augmented Generation (RAG)**.

### The RAG pattern

The idea is elegant:

1. **Ingest:** Take your documents, split them into chunks, convert each chunk into an embedding vector, and store in a vector database.
2. **Retrieve:** When a user asks a question, embed the question, find the most similar chunks in your vector DB.
3. **Generate:** Inject those chunks into the prompt as context. Ask the LLM to answer based on them.

The LLM is now "grounded" in real data rather than relying on memorization. Hallucinations drop dramatically. You can answer questions about documents the model has never seen.

### Why this needed embeddings

Plain keyword search (like Elasticsearch) matches words, not meanings. If a user asks *"what's our refund policy?"* and the document is titled *"Money-back guarantee process"*, keyword search misses. Embeddings solve this by converting both query and document into vectors where semantic similarity is geometric proximity. Embeddings are Chapter 1's word vectors, grown up: now they encode whole sentences and paragraphs.

### The vector database boom

2023–2024 saw an explosion of vector databases: **Pinecone**, **Weaviate**, **Qdrant**, **Chroma**. Postgres added `pgvector`. MongoDB added vector search. Elastic added vector search. Redis added vector search.

This is a pattern you'll see repeatedly in AI: a new primitive emerges, specialized vendors appear, and within 18 months the primitive is absorbed into every existing database. In 2026, "vector search" is a feature, not a product.

### RAG got sophisticated fast

The naïve version of RAG (embed → retrieve → generate) has known failure modes. Over 2024 the field developed:
- **Hybrid search** — combining vector search with keyword search (BM25), merged via reciprocal rank fusion
- **Reranking** — using a stronger model to rerank retrieved chunks
- **Query rewriting** — the LLM rewrites the user's question before search
- **Self-RAG** — the LLM decides *when* to retrieve, not always
- **GraphRAG** — building a knowledge graph over documents, retrieving via graph walks

### Further reading & watching

- 📄 [Original RAG paper (2020)](https://arxiv.org/abs/2005.11401)
- 📄 [Self-RAG](https://arxiv.org/abs/2310.11511) — model decides when to retrieve
- 📹 [LangChain — RAG From Scratch Playlist](https://www.youtube.com/playlist?list=PLfaIDFEXuae2LXbO1_PKyVJiQ23ZztA0x) ⭐ gold standard
- 📄 [Eugene Yan — Patterns for Building LLM Systems](https://eugeneyan.com/writing/llm-patterns/)
- 📄 [pgvector README](https://github.com/pgvector/pgvector) — add vector search to Postgres

---

## Chapter 9 — Reasoning Models & Test-Time Compute (2024–2025)

By 2024, a new wall was becoming visible. Frontier models had absorbed essentially all high-quality text on the internet. You couldn't just scale data much further. And scaling parameters alone was yielding diminishing returns. The industry needed a new axis to grow along.

The answer turned out to be: spend more compute **at inference time**, not training time.

### OpenAI o1 (September 2024)

In September 2024, OpenAI released a model called **o1**. What made it different: instead of responding immediately, it would first produce a long internal "chain of thought" — sometimes thousands of tokens of reasoning — before emitting a final answer. On hard problems (math olympiads, competitive programming, graduate-level physics), o1 outperformed GPT-4 by a wide margin.

The key insight: **for hard problems, thinking longer helps**. This is true for humans and, as it turned out, for models. Give an LLM more tokens to "think," and on tasks with verifiable answers, accuracy climbs dramatically.

This opened a new scaling axis: **test-time compute**. Historically, AI improved by training bigger models on more data. Now a second axis appeared — at inference, let the model think longer, sample more candidates, verify its work. More compute per query, better answers.

### Reasoning models become standard

Over 2024–2025, every frontier lab released reasoning models:
- OpenAI: o1, o3
- Anthropic: Claude with "extended thinking" modes
- Google: Gemini 2.0 "thinking" variants
- DeepSeek (China): R1, released open-source, demonstrated state-of-the-art reasoning could be achieved far more cheaply than was believed

### What this means for engineers

For most everyday tasks (summarization, simple Q&A, classification), fast models are still better — they're cheaper and the "thinking" doesn't help. But for complex tasks (code reasoning, math, multi-step planning, hard agent tasks), reasoning models are genuinely transformative. The engineering skill becomes: **knowing when to route a query to a fast model vs. a reasoning model**. This is the basis of modern *model routing*.

### The "chain of thought" is now a design primitive

For older models, you'd prompt "think step by step" to get CoT behavior. Reasoning models do this automatically and internally. But the design principle — *give the model room to think before answering* — now shapes how agent systems are built, how prompts are written, and how evaluation is done.

### Further reading & watching

- 📄 [OpenAI o1 System Card](https://openai.com/index/openai-o1-system-card/)
- 📄 [DeepSeek R1 paper](https://arxiv.org/abs/2501.12948) — open-source reasoning model
- 📄 [Let's Verify Step by Step (OpenAI)](https://arxiv.org/abs/2305.20050) — process reward models
- 📹 [Anthropic YouTube Channel](https://www.youtube.com/@anthropic-ai) — search "extended thinking"
- 📄 [Anthropic — Extended Thinking docs](https://docs.anthropic.com/en/docs/build-with-claude/extended-thinking)

---

## Chapter 10 — The Agent Era Begins (2025)

If 2023 was the year of chatbots, 2024 was the year of tools, and 2025 was the year of **agents**.

The difference is subtle but important:
- A **chatbot** responds to messages
- A **tool-using LLM** can invoke functions when asked
- An **agent** pursues goals autonomously — planning, acting, observing, self-correcting, and sometimes running for hours or days

### The ingredients that made agents work

Three things came together:
1. **Reliable tool use** (Chapter 7) — the model could call functions predictably
2. **Long context + RAG** (Chapters 4, 8) — the model could access memory and knowledge
3. **Reasoning** (Chapter 9) — the model could plan multi-step actions

Combine them and you get an entity that can, for example, be told "investigate this customer's complaint" and autonomously: read their support history, query their account, check related outages, draft a response, and escalate if needed.

### Frameworks emerged

Building agents from scratch was possible but tedious. Frameworks crystallized the patterns:
- **LangChain** (earliest, most ecosystem)
- **LangGraph** (agents as state machines — the production standard)
- **CrewAI** (role-based multi-agent)
- **AutoGen** (Microsoft — conversation-based multi-agent)
- **Pydantic AI** (Python-type-safe agents)

LangGraph in particular matched how engineers already think: agents as graphs with explicit state, nodes, and conditional edges. Debuggable. Testable. Checkpointable.

### Long-running agents

A genuinely new capability in 2025 was **long-running agents** — agents that persist for hours, days, or weeks, checkpointing state to databases, surviving restarts, and doing substantial work autonomously.

Anthropic's "Project Vend" experiments had Claude autonomously managing real-world business operations. By late 2025 / early 2026, "vibe physics" was a term for using AI as a research collaborator on multi-day theoretical physics problems — setting up simulations, interpreting results, proposing new hypotheses, writing up findings.

The workflow pattern that emerged: **human sets goal → agent plans → agent executes with periodic checkpoints → human reviews key decisions → agent continues**. Think of agents as interns who can work nights and weekends, if you trust them enough.

### The productivity data

Studies over 2025 reported that knowledge workers using AI saved 30–80% of time on task subsets. Coding in particular saw massive productivity gains — engineers using Cursor, Claude Code, or similar tools reported 2–5x faster shipping on many task types. This reshaped hiring: "can you effectively use AI tools" became as important as classical coding ability.

### Further reading & watching

- 📄 [Anthropic — Building effective agents](https://www.anthropic.com/research/building-effective-agents)
- 📄 [LangGraph Conceptual Guide](https://langchain-ai.github.io/langgraph/concepts/)
- 📹 [LangChain YouTube Channel — agent tutorials](https://www.youtube.com/@LangChain)
- 📹 [AI Engineer Conference Channel](https://www.youtube.com/@aiDotEngineer) — production agent talks
- 📄 [Andrew Ng — Agentic Design Patterns (4-part series)](https://www.deeplearning.ai/the-batch/issue-241/)

---

## Chapter 11 — MCP and the Standardization Wave

Every agent framework, every AI app, every IDE with AI features faced the same boring problem: *how do I let my AI connect to the user's tools and data?* Every company was solving it differently. Claude had one plugin format. ChatGPT had another. Custom GPTs had a third. Every IDE had its own. It was the API integration problem of 2005 all over again, but for AI.

In November 2024, Anthropic proposed an open standard called **Model Context Protocol (MCP)** to solve this.

### What MCP is

MCP defines three primitives that any server can expose:
- **Tools** — functions the AI can invoke
- **Resources** — data the AI can read
- **Prompts** — reusable prompt templates

And two transport modes:
- **stdio** — the server runs as a subprocess (local, simple)
- **HTTP/SSE** — the server is networked (remote, production)

Any AI client that speaks MCP can use any MCP server. Write once, work everywhere. The analogy that stuck was **"USB-C for AI agents."**

### The adoption curve

MCP went from "proposal" to "de facto standard" faster than anyone expected. Within months, Claude Desktop, Cursor, Zed, VS Code (via extensions), and many others became MCP clients. Reference MCP servers appeared for GitHub, GitLab, Postgres, Slack, Google Drive, filesystem, and dozens of SaaS products. In December 2025, Anthropic donated MCP to a new **Agentic AI Foundation**, making it a community-governed standard.

### Why this matters more than it seems

MCP isn't a sexy AI breakthrough. It's plumbing. But plumbing determines ecosystems. Once a standard interface exists:
- Small teams can build MCP servers for their niche tools and instantly have AI integration
- Big companies don't have to integrate every AI platform separately — they expose one MCP server
- Agents can compose tools across domains (pull data from Salesforce → analyze → write to Notion → notify in Slack) without custom code

MCP is likely to be remembered as the moment AI became an *ecosystem* rather than a set of products.

### For backend engineers specifically

MCP is where your skills become most directly valuable. An MCP server is a well-typed service exposing endpoints — except the consumer is an AI, not another microservice. Every backend service you've built can be wrapped as an MCP server, instantly making it AI-accessible.

### Further reading & watching

- 📄 [Official MCP Docs](https://modelcontextprotocol.io/introduction)
- 📄 [MCP Specification](https://modelcontextprotocol.io/specification)
- 🐙 [modelcontextprotocol/python-sdk](https://github.com/modelcontextprotocol/python-sdk)
- 🐙 [modelcontextprotocol/servers — reference implementations](https://github.com/modelcontextprotocol/servers)
- 📹 [Anthropic YouTube Channel](https://www.youtube.com/@anthropic-ai) — search "MCP"

---

## Chapter 12 — Where We Are Now (2026)

As of April 2026, the frontier looks like this:

### Models

Frontier general-purpose models (Claude Opus 4.6, GPT-class successors, Gemini) combine:
- Long context (200k–1M+ tokens)
- Native multimodality (text, images, audio, video in and out)
- Tool use as a first-class capability
- Extended thinking / reasoning on demand
- Strong agentic behavior across multi-step tasks

Small, efficient models (Claude Haiku 4.5, small Llamas, small Gemini, Phi-family) run on laptops and phones, matching GPT-4-class performance from 2023 at a tiny fraction of the cost. **On-device AI is real.**

### Agents

The pattern for production AI systems is stabilizing around:
- **LangGraph or similar** for orchestration
- **MCP servers** for tool/data connectivity
- **Vector DBs** (usually pgvector for startups, specialized DBs at scale) for knowledge
- **Langfuse/LangSmith/Braintrust** for observability and evals
- **Reasoning models** for hard tasks; fast models for simple ones

Multi-agent systems — orchestrator + specialized workers — are being deployed in real companies for code review, customer service, research, and ops. Reliability is the binding constraint, not capability.

### Science and other domains

AI is becoming a real research collaborator in domains with verifiable outputs: mathematics (Terence Tao has publicly discussed using AI for proofs), theoretical physics ("vibe physics"), protein design, materials discovery. "Long-running scientific computing" — agents running multi-day experiments — is an emerging practice.

### The economy

The Anthropic Economic Index and similar efforts are tracking AI's actual impact on labor and productivity. Early data suggests large productivity gains in coding, writing, analysis, and customer service — with smaller but real gains almost everywhere else. Policy debates around labor displacement and AI safety are live and serious.

### Safety and alignment

Major labs have formalized safety frameworks. Anthropic published its "Constitution" in January 2026 — an explicit ethical framework governing model behavior. Interpretability research (understanding what's happening inside models) has become a major field, with early results on detecting emotion-like internal states, introspection, and deception.

### The open-source track

Open models (DeepSeek, Llama, Mistral, Qwen) stay 6–12 months behind frontier closed models but are increasingly useful for production — especially when privacy, cost, or customization matter more than raw capability.

### Further reading & watching

- 📄 [Anthropic Research](https://www.anthropic.com/research) — current frontier research
- 📄 [OpenAI Research](https://openai.com/research/)
- 📄 [Anthropic Economic Index](https://www.anthropic.com/economic-index)
- 📄 [Lilian Weng's Blog](https://lilianweng.github.io/) — deep research dives
- 📹 [Latent Space Podcast](https://www.latent.space/) — technical interviews with AI engineers

---

## Epilogue — What Comes Next

Predicting AI is humbling — every serious forecast from 2020 underestimated what happened. But reading the trajectory, a few threads seem likely to continue:

**Context windows will keep expanding.** Eventually "context" and "memory" will merge — agents will have persistent memory spanning weeks or months of interaction.

**Reasoning will get cheaper.** The compute cost of a "reasoning token" keeps dropping. By 2027–2028, running an agent that thinks as deeply as GPT-5 might cost what GPT-3.5 does today.

**Agents will become infrastructure.** Every backend service will eventually expose an MCP interface. Every knowledge worker will manage a small fleet of agents. "Deploy an agent" will be as routine as "deploy a cron job."

**Specialization will emerge.** We'll likely see agents trained specifically for coding, science, legal, medical, and other domains — not as fine-tuned toys but as genuine specialists.

**New capabilities will be surprising.** Emergent behavior has surprised the field at every scale. Predicting it is folly. But expect some number of 2027's capabilities to be things we can't currently imagine.

**The "AI engineer" role will solidify.** Just as "web developer" became a real profession in the 2000s, "AI engineer" is becoming one now — and will have its own senior tracks, specializations, and career ladders by 2028.

### Closing thought

The story of LLMs is, at its core, a story about a single boring idea — **predict the next token, but at enormous scale** — pushed further than anyone expected and unlocking capabilities no one predicted. It's a genuinely unusual moment in the history of software. Most technologies have a clear theoretical ceiling. This one keeps surprising us.

You don't need to be a researcher to participate. You need the mental models. The ideas in this document — embeddings, attention, tokens, context, tool use, RAG, agents, MCP — are the vocabulary of the field. Learn them. Build with them. Watch what's next.

---

## 🎓 Further Learning — The Canonical Reading List

**Blogs & people to follow**
- [Simon Willison](https://simonwillison.net/) — pragmatic, engineering-first AI writing
- [Lilian Weng](https://lilianweng.github.io/) — research-level deep dives
- [Jay Alammar](https://jalammar.github.io/) — the illustrated guides
- [Jason Liu](https://jxnl.co/writing/) — applied patterns, structured outputs
- [Eugene Yan](https://eugeneyan.com/) — LLM systems engineering
- [Hamel Husain](https://hamel.dev/) — evals, production AI
- [Chip Huyen](https://huyenchip.com/) — ML systems design

**Foundational videos**
- [Andrej Karpathy — Intro to LLMs (1hr)](https://www.youtube.com/watch?v=zjkBMFhNj_g) ⭐ start here if you watch only one
- [Andrej Karpathy — Let's build GPT from scratch](https://www.youtube.com/watch?v=kCc8FmEb1nY)
- [3Blue1Brown — What is a GPT?](https://www.youtube.com/watch?v=wjZofJX0v4M)
- [3Blue1Brown — Attention in transformers](https://www.youtube.com/watch?v=eMlx5fFNoYc)

**Channels worth subscribing**
- [Andrej Karpathy](https://www.youtube.com/@AndrejKarpathy)
- [3Blue1Brown](https://www.youtube.com/@3blue1brown)
- [LangChain](https://www.youtube.com/@LangChain)
- [DeepLearning.AI](https://www.youtube.com/@Deeplearningai)
- [Anthropic](https://www.youtube.com/@anthropic-ai)
- [AI Engineer Conference](https://www.youtube.com/@aiDotEngineer)

**Podcasts**
- [Latent Space](https://www.latent.space/) — technical interviews
- [Dwarkesh Podcast](https://www.dwarkeshpatel.com/) — long-form AI researcher interviews
- [The TWIML AI Podcast](https://twimlai.com/podcast/twimlai/)

**Foundational papers (in order of relevance)**
- [Attention Is All You Need (2017)](https://arxiv.org/abs/1706.03762)
- [BERT (2018)](https://arxiv.org/abs/1810.04805)
- [GPT-3 (2020)](https://arxiv.org/abs/2005.14165)
- [RAG (2020)](https://arxiv.org/abs/2005.11401)
- [InstructGPT / RLHF (2022)](https://arxiv.org/abs/2203.02155)
- [Constitutional AI (2022)](https://arxiv.org/abs/2212.08073)
- [ReAct (2022)](https://arxiv.org/abs/2210.03629)
- [Chain-of-Thought Prompting (2022)](https://arxiv.org/abs/2201.11903)
- [Toolformer (2023)](https://arxiv.org/abs/2302.04761)
- [GPT-4 Technical Report (2023)](https://arxiv.org/abs/2303.08774)
- [LLaMA (2023)](https://arxiv.org/abs/2302.13971)

---

*Written April 2026. The field will have moved by the time you read this — which is exactly the point of understanding the story behind the technology.*
