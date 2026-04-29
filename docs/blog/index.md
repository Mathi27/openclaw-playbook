# Blog

AI Agent Stack

What has shifted since the 2025  

Agents are showing up outside the chat window. In 2025, talking to an agent mostly meant typing into ChatGPT or Claude.ai. In 2026, agents live inside Cursor, inside Slack channels, inside browsers like Comet, Dia, and Arc Search, inside the IDE, inside enterprise dashboards, and increasingly inside approval queues that route requests to a human only when a policy says so. The surface area where humans interact with agents has become its own design problem.

Coding harnesses became their own product category. Last year, the framework conversation mostly came down to LangChain or LlamaIndex. This year, the harnesses people actually live inside are Claude Code, Codex, Cursor‘s agent mode, and Replit Agent. These are full products that ship with the agent loop inside them. The planner, the tool registry, the memory, the streaming protocol all come pre-wired. The job in 2026 is picking the right harness for your workload, the same way you would pick an IDE.

The wires between agents are getting standardized. MCP was very early at the start of 2025. Today it ships in every major harness. A2A is in production at a few teams we work with. AG-UI and A2UI are emerging for streaming UIs. Publishing an MCP server is starting to take the place of writing a custom integration for every tool. A lot of the change in the layers below follows from this one.

How the nine layers fit together

Each of those three shifts shows up in the picture below. Agents living in more surfaces is what gives the interface its own layer at the top. Coding harnesses maturing into products is what creates the heavy end of that interface layer (the surfaces that ship the agent loop fused in). The protocols handling the wiring is what lets tools, knowledge, and memory sit as their own clean concerns. Observability and governance get lifted out of the stack and run as vertical rails, since they touch every layer above them.

The full picture splits into four groups, plus two rails:

The top (Layer 1), where humans meet the agent (chat surfaces, workspaces, browser agents, and the coding harnesses where the agent and the surface ship together).

The core (Layers 2 through 4), where the agent’s loop machinery lives: runtimes, protocols, and tools.

The middle (Layers 5 and 6), what the agent reads in and what it retains: knowledge and memory.

The foundation (Layer 7), where intelligence comes from: models, inference, and routing.

Two vertical rails (Layers 8 and 9): observability and evals, then governance and security. Both touch every layer above them.

Below, I walk each layer: what it is for, what teams actually use, and where the 2026 picture moved since 2025.

Layer 1: Agent Interfaces, Workspaces, and Harnesses
This sits at the top of the picture. It is where the agent shows up for the human.

In 2025, most conversations about agents pointed at the chat window. The set of meaningful surfaces is wider in 2026. Agents now live inside the IDE, inside Slack threads, inside the browser, inside the dashboard, and inside approval queues. The spectrum here runs from light to heavy. The light end is a Slack channel that talks to an agent running somewhere else. The heavy end is a coding harness like Claude Code that ships the entire agent loop fused into the surface itself. Both count as Layer 1.

Some of the surfaces worth tracking:

Coding harnesses (the agent loop ships with the surface): Claude Code, Codex, Cursor‘s agent mode, Windsurf, Replit Agent, Cline, Aider

Workspace agents: Slack agents, Microsoft Copilot, Google Workspace agents, Notion AI

Browser agents: Perplexity Comet, Dia, Arc Search

Approval and review surfaces: PR review bots, audit dashboards, human-in-the-loop queues

The design problem in this layer is choosing which surface to put the agent on, deciding how much of the loop ships with the surface, and shaping the human’s role so they stay in control.

Layer 2: Agent Runtimes
This is where the agent loop actually lives in code. The runtime is the planner, the executor, the tool dispatcher, the state machine, and the streaming surface, all working together. Some teams build their own. Most pick one of the orchestration libraries and write code inside it.

The shift in 2026 is that runtimes are a real category, distinct from the coding harnesses at Layer 1 that wrap them up as full products. If you are using one of those products, the runtime is whatever was baked in. If you are building your own agent inside an enterprise codebase, you are picking from the list below.

A few of the runtimes in active use:

LangGraph, OpenAI Agents SDK, Google ADK, Microsoft Agent Framework, AutoGen, CrewAI, Agno, DSPy, Letta

The runtime layer has commoditized faster than I expected. A year ago, picking a runtime was the most consequential decision in an agent project. In 2026, that decision mostly comes down to fit with your stack and your team’s preferences (with one or two exceptions, depending on how serious your state and durability requirements are).

Layer 3: Protocols and Interoperability
I almost did not include this layer in the 2025 version because it didn’t really exist yet. In 2026 it is connective tissue.

The protocols in active use:

MCP for tool and resource access

A2A for agent-to-agent calls

AG-UI and A2UI for streaming interfaces and shared UI state

Emerging commerce and identity protocols for agents that transact

The reason this matters is reach. When a tool publishes an MCP server, every harness can call it. When an agent speaks A2A, it can hand off work to another team’s agent without a custom integration. The work that used to take a sprint now takes a config file.

For anything new in 2026, building to the protocols is the move that pays back over time. Custom integrations carry a long maintenance tail.

yer 4: Tools, Actions, and Sandboxes
Agents do not matter unless they can act. This layer is what they act through.

Two things changed in 2026. First, computer-use and browser-use moved from demo to production. Anthropic, OpenAI, and Google all ship models that can drive a browser or a desktop. Second, sandbox infrastructure became a real category, because nobody is letting an agent run code on their laptop without a wrapper.

What teams are reaching for here:

Code execution sandboxes: E2B, Modal, Daytona

Browser automation: Browserbase, Steel, browser-use

Tool registries and integrations: Composio, Arcade

Native primitives: Anthropic’s computer-use, OpenAI’s Operator, MCP servers shipped by every major SaaS

The question to ask before you ship: what can this agent do, and what does the worst version of doing it look like? If you can answer that, you can put the right sandbox and approval gate around it.

Layer 5: Knowledge, Context, and Retrieval
This is what most people called RAG in 2025. In 2026 the term feels small. Retrieval is one move inside a larger context problem: getting the agent the information it needs, from a trustworthy source, in a shape it can use.

The pieces in this layer:

Vector databases: Pinecone, Weaviate, Qdrant, Chroma, Milvus, Supabase pgvector

Enterprise search and indexing: Glean, Vectara, Hebbia

Document intelligence: LlamaIndex, Reducto, Unstructured

Rerankers and graph retrievers: Cohere Rerank, Voyage, Neo4j-backed retrieval

The teams making the most progress here treat retrieval as an evals problem first and an infrastructure problem second. The vector database is rarely the bottleneck. Which chunks got retrieved and why almost always is.

Layer 6: Memory and State Management
In 2025, memory and knowledge were the same layer in every guide I read, including mine. They are different problems. Knowledge is the layer that pulls in external information for the agent to read. Memory is the layer that holds onto what the agent itself produces, across steps, sessions, and users.

The memory and state options in active use:

Agent memory platforms: Zep, Letta, Mem0, Cognee

Framework-native memory: LangChain memory, LangGraph checkpoints, OpenAI Agents SDK state

State stores: Redis, durable execution platforms like Temporal and Inngest

The reason this layer exists as its own thing in 2026: agents that span sessions and users need a memory system that knows what to keep, what to age out, and what to surface back into context. That is a different shape of problem than vector retrieval, and it deserves its own tooling.

Layer 7: Models, Inference, and Routing
The foundation. Without a capable model, none of the layers above hold up.

Two patterns are normal now that were unusual a year ago. First, most production agents call more than one model, and the agent itself decides which one to use for which step. Second, the routing layer is its own product category, with billing, fallback, and policy logic baked in.

The model and inference options:

Closed models: OpenAI, Anthropic, Google Gemini, xAI Grok

Open-weight providers: DeepSeek, Mistral, Meta Llama, Qwen

Inference platforms: Together, Fireworks, Groq, Cerebras, SambaNova, AWS Bedrock

Routing and gateways: LiteLLM, OpenRouter, Portkey, Helicone

Local serving: vLLM, SGLang, Ollama, llama.cpp

If you are starting an agent project today, pick a router on day one. The cost of swapping a model is much lower when the router was there from the start.


This is the rail that runs down the side of the whole picture, watching every layer.

In 2025, observability mostly meant tracing LLM calls. In 2026 it is a much bigger category. It now covers structured tracing, eval pipelines, regression suites, prompt and tool versioning, online and offline evaluation, drift detection, and human review of agent outputs. The good teams treat evals as core engineering. The teams that skip this layer ship a demo that breaks in week three.

The observability and evals options:

Tracing and analytics: LangSmith, Langfuse, Helicone, Weights & Biases Weave

Eval-first platforms: Braintrust, Arize, Phoenix, Comet Opik

Eval frameworks: Promptfoo, DeepEval, Inspect

Open standards: OpenTelemetry for traces, OpenInference for LLM-specific spans

The bar for this layer is simple. A team with real observability can tell you in five minutes whether their last change made the agent better or worse on their eval set. Anything short of that is logging dressed up as observability.

Layer 9: Governance, Security, and Human Control (the second vertical rail)
The second rail. This is the layer that decides whether the agent is allowed to act, who can override it, and what gets recorded when it does.

This layer barely showed up in the 2025 guide. In 2026 it is what separates a pilot from a production deployment. Every enterprise contract I work on now starts with the governance conversation.

The governance and security pieces:

Permissions and identity: Auth0 FGA, Permit.io, AWS IAM patterns adapted for agents

Prompt injection and DLP: Lakera, Protect AI, NVIDIA NeMo Guardrails

Sandboxing: E2B, hardened browser environments, ephemeral compute

Audit and policy: structured action logs, policy-as-code (OPA), human approval queues

Frameworks for human-in-the-loop: built into LangGraph, OpenAI Agents SDK, and most modern harnesses

What pushes governance up the priority list is autonomy. The moment your agent can act without a human reviewing each step, you are running a system that needs scoping, audit, and override. Every enterprise audit I run now spends most of its time on this layer. The model question rarely comes up.

