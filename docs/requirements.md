Forge v0.1 — Requirements

Product goal

Forge is a cloud-based AI coding environment that allows a user to connect a GitHub repository and give an AI agent coding tasks. The agent operates inside an isolated sandbox, can inspect and modify code, run commands/tests, and ultimately create a Git commit or Pull Request.

Core user flow
Sign up / Login
      ↓
Connect GitHub
      ↓
Select Repository
      ↓
Create Coding Session
      ↓
Sandbox Created
      ↓
Agent Receives Task
      ↓
┌───────────────────────┐
│ Read / Search Code    │
│ Modify Files          │
│ Run Terminal Commands │
│ Run Tests             │
│ Inspect Results       │
│ Repeat if necessary   │
└───────────┬───────────┘
            ↓
       Show Changes
            ↓
       User Approval
            ↓
       Commit / PR
Functional requirements

Authentication

User can register/login.
Sessions are authenticated.
User can access only their own projects/sessions.

GitHub

User can connect a GitHub account through our GitHub App.
User can view repositories they have authorized.
Forge can clone the selected repository.
Forge can create commits/PRs with appropriate permissions.

Sandbox

Coding sessions execute in isolated environments.
Sandbox can run shell commands.
Sandbox has Git and common development tooling.
Sandbox can be destroyed/recreated.
Secrets should not be unnecessarily exposed to the sandbox.

Agent

User can send a coding task.
Agent can inspect repository files.
Agent can search the codebase.
Agent can modify files.
Agent can execute commands.
Agent can run tests.
Agent can observe command/test results and continue working.
Agent stops when the task is complete or requires user intervention.

Real-time UI

User sees agent progress.
Terminal output streams to the UI.
Tool executions are visible.
Errors are visible.
Final changes/diff are displayed.

Git

User can inspect the diff.
User can approve changes.
Forge can commit changes.
Forge can push changes.
Forge can create a Pull Request.
Non-functional requirements

These are just as important.

Security
API server
    ≠
code execution environment

We should never allow arbitrary user/agent commands to execute directly on our API server.

Reliability

A failed agent task shouldn't bring down the API.

Isolation

Different users' coding environments must not share writable state accidentally.

Observability

We should eventually be able to answer:

"What was the agent doing when it failed?"

So agent runs, tool executions, errors, and important events should be traceable.

Extensibility

The agent should use a tool interface, so adding:

Browser
LSP
Deploy
Database

later doesn't require rewriting the entire agent.

Explicitly out of scope for V0.1

This is important.

We will not initially build:

Kubernetes
Multi-agent collaboration
RAG
LSP
Billing
Team workspaces
Advanced deployment infrastructure
Fine-tuning
Custom foundation models
Large-scale cloud orchestration

We'll add these only after the core agent works.

V0.1 success criteria

I would consider the first real version successful when we can demonstrate this:

"Add a dark mode toggle to this React application."
                         ↓
                       Forge
                         ↓
                 Clone GitHub repo
                         ↓
                 Start sandbox
                         ↓
                  Agent inspects code
                         ↓
                  Agent edits files
                         ↓
                   Runs tests
                         ↓
                    Shows diff
                         ↓
                  User approves
                         ↓
                  Creates Git commit
                         ↓
                  Creates Pull Request

That single demo is our north star.

Everything we build should move us closer to that.