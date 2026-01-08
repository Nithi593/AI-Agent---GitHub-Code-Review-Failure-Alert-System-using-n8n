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

SETUP:

AI-Powered GitHub Code Review Automation (n8n)

This project contains two n8n workflows:

✅ Workflow 1 — AI Code Review on GitHub Push

Triggered on every GitHub push, it:

Fetches commit details + changed files

Filters Java source files only

Builds project structure (repo tree)

Fetches file content + diff

Sends context to an LLM (Gemini) for review

Posts inline GitHub commit comments for issues

If no issues are found, optionally triggers an email notification

✅ Workflow 2 — Error Monitoring & Alerting

Triggered automatically when Workflow 1 fails, it:

Captures execution details (workflow name, execution ID, last node)

Sends an email alert with error details and a short summary

Requirements

n8n (Self-hosted or Cloud)

GitHub repository access + token

Gemini / Google PaLM API key configured in n8n

Gmail OAuth2 credentials configured in n8n

Setup Instructions
1) Import Workflows

Open n8n

Click Import workflow

Import:

workflow1.json

workflow2_error_alert.json

2) Create Credentials in n8n
✅ GitHub API Credential

Create a GitHub credential in n8n with a PAT (Personal Access Token) that has:

repo access (for private repos)

public_repo (for public repos)

Used by:

GitHub Trigger

HTTP Request nodes posting comments

✅ Gemini / Google PaLM Credential

Create a Google Gemini / PaLM credential in n8n and connect it to the AI node.

Used by:

AI Reviewer node

✅ Gmail OAuth2 Credential

Create a Gmail OAuth2 credential in n8n.

Used by:

No Review email (Workflow 1)

Error alert email (Workflow 2)

3) Update Placeholders

In Workflow 1:

Replace:

YOUR_GITHUB_USERNAME

YOUR_REPO_NAME

YOUR_EMAIL@example.com

In Workflow 2:

Replace:

YOUR_ALERT_EMAIL@example.com

4) Link Workflow 2 to Workflow 1 (Error Workflow)

Open Workflow 1

Go to Settings

Under Error Workflow, select Workflow 2

Save

✅ Note: Workflow 2 will show as “Inactive” and that is correct — Error Trigger workflows don’t require activation.

Testing
Test Workflow 1

Push a commit that modifies any .java file and check:

GitHub commit → inline comments created

Test Error Workflow (Workflow 2)

Temporarily break a node in Workflow 1 (e.g., invalid URL), execute workflow, and confirm:

Workflow 2 sends a failure email with details

Notes / Tips

For larger files, the workflow truncates file content to avoid sending excessive payload to the model.

You can extend file filtering for .xml, .yml, .js, etc.

You can switch from commit comments to PR review comments if you want PR-based reviews.
* Inline commit comments via GitHub API
* Automated failure alerts via Gmail

This project reinforced how low-code orchestration + APIs + AI can be combined to build powerful, production-grade developer tooling — not just demos.
Always excited to build systems that improve code quality, reliability, and developer experience 🚀
