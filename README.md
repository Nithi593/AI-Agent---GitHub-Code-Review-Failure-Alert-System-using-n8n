# AI-Agent---GitHub-Code-Review-Failure-Alert-System-using-n8n

Recently, I designed and implemented an end-to-end AI Agent using n8n that brings together GitHub, AI-assisted code review, and operational alerting — turning every code push into an automated quality gate.
🔧 What the workflow does:
* Triggers on GitHub push events
* Analyzes changed Java files only (ignores build artifacts)
* Builds full project context dynamically by reading the repository tree
* Fetches file content + diffs for accurate, context-aware reviews
* Uses an LLM (Gemini) as a senior code reviewer to identify:
    * Bugs & logical issues
    * Performance concerns
    * Security risks
    * Incorrect imports or missing classes
    * Best-practice violations
* Posts inline review comments directly on the commit — just like a human reviewer
🚨 Operational Safety Built-In
To make this production-ready, I also implemented:
* Centralized error handling via n8n Error Trigger
* Automatic email alerts on workflow failure with:
    * Workflow name & execution ID
    * Failed node details
    * Root error message
    * Execution trace summary
This ensures silent failures never go unnoticed.

🏗️ Why this matters in real engineering teams
This automation mirrors real-world CI/CD and platform engineering needs:
✔ Reduces manual code review effort ✔ Provides fast feedback to developers ✔ Enforces consistent review standards ✔ Catches issues early (shift-left quality) ✔ Improves developer velocity without sacrificing reliability ✔ Adds observability and alerting to automation pipelines
This approach scales especially well for large teams, microservices, and fast-moving codebases, where human review alone becomes a bottleneck.

🛠️ Tech stack used:
* n8n (workflow orchestration & error handling)
* GitHub Webhooks & REST APIs
* LLM-based code review (Gemini)
* Java source analysis
* Inline commit comments via GitHub API
* Automated failure alerts via Gmail

This project reinforced how low-code orchestration + APIs + AI can be combined to build powerful, production-grade developer tooling — not just demos.
Always excited to build systems that improve code quality, reliability, and developer experience 🚀
