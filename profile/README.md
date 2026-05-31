# Alfmir.ai | Beta
AI code agent for full-project workflows.

Alfmir.ai runs real end-to-end coding jobs against full repositories: it checks out code, executes an agent run from your prompt, and produces a reviewable diff you can merge. It’s fully open source (MIT), with a hosted cloud experience plus a self-host path.

**An entire AI workspace for building. Code, Chat, Image Design.**

### [View the Code](https://github.com/alfmir-ai/alfmir.ai)

https://github.com/alfmir-ai/alfmir.ai

### [Try the App](https://alfmir.ai)

https://alfmir.ai

## Quick links

- [Key features](#key-features)
- [Screenshots](#screenshots)
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
- **Alfmir Shell | ALSH**
  - Bash Shell Modifications with Alfmir.ai Integration.

## Screenshots

<img width="1772" height="1504" alt="image" src="https://github.com/user-attachments/assets/8430bc3b-5985-4641-8764-72ecb060b5d4" />  

<img width="1601" height="987" alt="image" src="https://github.com/user-attachments/assets/73aae0e1-34e1-4105-bd6d-e6b33e232810" />  

<img width="736" height="1483" alt="image" src="https://github.com/user-attachments/assets/39a456d8-9972-4a53-b571-881773fee18e" />  

<img width="1327" height="1498" alt="image" src="https://github.com/user-attachments/assets/f0d9c381-c877-4e16-a725-d671896dcba9" />  

<img width="2083" height="749" alt="image" src="https://github.com/user-attachments/assets/e8a024ba-eb67-4a85-8bc6-69fe24bd2981" />  

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

Server Architecture is divided into separate components. For code.alfmir.ai, it has separate front-end servers, a back-end working-environment server, a git host, a separate database server, and a separate LiteLLM proxy server.

The front-end is hosted as multiple round-robin webservers for easy scalability. The front-end servers do not retain any user information, so it is easy to scale up as many as needed, and it does not matter which front-end server the user connects to. The chat.alfmir.ai has a separate front-end server, but shares the database server.

The back-end working-environment server, to start, hosts the users working environment and runs the AI code agent on the working environment, it also hosts the Qwen 30b LLM model on the GPU. As users grow, multiple back-end servers will be scaled similar to the front-end. The LiteLLM proxy server routes for the chat.alfmir.ai front-end and for the advanced Kwaipilot: KAT-Coder-Pro V2 model for the code agent.

The AI agent that runs on user code is ran unpriveledged, and sandboxed, isolating operations to read/write on the users files only, and git operations. Preventing any code execution or directory escape.

Alfmir.ai is built with a focus on privacy and security. User data sent in chats/LLM prompts is encrypted on disk/in database using a zero-access-style approach, so the data is not accessible by Alfmir.ai when it is not actively in use by Alfmir.ai services. User git working directories are encrypted the same way whenever the AI agent is not actively working in a user’s directory (This allows user code to remain as private as possible, if the user uses an external git integration like GitHub instead of the Alfmir.ai git host.). Redaction controls are applied to reduce accidental exposure in logs and operational telemetry.

## License

MIT.

## Contact

- engineering@lochner.tech

## Company

Built by Lochner Technology ([lochner.tech](https://lochner.tech)).
