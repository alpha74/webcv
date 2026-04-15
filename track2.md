# 🚀 AI Learning Path for Backend Engineers

Source: Claude

> **Built for the next 2 years, not just today.** A hands-on roadmap for backend engineers (4-5y exp) to become AI engineers — with resources, GitHub projects, and build tutorials for every stage.

---

## Table of Contents
- [The Big Picture](#the-big-picture)
- [Stage 0 — 10x Your Daily Work NOW](#stage-0--10x-your-daily-work-now)
- [Stage 1 — LLM Internals](#stage-1--llm-internals)
- [Stage 2 — Context Engineering](#stage-2--context-engineering)
- [Stage 3 — Tool Use & Function Calling ⭐](#stage-3--tool-use--function-calling-)
- [Stage 4 — Structured Outputs + Pydantic](#stage-4--structured-outputs--pydantic)
- [Stage 5 — RAG & Vector Search](#stage-5--rag--vector-search)
- [Stage 6 — Agent Frameworks (LangGraph)](#stage-6--agent-frameworks-langgraph)
- [Stage 7 — MCP Servers ⭐](#stage-7--mcp-servers-)
- [Stage 8 — AI-Native Backend Patterns](#stage-8--ai-native-backend-patterns)
- [Stage 9 — LLMOps & Evals](#stage-9--llmops--evals)
- [Stage 10 — Multi-Agent Systems](#stage-10--multi-agent-systems)
- [Staying Current](#staying-current)
- [Recommended Timeline](#recommended-timeline)

---

## The Big Picture

In 2 years, backend engineering will split into two tracks:
1. Engineers who build **systems that use AI** as a component (agents, pipelines, tools)
2. Engineers who build **the AI infrastructure itself** (model serving, training infra)

This path targets track 1 — the larger and more immediately valuable path. Your existing backend skills (APIs, databases, async systems, reliability engineering) are directly transferable.

**The key insight:** AI agents are becoming a new kind of microservice. Your job as a backend engineer is increasingly to build the infrastructure *around* these agents — memory systems, tool servers, orchestration layers, evaluation pipelines, and reliability guarantees.

---

## Stage 0 — 10x Your Daily Work NOW
*Start immediately, parallel to everything else*

Before learning to *build* AI systems, use AI systems daily. Switch your editor, use AI as a pair programmer, change your workflow.

### Resources
- 📹 [Cursor Tutorial for Developers](https://www.youtube.com/watch?v=ocMDzfBRGj8) — YouTube, hands-on
- 📹 [ThePrimeagen on AI-assisted coding](https://www.youtube.com/watch?v=wF7-_K_RHYU) — Engineering perspective
- 📄 [Claude for Coding (Anthropic docs)](https://docs.anthropic.com/en/docs/use-cases/coding)
- 📄 [Cursor Official Docs](https://docs.cursor.com/)
- 📹 [GitHub Copilot Workspace Demo](https://www.youtube.com/watch?v=DlH5-9MQj9w)

### Tools to Install Today
- **Cursor** — https://cursor.com (main editor)
- **Claude Desktop** — https://claude.ai/download (chat-based AI assistant)
- **GitHub Copilot** — as a secondary option

### 🔨 10x Win
Take a real task from your current job — write a new API endpoint or refactor an existing service — and do it entirely with AI assistance. Track time vs. your normal pace.

---

## Stage 1 — LLM Internals
**Time:** 3-5 days | **Maps to:** Understanding a new database engine

Think of LLMs as stateless functions: `f(conversation_history) → next_token`. All "memory" is external state you manage — exactly the kind of problem you already know how to solve.

### Resources
- 📹 [Andrej Karpathy — Intro to LLMs (1hr)](https://www.youtube.com/watch?v=zjkBMFhNj_g) ⭐ BEST single video
- 📹 [3Blue1Brown — What is a GPT?](https://www.youtube.com/watch?v=wjZofJX0v4M) — 27min visual intuition
- 📹 [Karpathy — Build nanoGPT from scratch](https://www.youtube.com/watch?v=kCc8FmEb1nY) — 2hrs, optional deep dive
- 📄 [Anthropic API Quickstart](https://docs.anthropic.com/en/docs/quickstart)
- 📄 [OpenAI API Quickstart](https://platform.openai.com/docs/quickstart)

### GitHub References
- 🔗 [karpathy/nanoGPT](https://github.com/karpathy/nanoGPT) — Build a GPT from scratch
- 🔗 [anthropics/anthropic-sdk-python](https://github.com/anthropics/anthropic-sdk-python) — Official Anthropic SDK
- 🔗 [anthropics/anthropic-cookbook](https://github.com/anthropics/anthropic-cookbook) — API usage examples

### 🔨 Build: Raw HTTP Chatbot
Build a CLI chatbot using only `httpx` calling the API directly. No SDKs. Manually maintain the conversation array across turns.

**Build Tutorials:**
- 📹 [Build a ChatGPT CLI in Python](https://www.youtube.com/watch?v=pgW5GuXy4iQ)
- 🔗 [Simple Anthropic CLI example](https://github.com/anthropics/anthropic-cookbook/tree/main/misc)

---

## Stage 2 — Context Engineering
**Time:** 1 week | **Maps to:** API contract design

"Prompt engineering" is evolving into **context engineering** — designing what information goes into an LLM's context, how it's structured, and when it's retrieved. A system prompt is like an API spec.

### Resources
- 📄 [Anthropic Prompt Engineering Guide](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview) ⭐ Best in ecosystem
- 📄 [DAIR.AI Prompt Engineering Guide](https://www.promptingguide.ai/) — Comprehensive reference
- 🎓 [DeepLearning.AI — ChatGPT Prompt Engineering for Developers](https://www.deeplearning.ai/short-courses/chatgpt-prompt-engineering-for-developers/) — Free, 1hr with notebooks
- 📄 [Simon Willison's Blog](https://simonwillison.net/) — Pragmatic AI writing
- 📄 [OpenAI Prompt Engineering Guide](https://platform.openai.com/docs/guides/prompt-engineering)

### GitHub References
- 🔗 [dair-ai/Prompt-Engineering-Guide](https://github.com/dair-ai/Prompt-Engineering-Guide) — Massive resource repo
- 🔗 [anthropics/prompt-eng-interactive-tutorial](https://github.com/anthropics/prompt-eng-interactive-tutorial) — Hands-on Anthropic course
- 🔗 [f/awesome-chatgpt-prompts](https://github.com/f/awesome-chatgpt-prompts) — Reference prompts

### 🔨 Build: Structured Data Extractor
Pull structured fields from messy Slack messages or Jira comments.

**Build Tutorials:**
- 📹 [Extract Structured Data from Unstructured Text](https://www.youtube.com/watch?v=yj-wSRJwrrc)
- 🔗 [Example: Email to JSON extractor](https://github.com/anthropics/anthropic-cookbook/tree/main/skills/classification)

---

## Stage 3 — Tool Use & Function Calling ⭐
**Time:** 1 week | **Maps to:** Webhook handlers where the caller is AI
**This is the pivot point — master this and everything else follows.**

In the near future, every microservice you build will need an AI-callable interface. Function calling is the foundation.

### Resources
- 📄 [Anthropic Tool Use Docs](https://docs.anthropic.com/en/docs/build-with-claude/tool-use/overview) ⭐ Start here
- 📄 [OpenAI Function Calling Guide](https://platform.openai.com/docs/guides/function-calling)
- 🎓 [DeepLearning.AI — Functions, Tools and Agents with LangChain](https://www.deeplearning.ai/short-courses/functions-tools-agents-langchain/) — Free, 2hrs
- 📹 [Fireship — Function Calling in 100 seconds](https://www.youtube.com/watch?v=aqdWSYWC_LI)
- 📹 [AI Jason — Function Calling Deep Dive](https://www.youtube.com/watch?v=PlhMqxD4FRs)

### GitHub References
- 🔗 [anthropics/anthropic-cookbook — Tool Use](https://github.com/anthropics/anthropic-cookbook/tree/main/tool_use) — Official examples
- 🔗 [openai/openai-cookbook — Function Calling](https://github.com/openai/openai-cookbook/tree/main/examples) — OpenAI examples
- 🔗 [run-llama/llama_index — Agent Tools](https://github.com/run-llama/llama_index/tree/main/llama-index-core/llama_index/core/tools)

### 🔨 Build: DevOps Agent with Real Tools
An agent with tools: `query_database()`, `check_service_health()`, `read_logs()`, `create_jira_ticket()`. Ask it "why is the payment service slow today?"

**Build Tutorials:**
- 📹 [Build an AI Agent from Scratch with Tools](https://www.youtube.com/watch?v=aqdWSYWC_LI)
- 📹 [James Briggs — Agents with Tool Use](https://www.youtube.com/watch?v=04MM0PXv2Fk)
- 🔗 [Reference: Customer Service Agent](https://github.com/anthropics/anthropic-cookbook/tree/main/tool_use/customer_service_agent.ipynb)

---

## Stage 4 — Structured Outputs + Pydantic
**Time:** 3-4 days | **Maps to:** Type-safe API responses

Make LLM outputs as reliable as typed API contracts using the `instructor` library.

### Resources
- 📄 [Instructor Library Docs](https://python.useinstructor.com/) ⭐ Clearest docs in AI ecosystem
- 📹 [Jason Liu — Structured Outputs Walkthrough](https://www.youtube.com/watch?v=yj-wSRJwrrc)
- 📄 [Jason Liu's Blog — jxnl.co](https://jxnl.co/writing/) — Must-follow
- 📄 [Pydantic Docs](https://docs.pydantic.dev/) — Foundation library
- 📄 [OpenAI Structured Outputs Guide](https://platform.openai.com/docs/guides/structured-outputs)

### GitHub References
- 🔗 [jxnl/instructor](https://github.com/jxnl/instructor) ⭐ THE library + examples in `/examples`
- 🔗 [instructor examples dir](https://github.com/jxnl/instructor/tree/main/examples) — Production-ready patterns
- 🔗 [pydantic/pydantic](https://github.com/pydantic/pydantic)

### 🔨 Build: Incident Analyzer
Paste a raw PagerDuty alert or incident report, extract structured fields (severity, affected services, root cause hypothesis, suggested actions).

**Build Tutorials:**
- 📹 [Build an Incident Response AI with Instructor](https://www.youtube.com/watch?v=yj-wSRJwrrc)
- 🔗 [Example: Data extraction with Instructor](https://github.com/jxnl/instructor/blob/main/examples/extract_users/run.py)

---

## Stage 5 — RAG & Vector Search
**Time:** 1-2 weeks | **Maps to:** Adding a semantic search index

Embeddings are semantic hash functions. Vector databases are similarity indexes. You already understand indexing — this is the same discipline applied to meaning.

### Resources
- 🎓 [DeepLearning.AI — Building and Evaluating Advanced RAG](https://www.deeplearning.ai/short-courses/building-evaluating-advanced-rag/) — Free, hands-on
- 📄 [pgvector README](https://github.com/pgvector/pgvector) ⭐ Add vector search to Postgres
- 📄 [Chroma Docs](https://docs.trychroma.com/) — Easiest local vector DB
- 📹 [Fireship — Vector Databases Explained](https://www.youtube.com/watch?v=klTvEwg3oJ4)
- 📄 [LangChain RAG Tutorial](https://python.langchain.com/docs/tutorials/rag/)
- 📹 [Greg Kamradt — Levels of RAG Complexity](https://www.youtube.com/watch?v=TRjq7t2Ms5I)

### GitHub References
- 🔗 [pgvector/pgvector](https://github.com/pgvector/pgvector) — Postgres vector extension
- 🔗 [chroma-core/chroma](https://github.com/chroma-core/chroma) — Local vector DB
- 🔗 [langchain-ai/rag-from-scratch](https://github.com/langchain-ai/rag-from-scratch) ⭐ Excellent walkthrough
- 🔗 [run-llama/llama_index](https://github.com/run-llama/llama_index) — Full RAG framework
- 🔗 [weaviate/weaviate](https://github.com/weaviate/weaviate) — Production vector DB

### 🔨 Build: Chat With Your Codebase
Index a repo, embed all source files, store in pgvector (use existing Postgres), build a CLI answering questions like "where is authentication handled?"

**Build Tutorials:**
- 📹 [Build "Chat with Your Code" with RAG](https://www.youtube.com/watch?v=Ix9WIZpArm0)
- 📹 [RAG From Scratch - LangChain Series](https://www.youtube.com/playlist?list=PLfaIDFEXuae2LXbO1_PKyVJiQ23ZztA0x) ⭐ Full playlist
- 🔗 [Reference: Codebase chat example](https://github.com/langchain-ai/langchain/tree/master/templates)

---

## Stage 6 — Agent Frameworks (LangGraph)
**Time:** 2 weeks | **Maps to:** Workflow engine with AI decision nodes

Skip deep LangChain — go straight to **LangGraph**. It models agents as directed graphs with nodes and edges, mapping directly to state machines you've already designed.

### Resources
- 📄 [LangGraph Official Tutorials](https://langchain-ai.github.io/langgraph/tutorials/introduction/) ⭐ Start here
- 🎓 [DeepLearning.AI — AI Agents in LangGraph](https://www.deeplearning.ai/short-courses/ai-agents-in-langgraph/) — Free, best LangGraph course
- 📹 [LangChain YouTube Channel](https://www.youtube.com/@LangChain) — Frequent tutorials
- 📄 [LangGraph How-to Guides](https://langchain-ai.github.io/langgraph/how-tos/) — Copy-paste patterns
- 📹 [Harrison Chase — Building Agents with LangGraph](https://www.youtube.com/watch?v=pbAd8O1Lvm4)

### GitHub References
- 🔗 [langchain-ai/langgraph](https://github.com/langchain-ai/langgraph) ⭐ Main repo
- 🔗 [langchain-ai/langgraph — examples](https://github.com/langchain-ai/langgraph/tree/main/examples) — Official examples
- 🔗 [langchain-ai/langgraph-swarm-py](https://github.com/langchain-ai/langgraph-swarm-py) — Multi-agent patterns
- 🔗 [von-development/awesome-LangGraph](https://github.com/von-development/awesome-LangGraph) — Community resources

### 🔨 Build: Automated Incident Response Agent
On alert received: checks service health → queries recent logs → checks deployment history → cross-references runbook → drafts triage report.

**Build Tutorials:**
- 📹 [Build an Agent with LangGraph from Scratch](https://www.youtube.com/watch?v=PqS1kib7RTw)
- 📹 [LangGraph Deep Dive Playlist](https://www.youtube.com/playlist?list=PLfaIDFEXuae16n2TWUkKq5PgJ0w6Pkwtg)
- 🔗 [Reference: ReAct agent with LangGraph](https://github.com/langchain-ai/langgraph/blob/main/examples/create-react-agent.ipynb)

---

## Stage 7 — MCP Servers ⭐
**Time:** 1-2 weeks | **Maps to:** Building the AI interface layer of backend services

MCP is the most strategic thing on this list. Your existing backend services can each become an MCP server — wrap them and any AI agent can use them.

### Resources
- 📄 [Official MCP Docs](https://modelcontextprotocol.io/introduction) ⭐ The spec + quickstarts
- 📄 [MCP Python SDK](https://github.com/modelcontextprotocol/python-sdk) — Reference implementation
- 📹 [Jack Herrington — MCP Crash Course](https://www.youtube.com/watch?v=LqTQi8qexJM) ⭐ Very practical
- 📹 [Anthropic — Building MCP Servers](https://www.youtube.com/watch?v=EKCKxqAMHMw)
- 📄 [MCP Python Quickstart](https://modelcontextprotocol.io/quickstart/server)
- 📹 [AI Engineer — MCP Workshop](https://www.youtube.com/watch?v=kQmXtrmQ5Zg)

### GitHub References
- 🔗 [modelcontextprotocol/python-sdk](https://github.com/modelcontextprotocol/python-sdk) ⭐ Official SDK
- 🔗 [modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers) ⭐ Reference servers (filesystem, GitHub, Slack, etc.)
- 🔗 [punkpeye/awesome-mcp-servers](https://github.com/punkpeye/awesome-mcp-servers) — Curated list of MCP servers
- 🔗 [modelcontextprotocol/typescript-sdk](https://github.com/modelcontextprotocol/typescript-sdk) — TS alternative
- 🔗 [modelcontextprotocol/inspector](https://github.com/modelcontextprotocol/inspector) — Debugging tool

### 🔨 Build Sequence
1. **Wrap a public API** (GitHub, Notion, Jira) as MCP server — connect to Claude Desktop
2. **Postgres as MCP resource** — query your DB conversationally
3. **Deployment pipeline MCP** — trigger deploys, check status, rollback

**Build Tutorials:**
- 📹 [Build Your First MCP Server](https://www.youtube.com/watch?v=LqTQi8qexJM)
- 📹 [Matt Pocock — MCP Server Tutorial](https://www.youtube.com/watch?v=Hx_MuRSHmsU)
- 📹 [Build a Notion MCP Server](https://www.youtube.com/watch?v=-x5ciiKXkG0)
- 🔗 [Reference: Filesystem MCP Server](https://github.com/modelcontextprotocol/servers/tree/main/src/filesystem)
- 🔗 [Reference: GitHub MCP Server](https://github.com/modelcontextprotocol/servers/tree/main/src/github)
- 🔗 [Reference: Postgres MCP Server](https://github.com/modelcontextprotocol/servers/tree/main/src/postgres)

---

## Stage 8 — AI-Native Backend Patterns
**Time:** 1-2 weeks | **Maps to:** Distributed systems patterns for AI

New patterns every backend engineer needs: streaming APIs, agent state persistence, async execution, prompt injection defense.

### Resources
- 📄 [LangGraph Persistence & Checkpointing](https://langchain-ai.github.io/langgraph/concepts/persistence/)
- 📄 [Streaming with Anthropic API](https://docs.anthropic.com/en/api/messages-streaming)
- 📄 [OWASP LLM Top 10](https://owasp.org/www-project-top-10-for-large-language-model-applications/) ⭐ AI security essentials
- 📹 [Fireship — SSE vs WebSockets](https://www.youtube.com/watch?v=n9mRjkQg3VE)
- 📄 [Eugene Yan — Patterns for Building LLM Systems](https://eugeneyan.com/writing/llm-patterns/) ⭐ Must-read
- 📄 [Anthropic — Prompt Injection Defense](https://www.anthropic.com/research/mitigating-prompt-injection-attacks)

### GitHub References
- 🔗 [Arize-ai/phoenix](https://github.com/Arize-ai/phoenix) — LLM observability
- 🔗 [langfuse/langfuse](https://github.com/langfuse/langfuse) — Open-source LLM engineering platform
- 🔗 [protectai/rebuff](https://github.com/protectai/rebuff) — Prompt injection detection
- 🔗 [sbdchd/squawk](https://github.com/sbdchd/squawk) — Postgres migration safety (patterns apply to agent DBs)

### 🔨 Build: Async Long-Running Agent
POST research task → get job ID → agent runs async with state checkpointed to Postgres → poll for status → stream results via SSE.

**Build Tutorials:**
- 📹 [Streaming AI Responses with SSE](https://www.youtube.com/watch?v=XQjKcbcmrRI)
- 📹 [LangGraph Persistence Tutorial](https://www.youtube.com/watch?v=DZL-k8gzZCE)
- 🔗 [Reference: Background job queue with Celery](https://github.com/celery/celery)

---

## Stage 9 — LLMOps & Evals
**Time:** 1 week | **Maps to:** Observability/SRE for AI systems

Evals are test suites for AI behavior. Without them, you're shipping on vibes. With them, you have regression detection and performance benchmarks.

### Resources
- 📄 [RAGAS Framework Docs](https://docs.ragas.io/) ⭐ De facto RAG eval standard
- 📄 [Braintrust Eval Platform](https://www.braintrustdata.com/docs) — Best eval tool, strong free tier
- 📄 [LangSmith Docs](https://docs.smith.langchain.com/) — Tracing + evals
- 📹 [Hamel Husain — Your AI Product Needs Evals](https://www.youtube.com/watch?v=r4kAsWMCTBQ) ⭐ MUST WATCH
- 📄 [Eugene Yan — LLM Evaluation](https://eugeneyan.com/writing/evals/)
- 📹 [Shreya Shankar — Evaluating LLM Apps](https://www.youtube.com/watch?v=eLXF0VojuSs)

### GitHub References
- 🔗 [explodinggradients/ragas](https://github.com/explodinggradients/ragas) ⭐ RAG evaluation
- 🔗 [openai/evals](https://github.com/openai/evals) — OpenAI's framework
- 🔗 [confident-ai/deepeval](https://github.com/confident-ai/deepeval) — Pytest-style LLM testing
- 🔗 [langfuse/langfuse](https://github.com/langfuse/langfuse) — Open-source LLM observability
- 🔗 [Helicone/helicone](https://github.com/Helicone/helicone) — LLM monitoring

### 🔨 Build: Add Eval Suite to Your Agent
Take the incident response agent from Stage 6, create 20 test scenarios with expected behaviors, run automatically in CI.

**Build Tutorials:**
- 📹 [Building Evals for LLM Apps](https://www.youtube.com/watch?v=eLXF0VojuSs)
- 📹 [RAGAS Quickstart](https://www.youtube.com/watch?v=fWC4VxolWAk)
- 🔗 [Reference: Eval examples with Braintrust](https://github.com/braintrustdata/braintrust-cookbook)

---

## Stage 10 — Multi-Agent Systems
**Time:** 2 weeks | **Maps to:** Microservices, but agents are the services

One orchestrator routes to specialized workers. Same distributed systems thinking — failures, retries, timeouts, partial failure handling.

### Resources
- 🎓 [DeepLearning.AI — Multi AI Agent Systems with crewAI](https://www.deeplearning.ai/short-courses/multi-ai-agent-systems-with-crewai/) — Free
- 📄 [LangGraph Multi-Agent Architecture](https://langchain-ai.github.io/langgraph/concepts/multi_agent/)
- 📄 [AutoGen Docs — Microsoft](https://microsoft.github.io/autogen/)
- 📹 [Andrew Ng — Agentic Design Patterns](https://www.youtube.com/watch?v=sal78ACtGTc)
- 📄 [CrewAI Docs](https://docs.crewai.com/)

### GitHub References
- 🔗 [joaomdmoura/crewAI](https://github.com/joaomdmoura/crewAI) ⭐ Popular multi-agent framework
- 🔗 [microsoft/autogen](https://github.com/microsoft/autogen) ⭐ Microsoft's framework
- 🔗 [langchain-ai/langgraph — multi-agent examples](https://github.com/langchain-ai/langgraph/tree/main/examples/multi_agent)
- 🔗 [OpenBMB/ChatDev](https://github.com/OpenBMB/ChatDev) — Multi-agent software company simulation
- 🔗 [geekan/MetaGPT](https://github.com/geekan/MetaGPT) — Multi-agent software dev

### 🔨 Build: PR Review Pipeline
One agent reads diff → one checks security → one checks performance → one checks test coverage → orchestrator aggregates and posts GitHub review.

**Build Tutorials:**
- 📹 [Multi-Agent Systems with CrewAI](https://www.youtube.com/watch?v=kBXYFaZ0EN0)
- 📹 [AutoGen Tutorial Series](https://www.youtube.com/playlist?list=PLp9pLaqAQbY2vUjGEVgz8yAOdJlyy3AQb)
- 📹 [Build a Code Review Agent](https://www.youtube.com/watch?v=7Ts1X8D3g7Q)
- 🔗 [Reference: CrewAI code examples](https://github.com/joaomdmoura/crewAI-examples)

---

## Staying Current

### Must-Follow Sources

| Source | Why It's Worth Your Time | Format |
|---|---|---|
| [Latent Space Podcast](https://www.latent.space/) | Deep technical interviews | Podcast |
| [TLDR AI Newsletter](https://tldr.tech/ai) | 5-min daily digest, high signal | Email |
| [Simon Willison's Blog](https://simonwillison.net/) | Pragmatic AI engineering | Blog |
| [Jason Liu's Blog](https://jxnl.co/writing/) | Applied AI patterns | Blog |
| [Eugene Yan's Blog](https://eugeneyan.com/) | Applied ML/LLM systems | Blog |
| [Lilian Weng's Blog](https://lilianweng.github.io/) | Research-level depth | Blog |
| [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA) | Open-source model community | Reddit |
| [Papers With Code](https://paperswithcode.com/) | Research + implementations | Site |

### Essential Papers (1 per week)
- **ReAct: Synergizing Reasoning and Acting** — [arxiv](https://arxiv.org/abs/2210.03629)
- **Toolformer: Language Models Can Teach Themselves to Use Tools** — [arxiv](https://arxiv.org/abs/2302.04761)
- **Attention Is All You Need** — [arxiv](https://arxiv.org/abs/1706.03762)
- **Chain-of-Thought Prompting** — [arxiv](https://arxiv.org/abs/2201.11903)
- **Retrieval-Augmented Generation (RAG)** — [arxiv](https://arxiv.org/abs/2005.11401)

---

## Recommended Timeline

```
Week 1-2:     Stage 0 (ongoing) + Stage 1 (LLM Internals)
Week 3:       Stage 2 (Context Engineering)
Week 4:       Stage 3 (Tool Use) ⭐ pivot point
Week 5:       Stage 4 (Structured Outputs)
Week 6-7:     Stage 5 (RAG + pgvector)
Week 8-9:     Stage 6 (LangGraph)
Week 10-11:   Stage 7 (MCP Servers) ⭐ career inflection
Week 12:      Stage 8 (AI-Native Backend Patterns)
Week 13:      Stage 9 (LLMOps + Evals)
Week 14-15:   Stage 10 (Multi-Agent Systems)
Ongoing:      Weekly paper + daily TLDR AI + monthly project
```

**Total: ~3 months of consistent evenings/weekends.** Productivity gains from Stage 0 start immediately.

---

## Portfolio Checklist

By the end, you should have these projects on GitHub:

- [ ] Raw API chatbot (no SDKs)
- [ ] Structured data extractor
- [ ] DevOps agent with real tools
- [ ] Incident analyzer (Pydantic/Instructor)
- [ ] "Chat with your codebase" RAG app
- [ ] Automated incident response agent (LangGraph)
- [ ] At least 2 custom MCP servers (wrapping real APIs)
- [ ] Long-running async agent with state persistence
- [ ] Eval suite for one of the above agents
- [ ] Multi-agent PR review pipeline

---

## The Career Inflection Point

The engineers who will be most valuable in 2 years aren't the ones who learned the most AI theory — they're the ones who combined solid backend engineering fundamentals with AI fluency.

**You already have the hard part.** This path is the bridge.

The profile in extreme demand: *a backend engineer who can design agent-based systems, build MCP servers to connect them to business data, deploy them reliably with evals and monitoring, and reason about failure modes like a distributed systems engineer.*

That's exactly what this path builds toward.

---

*Last updated: April 2026*
