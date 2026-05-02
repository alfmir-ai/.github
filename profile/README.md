# Alfmir.ai
AI code agent for full-project workflows.

Alfmir.ai runs real end-to-end coding jobs against full repositories: it checks out code, executes an agent run from your prompt, and produces a reviewable diff you can merge. It’s fully open source (MIT), with a hosted cloud experience plus a self-host path.

**Come for the code agent. Stay for the workspace.**

**Formerly Alfe.** Alfmir.ai is the continuation of the Alfe project. You may still see “Alfe” referenced in code, docs, and legacy URLs while the transition finishes.

## Quick links

- [Key features](#key-features)
- [Architecture](#architecture)
- [License](#license)
- [Contact](#contact)
- [Company](#company)

## Key features

### Fully Available
- **AI code agent (primary): full-project workflows**
  - Runs against git repos (branch-based runs, patch generation, diff review, merge workflow).
  - Optimized for “do the work” prompts rather than chat-only assistance.
- **AI chat**
  - Workspace chat for planning and iteration.

### Available Partially in Code
- **Project management (GitHub-style tasks)**
  - Lightweight task boards / project management.
- **AI image design**
  - Generate and iterate on images inside the Chat workspace.
- **AI search (included in chat)**
  - Fast search.
- **Git hosting / repo workflows**
  - Repo operations for standard git collaboration.
- **Printify Integration**
  - Use your Printify API key to add designs to your stores.
- **ALSH Shell | Alfmir Shell**
  - Bash Shell Modifications with Alfmir.ai Integration.

## Architecture

Alfmir.ai’s value is the **agent + workflow layer**: repo execution, branching, diffs, task/workspace integration, and the UI that ties it together. Models are **swappable backends**—you should be able to choose based on speed, cost, and privacy requirements.

### Premium model path

- **Default engine (paid/cloud):** **KAT-Coder-Pro V2**
- **Routing:** via **OpenRouter** through **StreamLake**
- **Billing:** subscription + credits
- KAT is the premium default today, but it’s not the product—Alfmir.ai is designed to keep model backends interchangeable over time.

### Self-hosted and open model path

- **Supported open path:** **Qwen3-Coder-30B-A3B**
- Secondary path (capacity-limited)

### Server architecture

Server Architecture is divided into separate components. For code.alsh.ai, it has separate front-end servers, a back-end working-environment server, a git host, a separate database server, and a separate LiteLLM proxy server.

The front-end is hosted as multiple round-robin webservers for easy scalability. The front-end servers do not retain any user information, so it is easy to scale up as many as needed, and it does not matter which front-end server the user connects to. The chat.alsh.ai has a separate front-end server, but shares the database server.

The back-end working-environment server, to start, hosts the users working environment and runs the AI code agent on the working environment, it also hosts the Qwen 30b LLM model on the GPU. As users grow I will scale to multiple back-end servers similar to the front-end. The LiteLLM proxy server routes for the chat.alsh.ai front-end and for the advanced Kwaipilot: KAT-Coder-Pro V2 model for the code agent.

The AI agent that runs on user code is ran unpriveledged, and sandboxed, isolating operations to read/write on the users files only, and git operations. Preventing any code execution or directory escape.

The user data sent in chats/LLM prompts will be encrypted on disk/in database similar to Proton Mail encryption, so ideally data will not be accessible by Alfmir.ai, only by users themselves. User git working directories will be encrypted the same way when the AI agent is not actively working on the users directory (This allows user code to remain as private as possible, if the user uses an external git integration like GitHub instead of the Alfmir.ai git host.).

## License

MIT.

## Contact

- engineering@lochner.tech

## Company

Built by Lochner Technology ([lochner.tech](https://lochner.tech)).
