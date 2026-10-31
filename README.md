# LangChain & LangGraph Foundations — Annotated Learning Repository

A hands-on collection of 21 Jupyter notebooks covering foundational agents, tools, memory, multimodal inputs, MCP, state, multi-agent orchestration, RAG, SQL, middleware and human-in-the-loop workflows. Each notebook now begins with a learning guide and includes step-by-step Markdown explanations plus concise Python purpose comments around executable cells.

> **Attribution and licensing:** This repository is based on the supplied LangChain Foundations course materials. The original MIT license and copyright notice are retained. Review the license and any third-party assets/data before redistributing or publishing. These annotations are learning aids; they do not imply that the underlying course material was authored by the repository owner.

## Learning path

### Module 1 — Agent Fundamentals
| Notebook | What you will learn |
|---|---|
| `1.1_foundational_models.ipynb` | Initialize models, inspect responses, create agents and stream output. |
| `1.1_prompting.ipynb` | System prompts, few-shot prompting and structured output. |
| `1.2_tools.ipynb` | Define typed Python tools and let agents call them. |
| `1.2_web_search.ipynb` | Add live web search to ground answers in current information. |
| `1.3_memory.ipynb` | Use checkpointing and thread IDs for short-term memory. |
| `1.4_multimodal_messages.ipynb` | Send text, image and audio inputs. |
| `1.5_personal_chef.ipynb` | Build a recipe assistant with web search and memory. |

### Module 2 — Advanced Agent Patterns
| Notebook | What you will learn |
|---|---|
| `2.1_mcp.ipynb` | Connect local/hosted Model Context Protocol servers. |
| `2.1_travel_agent.ipynb` | Build an MCP-enabled travel agent. |
| `2.2_runtime_context.ipynb` | Pass request-scoped context into tools. |
| `2.2_state.ipynb` | Extend, write and read agent state. |
| `2.3_multi_agent.ipynb` | Delegate work to specialist subagents. |
| `2.4_wedding_planners.ipynb` | Coordinate specialist agents in a wedding-planner workflow. |
| `bonus_rag.ipynb` | Load, chunk, embed and retrieve documents for RAG. |
| `bonus_sql.ipynb` | Expose a sample SQL database through an agent tool. |

### Module 3 — Production-Oriented Agent Design
| Notebook | What you will learn |
|---|---|
| `3.2_managing_messages.ipynb` | Summarize, trim and delete conversation messages. |
| `3.3_hitl.ipynb` | Pause for human approval, rejection or edits. |
| `3.4_dynamic_models.ipynb` | Select models dynamically with middleware. |
| `3.4_dynamic_prompts.ipynb` | Adapt system prompts at runtime. |
| `3.4_dynamic_tools.ipynb` | Control tool availability dynamically. |
| `3.5_email_agent.ipynb` | Combine authentication, dynamic capabilities and human review in an email workflow. |

## Repository structure

```text
.
├── notebooks/
│   ├── module-1/       # Agent fundamentals and Personal Chef project
│   ├── module-2/       # MCP, state, multi-agent, RAG and SQL
│   └── module-3/       # Middleware, HITL and Email Assistant project
├── env_utils.py        # Local environment/setup verification
├── pyproject.toml      # Python project and dependency configuration
├── requirements.txt    # pip dependency list
├── uv.lock             # Locked uv dependency resolution
└── .env.example        # Safe credential template
```

The Module 3 `agent-chat-ui/` folder contains the supporting Next.js chat interface used by the project. Sample resources under each module are retained where they are required by the exercises.

## Setup

### Requirements
- Python `>=3.12,<3.14` (see `pyproject.toml`).
- `uv` recommended, or Python `venv` plus pip.
- API credentials for the providers/tools used by the notebook you intend to run.
- Optional local services/devices where applicable (MCP server, audio input, LangGraph Studio).

### 1. Clone and configure environment variables

```bash
git clone <your-public-repository-url>
cd <repository-folder>
cp .env.example .env  # Windows PowerShell: Copy-Item .env.example .env
```

Edit `.env` locally and replace only the credentials you need. **Never commit `.env`, paste API keys into notebooks, or share credentials in screenshots.** If a key has ever been committed or shared, revoke/rotate it with its provider; deleting the file from the latest commit is not sufficient.

### 2. Install dependencies

With `uv` (recommended):

```bash
uv sync
```

With pip:

```bash
python -m venv .venv
# macOS/Linux
source .venv/bin/activate
# Windows PowerShell
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

### 3. Verify and launch Jupyter

```bash
uv run python env_utils.py
uv run jupyter lab
```

Or activate `.venv` and run `python env_utils.py` followed by `jupyter lab`. Open the notebook you want to study and execute cells from top to bottom.

### 4. Optional LangGraph development server

From the relevant module directory (Module 1 or Module 3):

```bash
uv run langgraph dev
```

Some exercises also use `notebooks/module-2/resources/2.1_mcp_server.py`; start the server as described in that notebook before connecting the client.

## How to study each notebook

1. Read the **Purpose**, **Workflow**, **Learning objectives** and **Key learnings** sections added at the beginning.
2. Read the explanation immediately before each executable cell.
3. Run cells in order; many later cells depend on variables created earlier.
4. Inspect message histories, tool calls, state and metadata rather than judging only the final natural-language answer.
5. Change one input or configuration at a time and record how the behavior changes.
6. For external actions, use test accounts/data and require human approval where appropriate.

## Important implementation and safety notes

- **Credentials:** `.env` is intentionally excluded. `.env.example` contains placeholders only.
- **External calls and cost:** model, web-search and tracing calls may incur provider charges.
- **Model drift:** provider model IDs and SDK behavior evolve; update model names and dependencies deliberately and retest.
- **Memory:** in-memory checkpointers are useful for labs but are not durable production storage.
- **MCP:** only connect to trusted servers and review the tools they expose.
- **RAG:** retrieved documents may contain incorrect or malicious instructions; treat them as untrusted content and validate citations/claims.
- **SQL:** use least-privilege database credentials, read-only access where possible, and query validation/limits.
- **HITL:** approval flows are not a substitute for authentication or authorization.
- **Multimodal:** image/audio examples require supported models, correct formats and appropriate consent for recorded media.
- **Reproducibility:** notebook outputs have been cleared so no stale results or accidental runtime data are published. Run the notebooks to regenerate outputs.

## Key takeaways across the course

- An agent combines a model with instructions, tools and an execution loop.
- Tool schemas and descriptions are part of the agent interface: make them narrow and explicit.
- State, runtime context and message history serve different purposes and should be designed separately.
- MCP provides a reusable integration boundary for external tools.
- Multi-agent systems need clear specialist responsibilities and coordinator boundaries.
- RAG combines retrieval with generation; quality depends on ingestion, chunking, embeddings and retrieval.
- Middleware enables runtime policy and capability changes.
- Human review is essential before sensitive or irreversible actions.

## License and source attribution

The original `LICENSE` file is retained. Review it together with any included sample documents, images, database files and the upstream course terms before publishing. Keep attribution intact.
