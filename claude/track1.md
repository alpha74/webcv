# 🚀 AI Learning Path for Backend Engineers
### *A complete, standalone reference for going from backend engineer → AI engineer in ~3 months*

> **Built for the next 2 years, not just today.** Deep concept explanations, curated resources, GitHub projects, and build tutorials for every stage.

---

## 📑 Table of Contents

1. [The Big Picture](#the-big-picture)
2. [How to Use This Document](#how-to-use-this-document)
3. [Glossary of Key Terms](#glossary-of-key-terms)
4. [Stage 0 — 10x Your Daily Work NOW](#stage-0--10x-your-daily-work-now)
5. [Stage 1 — LLM Internals](#stage-1--llm-internals)
6. [Stage 2 — Context Engineering](#stage-2--context-engineering)
7. [Stage 3 — Tool Use & Function Calling ⭐](#stage-3--tool-use--function-calling-)
8. [Stage 4 — Structured Outputs + Pydantic](#stage-4--structured-outputs--pydantic)
9. [Stage 5 — RAG & Vector Search](#stage-5--rag--vector-search)
10. [Stage 6 — Agent Frameworks (LangGraph)](#stage-6--agent-frameworks-langgraph)
11. [Stage 7 — MCP Servers ⭐](#stage-7--mcp-servers-)
12. [Stage 8 — AI-Native Backend Patterns](#stage-8--ai-native-backend-patterns)
13. [Stage 9 — LLMOps & Evals](#stage-9--llmops--evals)
14. [Stage 10 — Multi-Agent Systems](#stage-10--multi-agent-systems)
15. [Staying Current](#staying-current)
16. [Timeline & Portfolio Checklist](#timeline--portfolio-checklist)

---

## The Big Picture

### Where backend engineering is heading (2026–2028)

In 2 years, backend engineering will split into two tracks:

1. **Track A — Engineers who build systems that USE AI** as a component (agents, pipelines, tools)
2. **Track B — Engineers who build the AI infrastructure itself** (model serving, training, inference optimization)

This guide targets **Track A** — the larger and more immediately valuable path. Your existing backend skills (APIs, databases, async systems, reliability engineering, distributed systems) are *directly* transferable.

### The core mental shift

> AI agents are becoming a new kind of microservice.

Instead of a service that executes logic **deterministically**, an agent executes logic **probabilistically**, uses tools, maintains state, and makes decisions. Your job as a backend engineer is increasingly to build the infrastructure *around* these agents — memory systems, tool servers, orchestration layers, evaluation pipelines, and reliability guarantees.

### Why backend engineers have an unfair advantage

- **APIs & contracts** → Prompt engineering is really API contract design
- **Databases** → Vector databases are just a new index type
- **Async systems** → Agents run async and need job queues
- **Distributed systems** → Multi-agent systems are microservices with probabilistic routing
- **Observability** → LLMOps is just observability applied to AI
- **Type safety** → Pydantic + Instructor bring it to LLM outputs

---

## How to Use This Document

1. **Do stages sequentially** — each builds on the previous. The "pivot points" (⭐) are where everything clicks.
2. **Always end a stage with code you can push to GitHub** — no passive reading.
3. **Run Stage 0 in parallel with everything else** — it's a productivity multiplier from day one.
4. **Use the "Resources" sections as a menu, not a checklist** — pick 1-2 per stage that match your learning style.
5. **A note on video links:** YouTube URLs occasionally break or change. Where possible, I've linked to **channels** and **playlists** (more stable) and used well-known canonical videos. If a video is unavailable, search the channel by topic — the content almost always exists.

---

## Glossary of Key Terms

| Term | Plain-English Definition |
|---|---|
| **LLM** (Large Language Model) | A neural network trained to predict the next "token" (word fragment) given previous tokens. GPT, Claude, Gemini, Llama are LLMs. |
| **Token** | A chunk of text (roughly 3/4 of a word on average). LLMs don't see characters or words — they see tokens. |
| **Context Window** | The maximum number of tokens an LLM can "see" at once (input + output). Think of it as a request payload size limit. |
| **Temperature** | A sampling parameter (0–2) controlling output randomness. 0 = deterministic, higher = more creative/random. |
| **System Prompt** | Instructions given to the LLM before any user messages — defines behavior, persona, constraints. |
| **Prompt Engineering** | The craft of designing inputs (prompts) to get desired outputs from LLMs. |
| **Context Engineering** | The discipline of designing what information lands in the context window, how it's structured, and when it's retrieved. |
| **Few-shot Learning** | Showing the LLM a few input/output examples in the prompt so it imitates the pattern. |
| **Chain-of-Thought (CoT)** | Prompting the LLM to "think step by step" before answering — dramatically improves reasoning. |
| **Function Calling / Tool Use** | Giving the LLM a list of functions it can invoke. The model returns structured calls; your code executes them. |
| **Structured Output** | Forcing the LLM's response to conform to a specific JSON schema or Pydantic model. |
| **Embedding** | A vector (list of numbers) representing the semantic meaning of text. Similar meanings → nearby vectors. |
| **Vector Database** | A database optimized for similarity search over embeddings. Examples: pgvector, Chroma, Pinecone, Weaviate. |
| **RAG** (Retrieval-Augmented Generation) | A pattern: find relevant chunks from a knowledge base → inject into prompt → generate answer. |
| **Agent** | An LLM that can use tools, maintain state, and take multi-step actions autonomously. |
| **ReAct** | Reason + Act pattern — the agent alternates reasoning steps with tool calls. |
| **MCP** (Model Context Protocol) | An open protocol standardizing how AI agents connect to external tools, data, and prompts. Think "USB-C for AI agents." |
| **LangGraph** | A framework for building agents as directed graphs (state machines) with explicit transitions. |
| **LLMOps** | DevOps for AI — deploying, monitoring, evaluating, and maintaining LLM systems in production. |
| **Eval** | A test case (or suite) that measures whether an LLM/agent produces the expected behavior. |
| **Prompt Injection** | An attack where malicious input data contains instructions that hijack the LLM. The "SQL injection" of AI. |
| **Multi-agent System** | Multiple specialized agents coordinating via a shared protocol (often orchestrator + workers). |
| **Test-time Compute** | Spending more compute at inference (thinking longer) to improve answer quality. Powers "reasoning models." |

---

## Stage 0 — 10x Your Daily Work NOW

> **⚡ Run this in parallel with every other stage. Impact starts today.**

### What is this stage?

Before you learn to *build* AI systems, you need to *use* them daily. This changes how you write code, debug, design systems, and document work. The productivity gains compound over time and make every later stage more intuitive — because you'll understand how tools behave as a user before you build them as an engineer.

### Why it matters (2-year outlook)

By 2027, AI-assisted coding will be as standard as IDE autocomplete. Engineers who haven't internalized the workflow will feel the productivity gap acutely — like a developer today who refuses to use a debugger.

### Core concepts

- **Inline AI editing** — Select code, press a shortcut (e.g., `Cmd+K` in Cursor), describe what you want changed in natural language, see a diff, accept or reject.
- **Agent mode** — Delegate larger refactors or multi-file tasks to the AI; review and commit.
- **AI pair programming** — Use Claude/ChatGPT for rubber-duck debugging, architecture discussion, or explaining legacy code.
- **Context-aware codegen** — Modern tools (Cursor, Copilot) index your codebase so suggestions are relevant to your project, not generic.

### 🛠️ Tools to install today

- **Cursor** — [cursor.com](https://cursor.com) — the editor of choice for AI-forward engineers (fork of VS Code)
- **Claude Desktop** — [claude.ai/download](https://claude.ai/download) — pair programmer + MCP client
- **GitHub Copilot** — [github.com/features/copilot](https://github.com/features/copilot) — secondary option
- **Aider** — [aider.chat](https://aider.chat) — terminal-based AI pair programmer (great for Linux/server work)

### 📚 Resources

**Docs & Articles**
- [Cursor Official Docs](https://docs.cursor.com/)
- [Claude for Coding — Anthropic](https://docs.anthropic.com/en/docs/about-claude/use-cases/coding)
- [Cursor Directory](https://cursor.directory/) — community-shared Cursor rules for different stacks

**Video Resources**
- 📹 [Cursor Channel](https://www.youtube.com/@cursor-ai) — official tutorials
- 📹 [Fireship YouTube Channel](https://www.youtube.com/@Fireship) — concise, engineering-focused AI tool videos
- 📹 [ThePrimeagen YouTube Channel](https://www.youtube.com/@ThePrimeTimeagen) — engineer perspective on AI tools

### 🔨 10x Win (do this within a week)

Take a real task from your current job — add a new API endpoint, refactor a service, write integration tests — and do it entirely with AI assistance in Cursor. Track your time vs. your normal pace. This primes your instincts for what AI is actually good at (and where it's not).

---

## Stage 1 — LLM Internals
**⏱ Time:** 3–5 days | **🔁 Backend Analogy:** Understanding a new database engine

### What is this stage?

Learn the conceptual model of how LLMs work — just enough theory to stop treating them as magic black boxes. You're not training models; you're learning what happens when you call one.

### Why it matters (2-year outlook)

LLM API calls will be as routine in backend codebases as database queries are today. Every backend engineer will need to reason about their cost, latency, failure modes, and limitations. Without this foundation, you'll make subtle design mistakes for years.

### Core concepts explained

**LLMs are stateless functions**  
`f(conversation_history) → next_token`. The model has no memory between requests. All "memory," "learning," or "state" across turns is *your* responsibility to manage externally — in a database, cache, or context window. This is the single most important insight.

**Tokens, not words**  
LLMs process text as **tokens** — sub-word units created by a tokenizer (BPE or similar). "Hello world" might be 2 tokens; "antidisestablishmentarianism" might be 7. This matters because pricing is per-token, context windows are measured in tokens, and latency scales with token count.

**The context window**  
The maximum number of tokens the model can see at once. Claude Sonnet 4.6 and GPT-4 class models handle ~200k tokens; some models go to 1M+. Everything — system prompt, few-shot examples, retrieved documents, user message, and generated response — must fit. Think of it as a hard request payload limit.

**Temperature and sampling**  
LLMs don't pick "the right" next token — they pick from a probability distribution. Temperature rescales that distribution: 0.0 = always pick the most likely token (deterministic), 1.0 = sample as-is, >1.0 = more random. Use 0 for extraction/classification; 0.7+ for creative tasks.

**Transformers & attention (high-level)**  
You don't need the math, but know this: transformers use **attention** — every token "looks at" every other token in the context to decide what to output. This is why context quality matters so much: irrelevant context distracts the model.

**Why models hallucinate**  
LLMs are trained to produce *plausible-sounding* tokens, not *true* ones. When asked something outside their training, they generate the most statistically likely continuation — which may be confidently wrong. RAG (Stage 5) is the primary mitigation.

### 📚 Resources

**Video Resources (all verified canonical)**
- 📹 [Andrej Karpathy — Intro to Large Language Models (1hr)](https://www.youtube.com/watch?v=zjkBMFhNj_g) ⭐ **Best single video on LLMs**
- 📹 [Andrej Karpathy — Let's build GPT from scratch (2hr)](https://www.youtube.com/watch?v=kCc8FmEb1nY) — optional deep dive
- 📹 [3Blue1Brown — But what is a GPT? Visual intro to transformers](https://www.youtube.com/watch?v=wjZofJX0v4M) — visual intuition
- 📹 [3Blue1Brown Neural Networks Playlist](https://www.youtube.com/playlist?list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi) — foundation
- 📹 [Karpathy YouTube Channel](https://www.youtube.com/@AndrejKarpathy) — all his LLM tutorials

**Docs**
- [Anthropic API Quickstart](https://docs.anthropic.com/en/docs/get-started)
- [OpenAI API Quickstart](https://platform.openai.com/docs/quickstart)
- [Anthropic — How Claude Works](https://docs.anthropic.com/en/docs/about-claude/models/overview)

### 🐙 GitHub References

- [karpathy/nanoGPT](https://github.com/karpathy/nanoGPT) — build a GPT from scratch in ~300 lines
- [anthropics/anthropic-cookbook](https://github.com/anthropics/anthropic-cookbook) — Claude API examples
- [openai/openai-cookbook](https://github.com/openai/openai-cookbook) — OpenAI API examples
- [anthropics/anthropic-sdk-python](https://github.com/anthropics/anthropic-sdk-python) — official SDK

### 🔨 Build: Raw HTTP Chatbot

Build a CLI chatbot using only `httpx` (or `requests`) calling the Anthropic or OpenAI API directly — **no SDKs, no frameworks**. Manually maintain the conversation array across turns. This forces you to understand exactly what every framework abstracts.

**Key things to implement:**
- Multi-turn conversation array management
- Handle rate limits (429 responses) with exponential backoff
- Streaming responses (SSE) for token-by-token display
- Token counting before sending (to prevent context overflow)

**Build tutorials / references:**
- [Anthropic Python Quickstart](https://docs.anthropic.com/en/docs/build-with-claude/overview)
- [Anthropic cookbook — misc examples](https://github.com/anthropics/anthropic-cookbook/tree/main/misc)

---

## Stage 2 — Context Engineering
**⏱ Time:** 1 week | **🔁 Backend Analogy:** API contract design

### What is this stage?

"Prompt engineering" is evolving into **context engineering** — the discipline of designing *what information* goes into an LLM's context window, *how it's structured*, and *when it's retrieved*. It's the single biggest lever on output quality.

### Why it matters (2-year outlook)

"Context Engineer" is becoming a real job title at AI-forward companies. The pattern you design for a prompt today will dictate reliability at scale tomorrow. Also: prompt-engineering-as-a-skill is fundamentally an engineering discipline — precision, reproducibility, testability — which plays directly to your strengths.

### Core concepts explained

**System prompts are API specs**  
A system prompt defines the model's behavior, persona, constraints, and output format. Think of it as writing documentation for an extremely capable but naïve contractor. Be explicit. Be precise. Give examples.

**Few-shot prompting**  
Including 2–5 input/output examples before the real task. LLMs excel at pattern imitation. Often 3 good examples outperform 10 paragraphs of instructions.

**Chain-of-Thought (CoT)**  
Asking the model to "think step by step" before answering. Dramatically improves accuracy on math, logic, and multi-step tasks. For reasoning models (like o1 / Claude thinking mode), this happens automatically.

**Instruction positioning**  
LLMs pay slightly more attention to the *start* and *end* of the context. Put the most critical instructions there. This is called the "lost in the middle" problem.

**Output formatting via markers**  
Using XML tags (`<thinking>...</thinking>`, `<answer>...</answer>`) or clear delimiters helps structured parsing and often helps the model itself organize its response.

**Context pollution**  
Every irrelevant token competes for attention. Aggressively trim context. Less is often more.

**Prompt templating**  
For production, never f-string-interpolate user input into prompts (injection risk). Use templating libraries (Jinja2, Pydantic-style templates) with clear variable boundaries.

### 📚 Resources

**Docs & Articles (highest signal)**
- [Anthropic Prompt Engineering Guide](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview) ⭐ best in ecosystem
- [DAIR.AI Prompt Engineering Guide](https://www.promptingguide.ai/) — comprehensive reference
- [OpenAI Prompt Engineering Guide](https://platform.openai.com/docs/guides/prompt-engineering)
- [Simon Willison's Blog — search "prompt"](https://simonwillison.net/tags/prompt-engineering/) — pragmatic AI writing

**Courses**
- 🎓 [DeepLearning.AI — ChatGPT Prompt Engineering for Developers](https://www.deeplearning.ai/short-courses/chatgpt-prompt-engineering-for-developers/) — free, 1hr, Jupyter notebooks
- 🎓 [Anthropic — Prompt Engineering Interactive Tutorial](https://github.com/anthropics/prompt-eng-interactive-tutorial) — hands-on

**Video Resources**
- 📹 [DeepLearning.AI YouTube](https://www.youtube.com/@Deeplearningai) — search "prompt engineering"
- 📹 [Andrew Ng & Isa Fulford — short course videos](https://www.deeplearning.ai/short-courses/chatgpt-prompt-engineering-for-developers/)

### 🐙 GitHub References

- [anthropics/prompt-eng-interactive-tutorial](https://github.com/anthropics/prompt-eng-interactive-tutorial) — Anthropic's free tutorial
- [dair-ai/Prompt-Engineering-Guide](https://github.com/dair-ai/Prompt-Engineering-Guide) — massive resource repo
- [f/awesome-chatgpt-prompts](https://github.com/f/awesome-chatgpt-prompts) — reference prompts

### 🔨 Build: Structured Data Extractor

Feed the tool messy unstructured text (emails, Slack messages, Jira comments) and get back clean structured fields — priority, assignee, status, deadline, affected systems.

**Key things to implement:**
- System prompt with role + output format (JSON)
- 3 few-shot examples covering edge cases
- XML tags around the input to prevent injection
- Retry logic on malformed output

**🔨 10x productivity bonus:** Point it at your Slack/email and auto-generate your weekly status update.

---

## Stage 3 — Tool Use & Function Calling ⭐
**⏱ Time:** 1 week | **🔁 Backend Analogy:** Webhook handlers where the caller is AI
> **🎯 PIVOT POINT — master this and everything else follows**

### What is this stage?

Function calling (aka tool use) is the bridge between "chatbot" and "agent." You define function schemas (name, description, typed parameters). The LLM decides when to call them and with what arguments. Your code executes the function and returns the result. The LLM continues reasoning.

### Why it matters (2-year outlook)

Every microservice you build in the future will need an AI-callable interface. Just as REST made services accessible to other services, function calling schemas (and MCP, which is the standardized networked version — Stage 7) will make services accessible to AI agents. Understanding this primitive now means you'll be architecting these interfaces at your company while others are still catching up.

### Core concepts explained

**The tool-use loop**
1. You call the LLM with a user message + a list of available tools
2. LLM returns either a text response OR a `tool_use` request with arguments
3. Your code executes the tool; captures the result
4. You call the LLM again with the original messages + tool result
5. LLM uses the result to produce a final answer (or request another tool)

**Function schemas**  
A JSON Schema describing each function: name, description (the LLM reads this!), parameters, types, required fields. **The description is critical — it's how the model knows when to use the tool.** Treat it like docstring writing on steroids.

**Parallel tool calls**  
Modern models can request multiple tools in a single response (e.g., "check weather in Paris AND search flights simultaneously"). Support this with concurrent execution.

**Tool result validation**  
Always validate tool outputs before feeding back to the model. If a tool errored, return a structured error message — the LLM can often self-correct.

**Max tool turns**  
Always cap the number of tool-use iterations (e.g., 10) to prevent infinite loops. This is your circuit breaker.

**ReAct pattern**  
Reason + Act. The LLM is prompted to alternate between "thinking" steps and tool calls. Most agent frameworks implement some form of this.

### 📚 Resources

**Docs (the highest-quality learning material for this topic)**
- [Anthropic Tool Use Docs](https://docs.anthropic.com/en/docs/build-with-claude/tool-use/overview) ⭐ start here
- [OpenAI Function Calling Guide](https://platform.openai.com/docs/guides/function-calling)
- [Anthropic — How Tool Use Works](https://docs.anthropic.com/en/docs/build-with-claude/tool-use/how-tool-use-works)

**Courses**
- 🎓 [DeepLearning.AI — Functions, Tools and Agents with LangChain](https://www.deeplearning.ai/short-courses/functions-tools-agents-langchain/) — free, 2hrs

**Video Resources**
- 📹 [Fireship YouTube Channel](https://www.youtube.com/@Fireship) — search "AI agents" or "function calling"
- 📹 [LangChain Channel](https://www.youtube.com/@LangChain) — search "tool use"
- 📹 [James Briggs](https://www.youtube.com/@jamesbriggs) — deep tutorials on agents and tools

### 🐙 GitHub References

- [anthropics/anthropic-cookbook — tool_use](https://github.com/anthropics/anthropic-cookbook/tree/main/tool_use) ⭐ official examples
- [openai/openai-cookbook — Function calling examples](https://github.com/openai/openai-cookbook/tree/main/examples) 
- [anthropics/courses](https://github.com/anthropics/courses) — Anthropic's course material

### 🔨 Build: DevOps Agent with Real Tools

An agent with tools mapped to real backend ops:
- `query_database(sql)` — run a SELECT on a read-replica
- `check_service_health(service)` — hit a health endpoint
- `read_logs(service, minutes)` — fetch recent logs
- `get_recent_deploys(service, hours)` — recent deployment history
- `create_jira_ticket(title, description)` — file a ticket

Ask it: *"Why is the payment service slow today?"* Watch it chain tools together to investigate.

This is far closer to production-grade agent work than most tutorials show.

---

## Stage 4 — Structured Outputs + Pydantic
**⏱ Time:** 3–4 days | **🔁 Backend Analogy:** Type-safe API responses

### What is this stage?

Make LLM outputs as reliable as typed API contracts. The `instructor` library wraps any LLM API and forces output to conform to a Pydantic schema — with automatic retries on validation failure.

### Why it matters (2-year outlook)

Production AI systems are built on reliable data contracts, not vibes. As agents move from "impressive demos" to "critical infrastructure," structured outputs become the baseline — not the exception.

### Core concepts explained

**The problem with free-text LLM outputs**  
LLMs occasionally produce malformed JSON, extra commentary, or slightly wrong field names. In production, this breaks downstream code unpredictably. You need validation, retries, and type safety.

**Native structured output modes**  
Both OpenAI (`response_format={"type":"json_schema"}`) and Anthropic (via tool use) now offer native structured output enforcement. The model is *constrained* at generation time to produce valid JSON matching your schema. This is more reliable than prompting alone.

**Pydantic as the schema source of truth**  
Define one Pydantic model → get JSON schema for the LLM → get runtime validation → get type hints in your IDE. Single source of truth.

**The `instructor` library**  
A thin wrapper around OpenAI/Anthropic/etc. that: (1) accepts a Pydantic model, (2) generates the schema for the LLM, (3) validates the response, (4) retries with error feedback if validation fails. Makes structured extraction trivial.

**Nested schemas & unions**  
You can model complex data — lists, nested objects, discriminated unions (using `Literal` types for tags). The LLM handles them well.

### 📚 Resources

**Docs**
- [Instructor Library Docs](https://python.useinstructor.com/) ⭐ clearest docs in the AI ecosystem
- [Pydantic Docs](https://docs.pydantic.dev/) — foundation library
- [OpenAI Structured Outputs](https://platform.openai.com/docs/guides/structured-outputs) — native mode

**Articles**
- [Jason Liu's Blog — jxnl.co](https://jxnl.co/writing/) ⭐ best engineering-focused AI writing online
- [Instructor — Why Structured Outputs?](https://python.useinstructor.com/why/)

**Video Resources**
- 📹 [Jason Liu YouTube](https://www.youtube.com/@jxnlco) — author of instructor
- 📹 Search "instructor pydantic llm" on YouTube for walkthroughs

### 🐙 GitHub References

- [jxnl/instructor](https://github.com/jxnl/instructor) ⭐ THE library
- [jxnl/instructor examples](https://github.com/jxnl/instructor/tree/main/examples) — production-ready patterns
- [pydantic/pydantic](https://github.com/pydantic/pydantic)
- [pydantic/pydantic-ai](https://github.com/pydantic/pydantic-ai) — newer agent framework built on Pydantic

### 🔨 Build: Incident Analyzer

Paste a raw PagerDuty alert or incident report. Extract structured fields as typed Pydantic objects:
- severity (enum)
- affected_services (list)
- root_cause_hypothesis (str)
- suggested_actions (list of action objects with priority + owner)
- similar_past_incidents (list, from RAG later)

Pipe the output to Slack as a formatted message.

---

## Stage 5 — RAG & Vector Search
**⏱ Time:** 1–2 weeks | **🔁 Backend Analogy:** Semantic search index

### What is this stage?

RAG (Retrieval-Augmented Generation) is the pattern of: **find relevant knowledge → inject into prompt → generate answer.** It lets LLMs reason over your private data without retraining.

### Why it matters (2-year outlook)

Vector search is being built into every major database — `pgvector` for Postgres, Elastic, MongoDB, Redis all now support it. In 2 years, adding semantic search will be as routine as adding full-text search. Understanding the fundamentals now means you'll implement it correctly while others cargo-cult bad patterns.

### Core concepts explained

**Embeddings = semantic hash functions**  
An embedding model converts text into a fixed-size vector (e.g., 1536 dimensions). Texts with similar meanings produce vectors that are close in vector space. This enables **semantic search** — "find text that *means* the same thing," not "find text with the same words."

**Cosine similarity**  
The standard metric for comparing embeddings. Range: -1 to 1. Closer to 1 = more similar. Most vector DBs use cosine similarity or (mathematically equivalent for normalized vectors) dot product / Euclidean distance.

**Vector databases**  
Specialized indexes for fast similarity search. They use algorithms like HNSW (Hierarchical Navigable Small World) to avoid comparing against every vector. Same conceptual role as a B-tree for range queries — just optimized for a different distance function.

**The RAG pipeline**
1. **Ingestion:** Split documents into chunks → embed each chunk → store in vector DB with metadata
2. **Retrieval:** Embed the user query → similarity search → get top-k chunks
3. **Generation:** Inject retrieved chunks into the prompt → LLM generates grounded answer

**Chunking strategy**  
How you split documents matters enormously. Fixed-size chunks lose context. Semantic chunking (by paragraph/section) is better. Recursive chunking with overlap is a solid default. Experiment.

**Hybrid search**  
Pure vector search misses exact matches (product codes, names). Pure keyword search misses semantic matches. Hybrid = both, merged with reciprocal rank fusion. Almost always better than either alone.

**Reranking**  
After retrieval, use a stronger (slower) model to rerank the top-k results. Libraries: Cohere Rerank, cross-encoders from sentence-transformers.

**Evaluation: RAGAS**  
Measure RAG quality with metrics like **faithfulness** (does the answer stay grounded in retrieved context?), **answer relevance**, **context precision/recall**.

### 📚 Resources

**Docs**
- [pgvector GitHub README](https://github.com/pgvector/pgvector) ⭐ add vector search to Postgres
- [Chroma Docs](https://docs.trychroma.com/) — easiest local vector DB
- [LangChain RAG Tutorial](https://python.langchain.com/docs/tutorials/rag/)
- [LlamaIndex Docs](https://docs.llamaindex.ai/) — RAG-focused framework

**Courses & Articles**
- 🎓 [DeepLearning.AI — Building and Evaluating Advanced RAG](https://www.deeplearning.ai/short-courses/building-evaluating-advanced-rag/) — free
- 🎓 [DeepLearning.AI — LangChain: Chat with Your Data](https://www.deeplearning.ai/short-courses/langchain-chat-with-your-data/) — free
- [Eugene Yan — RAG Patterns](https://eugeneyan.com/writing/llm-patterns/) — engineering-focused writeup

**Video Resources**
- 📹 [LangChain — RAG from Scratch Playlist](https://www.youtube.com/playlist?list=PLfaIDFEXuae2LXbO1_PKyVJiQ23ZztA0x) ⭐ **gold standard** walkthrough
- 📹 [Greg Kamradt YouTube](https://www.youtube.com/@DataIndependent) — RAG deep dives
- 📹 [Fireship — Vector Databases in 100 Seconds](https://www.youtube.com/@Fireship) — search "vector database"

### 🐙 GitHub References

- [pgvector/pgvector](https://github.com/pgvector/pgvector) ⭐ Postgres extension
- [chroma-core/chroma](https://github.com/chroma-core/chroma) — local vector DB
- [langchain-ai/rag-from-scratch](https://github.com/langchain-ai/rag-from-scratch) ⭐ excellent walkthrough
- [run-llama/llama_index](https://github.com/run-llama/llama_index) — RAG framework
- [weaviate/weaviate](https://github.com/weaviate/weaviate) — production vector DB
- [qdrant/qdrant](https://github.com/qdrant/qdrant) — Rust vector DB
- [explodinggradients/ragas](https://github.com/explodinggradients/ragas) — RAG eval

### 🔨 Build: Chat With Your Codebase

1. Clone a GitHub repo you work on
2. Chunk and embed all source files (use AST-aware chunking for code — chunk by function/class)
3. Store in **pgvector** (use your existing Postgres — teach yourself the extension)
4. Build a CLI that answers questions: "Where is authentication handled?", "How does the payment retry logic work?", "Who last modified the user service?"

Extend with: git metadata (author, last modified), hybrid search (embeddings + BM25), reranking.

---

## Stage 6 — Agent Frameworks (LangGraph)
**⏱ Time:** 2 weeks | **🔁 Backend Analogy:** State machine / workflow engine with AI decision nodes

### What is this stage?

**Skip deep LangChain — go straight to LangGraph.** LangGraph models agents as **directed graphs**: nodes are steps (LLM calls, tool calls, business logic), edges are transitions (with conditional routing). This maps beautifully to state machines and workflow engines you've already designed.

### Why it matters (2-year outlook)

Most complex business logic that today lives in hardcoded services will shift to agent-orchestrated workflows. Engineers who can design, debug, and maintain those workflows will own a critical part of the stack. LangGraph is the most production-ready framework in the ecosystem and the direction the industry is moving.

### Core concepts explained

**State**  
A typed dictionary (Pydantic model or TypedDict) that flows through the graph. Each node reads state, updates it, and passes it forward. This gives agents memory and inspectability.

**Nodes**  
Functions that take state → return state updates. Can be: LLM calls, tool executions, Python logic, sub-agents.

**Edges**  
Control flow. Static edges always transition A→B. **Conditional edges** branch based on state (e.g., "if agent decided to use a tool, go to tool node; else end").

**Cycles & loops**  
Unlike DAG-only workflow engines, LangGraph supports cycles — essential for ReAct-style reasoning (think → act → observe → think → …).

**Checkpointing & persistence**  
LangGraph can checkpoint state to a database after every node. This enables: pausing, resuming, time-travel debugging, human-in-the-loop approvals, and durability across restarts. This is the feature that makes LangGraph production-ready.

**Human-in-the-loop**  
You can pause the graph before destructive actions, request human approval, and resume. Essential for high-stakes agents.

**Subgraphs & multi-agent orchestration**  
Compose agents hierarchically — an "orchestrator" graph that delegates to "worker" subgraphs. This is your entry point to Stage 10.

### 📚 Resources

**Docs**
- [LangGraph Official Tutorials](https://langchain-ai.github.io/langgraph/tutorials/introduction/) ⭐ start here
- [LangGraph How-to Guides](https://langchain-ai.github.io/langgraph/how-tos/) — copy-paste patterns
- [LangGraph Conceptual Guide](https://langchain-ai.github.io/langgraph/concepts/)

**Courses**
- 🎓 [DeepLearning.AI — AI Agents in LangGraph](https://www.deeplearning.ai/short-courses/ai-agents-in-langgraph/) — free, best structured course

**Video Resources**
- 📹 [LangChain YouTube Channel](https://www.youtube.com/@LangChain) ⭐ frequent LangGraph tutorials
- 📹 [LangGraph Playlist on LangChain channel](https://www.youtube.com/@LangChain/playlists) — look for LangGraph playlists
- 📹 [Harrison Chase (LangChain CEO) talks](https://www.youtube.com/@LangChain/videos) — foundational talks on agent design

### 🐙 GitHub References

- [langchain-ai/langgraph](https://github.com/langchain-ai/langgraph) ⭐ main repo
- [langchain-ai/langgraph — examples](https://github.com/langchain-ai/langgraph/tree/main/examples) — official examples
- [langchain-ai/langchain](https://github.com/langchain-ai/langchain) — parent framework
- [von-development/awesome-LangGraph](https://github.com/von-development/awesome-LangGraph) — community resources

### 🔨 Build: Automated Incident Response Agent

When an alert arrives, the agent:
1. Checks service health endpoints
2. Queries recent logs (last 15 min)
3. Checks deployment history (last 24h)
4. Cross-references against your runbook (RAG over markdown docs)
5. Drafts a triage report with severity, hypothesis, and recommended actions
6. Pauses for human approval before filing a Jira ticket or paging on-call

Covers: state design, conditional routing, tool use, RAG integration, human-in-the-loop.

---

## Stage 7 — MCP Servers ⭐
**⏱ Time:** 1–2 weeks | **🔁 Backend Analogy:** Building the AI interface layer of your backend services
> **🎯 CAREER INFLECTION POINT for backend engineers**

### What is this stage?

MCP (**Model Context Protocol**) is the emerging open standard for how AI agents connect to external tools, data, and templates. Think "USB-C for AI agents" — a standardized connector that works across Claude, ChatGPT (via adapters), IDEs, and custom agents.

### Why it matters (2-year outlook)

Just as REST became the standard interface between services, MCP is becoming the standard interface between AI agents and services. In 2 years, you'll likely be building these at your company. **Your existing backend services can each become an MCP server — once wrapped, any AI agent can use them.** You're not learning a new technology from scratch; you're adding an AI-callable layer to things you've already built.

### Core concepts explained

**The three MCP primitives**
- **Tools** — Functions the AI can invoke (e.g., `create_ticket`, `deploy_service`). Similar to function calling, but standardized.
- **Resources** — Data the AI can read (files, DB rows, configs). Exposed as URIs the model can request.
- **Prompts** — Reusable prompt templates the host application can offer users (e.g., "Summarize this Jira epic").

**Transports**
- **stdio** — Local: the MCP server runs as a subprocess of the host (Claude Desktop, Cursor). Easy to develop.
- **SSE / HTTP** — Remote: the MCP server is a networked service. Required for production agents and multi-user systems.

**Hosts, clients, servers**  
- **Host** = the AI app (Claude Desktop, Cursor)
- **Client** = the component inside the host that talks MCP
- **Server** = your code exposing tools/resources/prompts

**Discovery**  
An MCP client asks a server "what tools/resources/prompts do you offer?" The server returns schemas. The host then injects these into the model's context on demand.

**Security considerations**
- MCP servers often run with user credentials — scope permissions carefully
- Treat all data returned from MCP servers as potentially adversarial (prompt injection, Stage 8)
- For SSE/HTTP servers, authenticate and authorize properly

### 📚 Resources

**Docs**
- [Official MCP Docs](https://modelcontextprotocol.io/introduction) ⭐ spec + quickstarts — start here
- [MCP Python Quickstart](https://modelcontextprotocol.io/quickstart/server)
- [MCP Specification](https://modelcontextprotocol.io/specification) — the full protocol

**Video Resources**
- 📹 [Anthropic YouTube Channel](https://www.youtube.com/@anthropic-ai) — search "MCP"
- 📹 [Matt Pocock YouTube](https://www.youtube.com/@mattpocockuk) — MCP tutorials
- 📹 YouTube search: ["MCP server tutorial python"](https://www.youtube.com/results?search_query=MCP+server+tutorial+python) — active topic with many new videos

### 🐙 GitHub References

- [modelcontextprotocol/python-sdk](https://github.com/modelcontextprotocol/python-sdk) ⭐ official SDK
- [modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers) ⭐ **reference servers** (filesystem, GitHub, Postgres, Slack, etc.) — study these first
- [modelcontextprotocol/typescript-sdk](https://github.com/modelcontextprotocol/typescript-sdk) — TS alternative
- [modelcontextprotocol/inspector](https://github.com/modelcontextprotocol/inspector) — debugging tool
- [punkpeye/awesome-mcp-servers](https://github.com/punkpeye/awesome-mcp-servers) — curated list
- [wong2/awesome-mcp-servers](https://github.com/wong2/awesome-mcp-servers) — alternative list

### 🔨 Build Sequence (in order)

**1. Wrap a public API as MCP**  
Pick an API you know well (GitHub, Notion, Linear, Jira). Expose 3–5 endpoints as MCP tools. Install locally in Claude Desktop. Have a conversation with your API.

**2. Postgres-as-resource MCP server**  
Expose a read-only DB (or read-replica) as MCP **resources**. Let Claude query tables conversationally. This is shockingly useful for on-call debugging.

**3. Deployment pipeline MCP (advanced)**  
Tools for: trigger deploy, check status, rollback, read deploy logs. Ship with careful permission scoping. This is the portfolio-worthy project — genuinely useful at any backend shop.

**Reference servers to study:**
- [Filesystem MCP Server](https://github.com/modelcontextprotocol/servers/tree/main/src/filesystem)
- [GitHub MCP Server](https://github.com/modelcontextprotocol/servers/tree/main/src/github)
- [Postgres MCP Server](https://github.com/modelcontextprotocol/servers/tree/main/src/postgres)
- [Slack MCP Server](https://github.com/modelcontextprotocol/servers/tree/main/src/slack)

---

## Stage 8 — AI-Native Backend Patterns
**⏱ Time:** 1–2 weeks | **🔁 Backend Analogy:** Distributed systems patterns, for AI

### What is this stage?

Build backend systems *designed for AI from the ground up* — not retrofitted. The new patterns: streaming APIs, agent state persistence, async execution, prompt injection defense.

### Why it matters (2-year outlook)

Naïve AI integrations (sync HTTP calls wrapping an LLM) hit scalability and reliability walls fast. The engineers who understand these patterns will build AI systems that actually work in production — and get promoted for it.

### Core concepts explained

**Streaming responses (SSE / WebSockets)**  
LLMs produce output token-by-token. Users hate waiting 15 seconds for a complete response. Stream tokens as they're generated over **Server-Sent Events** (simpler, one-way) or WebSockets (bidirectional). Buffer on the server, flush to client. Handle client disconnects gracefully.

**Async agent execution**  
Long-running agents (minutes to hours) can't be synchronous HTTP. Pattern: POST kicks off an async job → returns job ID → agent runs in background (Celery/ARQ/BullMQ) → client polls or listens on websocket for updates. Exactly like any other long-running backend job.

**State persistence & checkpointing**  
Agents must survive process restarts, crashes, and deployment. Checkpoint state after every step to Postgres/Redis. LangGraph handles this natively.

**Idempotency**  
Because agents retry, because humans re-run, because distributed systems are messy — every tool must be idempotent or have idempotency keys. Same rules you already apply to payment APIs.

**Prompt injection defense**  
The "SQL injection" of AI. A malicious document in your RAG corpus, a malicious web page your agent reads, a malicious email — any of these can contain instructions that hijack the model. Mitigations:
- Treat all retrieved content as **untrusted data**, never as instructions
- Use tool-use schemas (the model can only invoke *your* defined tools)
- Sandbox destructive actions behind human approval
- Detect prompt injection patterns (e.g., Rebuff library)
- Constrain privileges — agents should run with minimal permissions

**Cost & latency controls**
- Token budgets per user/request
- Model routing — cheap model for simple tasks, expensive model for complex
- Response caching (semantic cache: similar queries → cached response)
- Timeouts and circuit breakers around LLM calls

### 📚 Resources

**Docs & Articles**
- [LangGraph Persistence](https://langchain-ai.github.io/langgraph/concepts/persistence/) — checkpointing
- [Streaming with Anthropic API](https://docs.anthropic.com/en/api/messages-streaming)
- [Streaming with OpenAI API](https://platform.openai.com/docs/api-reference/streaming)
- [OWASP LLM Top 10](https://owasp.org/www-project-top-10-for-large-language-model-applications/) ⭐ AI security essentials
- [Eugene Yan — Patterns for Building LLM Systems](https://eugeneyan.com/writing/llm-patterns/) ⭐ must-read
- [Anthropic — Prompt Injection](https://docs.anthropic.com/en/docs/test-and-evaluate/strengthen-guardrails/mitigate-jailbreaks)

**Video Resources**
- 📹 [Fireship YouTube](https://www.youtube.com/@Fireship) — search "SSE" and "WebSockets" refreshers
- 📹 [LangChain Channel](https://www.youtube.com/@LangChain) — search "persistence" and "streaming"

### 🐙 GitHub References

- [langfuse/langfuse](https://github.com/langfuse/langfuse) — open-source LLM engineering platform
- [Arize-ai/phoenix](https://github.com/Arize-ai/phoenix) — LLM observability
- [protectai/rebuff](https://github.com/protectai/rebuff) — prompt injection detection
- [NVIDIA/NeMo-Guardrails](https://github.com/NVIDIA/NeMo-Guardrails) — guardrails framework

### 🔨 Build: Async Long-Running Agent

Full stack:
- **API:** `POST /agents/research` → returns `job_id`
- **Worker:** Background worker picks up the job, runs a LangGraph agent that checkpoints to Postgres after every node
- **Streaming:** `GET /agents/:job_id/stream` → SSE endpoint that streams agent progress as it happens
- **Security:** Sandbox any tool that could be exploited by retrieved content; rate-limit; auth
- **Observability:** Full tracing via Langfuse or LangSmith

This is production-grade agent infrastructure — genuinely a portfolio piece.

---

## Stage 9 — LLMOps & Evals
**⏱ Time:** 1 week | **🔁 Backend Analogy:** Observability + SRE for AI

### What is this stage?

Evals are test suites for AI behavior. LLMOps is the broader practice of deploying, monitoring, and maintaining LLM systems in production. Without this, you're shipping on vibes. With this, you have regression detection, performance benchmarks, and confidence in changes.

### Why it matters (2-year outlook)

Every company running AI in production will need engineers who can monitor model behavior, detect drift, A/B test prompts, and maintain eval suites. This is a natural extension of your SRE/platform-engineering instincts.

### Core concepts explained

**Types of evals**
- **Unit evals** — does this specific prompt produce this specific output? (deterministic, for regression)
- **Behavioral evals** — does the agent take reasonable actions on this scenario? (probabilistic, run many trials)
- **LLM-as-judge** — use a strong LLM to score outputs on rubrics. Cheaper than human rating; more reliable than regex.
- **Human evals** — gold standard for subjective quality; expensive but necessary for the first ~100 examples to calibrate.

**Eval datasets**  
A collection of (input, expected behavior) pairs. Treat like a test fixture. Add examples from real user traffic (especially failures) — this is your regression suite.

**Metrics**
- **Accuracy** — for classification/extraction tasks
- **Faithfulness** — does the answer stay grounded in context? (for RAG)
- **Context precision/recall** — did retrieval find the right chunks?
- **Task completion rate** — did the agent actually do the job?

**Tracing & observability**  
Every LLM call, every tool call, every agent step should produce a trace. You want to be able to open up any failed run and see exactly what happened. Tools: Langfuse (open source), LangSmith, Braintrust, Arize Phoenix.

**A/B testing prompts**  
Treat prompt changes like code changes. Run them against your eval set, compare metrics, deploy gradually.

**Model routing & fallbacks**  
Route easy queries to cheap models (Haiku, GPT-4o-mini), hard ones to expensive models (Opus, GPT-4). Build fallback chains for provider outages.

### 📚 Resources

**Docs**
- [RAGAS Framework Docs](https://docs.ragas.io/) ⭐ de facto RAG eval standard
- [Braintrust Docs](https://www.braintrustdata.com/docs)
- [LangSmith Docs](https://docs.smith.langchain.com/)
- [Langfuse Docs](https://langfuse.com/docs) — open source

**Articles**
- [Eugene Yan — LLM Evaluation](https://eugeneyan.com/writing/evals/) ⭐
- [Hamel Husain — Your AI Product Needs Evals](https://hamel.dev/blog/posts/evals/) ⭐ MUST READ
- [Jason Liu — Low Hanging Fruit for RAG](https://jxnl.co/writing/2024/02/28/levels-of-complexity-rag-applications/)

**Video Resources**
- 📹 [Hamel Husain YouTube](https://www.youtube.com/@hamelhusain) — eval talks
- 📹 [DeepLearning.AI](https://www.youtube.com/@Deeplearningai) — search "evaluation"

### 🐙 GitHub References

- [explodinggradients/ragas](https://github.com/explodinggradients/ragas) ⭐ RAG eval
- [openai/evals](https://github.com/openai/evals)
- [confident-ai/deepeval](https://github.com/confident-ai/deepeval) — pytest-style LLM testing
- [langfuse/langfuse](https://github.com/langfuse/langfuse) ⭐ open-source LLM ops
- [Helicone/helicone](https://github.com/Helicone/helicone) — LLM monitoring
- [Arize-ai/phoenix](https://github.com/Arize-ai/phoenix) — open-source observability

### 🔨 Build: Eval Suite for Your Incident Response Agent

Take your Stage 6 agent:
1. Create 20 test scenarios (synthetic incidents with expected behaviors)
2. Define metrics: "did it query logs?", "did it check recent deploys?", "did the hypothesis match?"
3. Implement LLM-as-judge for open-ended scoring
4. Wire into CI — every agent change runs the eval, PRs are blocked if scores regress
5. Instrument full tracing with Langfuse

This is the thing that separates production-quality work from demos.

---

## Stage 10 — Multi-Agent Systems
**⏱ Time:** 2 weeks | **🔁 Backend Analogy:** Microservices, where agents are the services

### What is this stage?

Coordinate multiple specialized agents via shared protocols. Orchestrator (like an API gateway) routes tasks to worker agents (like microservices). The same distributed systems thinking applies — failures, retries, timeouts, partial-failure handling.

### Why it matters (2-year outlook)

Complex business workflows currently requiring human coordination (customer onboarding, code reviews, content moderation, incident triage) will increasingly be handled by multi-agent systems. Engineers who can design, deploy, and maintain them work on the frontier — but with patterns borrowed directly from distributed systems.

### Core concepts explained

**Orchestrator + workers pattern**  
One manager agent decomposes tasks, routes to specialists, aggregates results. Specialists are narrow and expert (security reviewer, performance reviewer, etc.). Same pattern as API gateway + microservices.

**Agent-to-agent communication**  
Structured messages (Pydantic models), not free text. Define contracts. Think of it as gRPC between agents.

**Supervisor pattern (LangGraph)**  
A supervisor node inspects state and routes to the next worker. Workers return results; supervisor decides whether to continue or finish.

**Hierarchical teams**  
Orchestrators of orchestrators. Useful for large tasks — a "research team" sub-orchestrator coordinates 3 research agents, reports back to the top-level planner.

**Shared memory**  
Agents often need to share intermediate findings. Use a shared state store (Postgres, Redis), not message passing, for anything non-trivial.

**Failure handling**  
Specialists can fail (LLM errors, tool errors, bad outputs). Orchestrator should retry, fall back, or mark the task partial. Partial failure is the norm.

**Cost control**  
Multi-agent systems can easily 10x your LLM spend if unbounded. Set hard limits on agent-turns, enforce token budgets per task.

### 📚 Resources

**Docs**
- [LangGraph Multi-Agent Architecture](https://langchain-ai.github.io/langgraph/concepts/multi_agent/)
- [AutoGen Docs (Microsoft)](https://microsoft.github.io/autogen/)
- [CrewAI Docs](https://docs.crewai.com/)

**Courses**
- 🎓 [DeepLearning.AI — Multi AI Agent Systems with crewAI](https://www.deeplearning.ai/short-courses/multi-ai-agent-systems-with-crewai/) — free
- 🎓 [DeepLearning.AI — AI Agentic Design Patterns with AutoGen](https://www.deeplearning.ai/short-courses/ai-agentic-design-patterns-with-autogen/)

**Video Resources**
- 📹 [DeepLearning.AI YouTube](https://www.youtube.com/@Deeplearningai) — Andrew Ng's agentic design patterns talks
- 📹 [LangChain YouTube Channel](https://www.youtube.com/@LangChain) — search "multi-agent"

### 🐙 GitHub References

- [joaomdmoura/crewAI](https://github.com/joaomdmoura/crewAI) ⭐ popular multi-agent framework
- [joaomdmoura/crewAI-examples](https://github.com/joaomdmoura/crewAI-examples)
- [microsoft/autogen](https://github.com/microsoft/autogen) ⭐ Microsoft's framework
- [langchain-ai/langgraph — multi-agent examples](https://github.com/langchain-ai/langgraph/tree/main/examples/multi_agent)
- [OpenBMB/ChatDev](https://github.com/OpenBMB/ChatDev) — multi-agent software company simulation
- [geekan/MetaGPT](https://github.com/geekan/MetaGPT) — multi-agent software dev

### 🔨 Build: PR Review Pipeline (Multi-Agent)

Trigger on new PR:
- **Orchestrator agent** reads the diff + PR description
- **Security agent** checks for vulnerabilities (SQLi, secrets, unsafe deps)
- **Performance agent** checks for N+1 queries, inefficient loops, etc.
- **Test coverage agent** checks whether new code is adequately tested
- **Style agent** checks conventions vs. your codebase
- Orchestrator aggregates findings → posts a structured GitHub review comment

Real, portfolio-worthy, immediately useful at any company.

---

## Staying Current

### Must-follow sources

| Source | Why | Format |
|---|---|---|
| [Latent Space Podcast](https://www.latent.space/) | Deep technical interviews with AI engineers | Podcast |
| [TLDR AI Newsletter](https://tldr.tech/ai) | 5-min daily digest, high signal | Email |
| [Simon Willison's Blog](https://simonwillison.net/) | Pragmatic AI engineering | Blog |
| [Jason Liu's Blog](https://jxnl.co/writing/) | Applied AI patterns | Blog |
| [Eugene Yan's Blog](https://eugeneyan.com/) | Applied ML/LLM systems | Blog |
| [Hamel Husain's Blog](https://hamel.dev/) | Evals, production AI | Blog |
| [Lilian Weng's Blog](https://lilianweng.github.io/) | Research-level depth | Blog |
| [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA) | Open-source AI community | Reddit |
| [Hacker News](https://news.ycombinator.com/) | General tech + AI news | Site |
| [Papers With Code](https://paperswithcode.com/) | Research + implementations | Site |
| [Anthropic Research](https://www.anthropic.com/research) | Frontier safety/capability work | Blog |

### Essential papers (1 per week)

- **Attention Is All You Need** — [arxiv.org/abs/1706.03762](https://arxiv.org/abs/1706.03762) — foundational
- **Chain-of-Thought Prompting** — [arxiv.org/abs/2201.11903](https://arxiv.org/abs/2201.11903)
- **ReAct: Synergizing Reasoning and Acting** — [arxiv.org/abs/2210.03629](https://arxiv.org/abs/2210.03629)
- **Toolformer** — [arxiv.org/abs/2302.04761](https://arxiv.org/abs/2302.04761)
- **RAG (Retrieval-Augmented Generation)** — [arxiv.org/abs/2005.11401](https://arxiv.org/abs/2005.11401)
- **Self-RAG** — [arxiv.org/abs/2310.11511](https://arxiv.org/abs/2310.11511)
- **Constitutional AI** — [arxiv.org/abs/2212.08073](https://arxiv.org/abs/2212.08073)

### YouTube channels worth subscribing to

- [Andrej Karpathy](https://www.youtube.com/@AndrejKarpathy) — foundational lectures
- [3Blue1Brown](https://www.youtube.com/@3blue1brown) — visual math/ML intuition
- [LangChain](https://www.youtube.com/@LangChain) — agent framework tutorials
- [DeepLearning.AI](https://www.youtube.com/@Deeplearningai) — official course content
- [Fireship](https://www.youtube.com/@Fireship) — concise engineering takes
- [Matt Pocock](https://www.youtube.com/@mattpocockuk) — TypeScript + AI
- [James Briggs](https://www.youtube.com/@jamesbriggs) — applied LLM tutorials
- [Jason Liu](https://www.youtube.com/@jxnlco) — structured outputs, RAG
- [AI Engineer (conference channel)](https://www.youtube.com/@aiDotEngineer) — production AI talks

---

## Timeline & Portfolio Checklist

### Recommended 15-week timeline

```
Week 1-2:     Stage 0 (daily, forever) + Stage 1 (LLM Internals)
Week 3:       Stage 2 (Context Engineering)
Week 4:       Stage 3 (Tool Use) ⭐ pivot point
Week 5:       Stage 4 (Structured Outputs)
Week 6-7:     Stage 5 (RAG + pgvector)
Week 8-9:     Stage 6 (LangGraph)
Week 10-11:   Stage 7 (MCP Servers) ⭐ career inflection
Week 12:      Stage 8 (AI-Native Backend Patterns)
Week 13:      Stage 9 (LLMOps + Evals)
Week 14-15:   Stage 10 (Multi-Agent Systems)
Ongoing:      Weekly paper + daily TLDR AI + monthly portfolio update
```

**~3 months of consistent evenings/weekends.** Productivity gains from Stage 0 start immediately — don't wait for the rest.

### Portfolio checklist

By the end, you should have pushed these to GitHub:

- [ ] Raw HTTP chatbot (no SDKs, no frameworks)
- [ ] Structured data extractor for messy text
- [ ] DevOps agent with real tools (function calling)
- [ ] Incident analyzer (Instructor + Pydantic)
- [ ] "Chat with your codebase" RAG app using pgvector
- [ ] Automated incident response agent (LangGraph)
- [ ] At least 2 custom MCP servers (real APIs wrapped)
- [ ] Long-running async agent with state persistence + streaming
- [ ] Eval suite for one of the above agents (CI-integrated)
- [ ] Multi-agent PR review pipeline

---

## The Career Inflection Point

The engineers who will be most valuable in 2 years aren't the ones who learned the most AI theory — they're the ones who combined solid backend engineering fundamentals with AI fluency.

**You already have the hard part.** This path is the bridge.

The profile in extreme demand:

> *A backend engineer who can design agent-based systems, build MCP servers to connect them to business data, deploy them reliably with evals and monitoring, and reason about failure modes like a distributed systems engineer.*

That's exactly what this path builds toward.

---

## 📝 Note on Video Links

YouTube URLs occasionally change or get removed. To maximize durability, this document prioritizes:

1. **Channel URLs** — stable as long as the creator exists
2. **Well-known canonical videos** — e.g., Karpathy's "Intro to LLMs" (`zjkBMFhNj_g`), `nanoGPT` lecture (`kCc8FmEb1nY`), and 3Blue1Brown's GPT explainer
3. **Playlist URLs** — relatively stable
4. **Search URLs** — guaranteed to find something relevant

If any specific video link is broken, search the channel by the topic name — the content almost always still exists under a different URL.

---

*Compiled April 2026. Use this as your go-to reference — it's designed to stand alone.*
