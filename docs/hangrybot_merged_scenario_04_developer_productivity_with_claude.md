# HangryBot Merged Scenario 4: Developer Productivity with Claude

## Why this merged scenario exists

This scenario adapts the exam’s **Developer Productivity with Claude** setup into HangryBot’s environment and merges in the earlier HangryBot materials on:

- Claude Code repository configuration
- MCP tool design and integration
- built-in tool usage with Read, Write, Bash, Grep, and Glob
- context-management patterns for long engineering sessions
- selective agentic orchestration for codebase exploration and automation

The result is a scenario about helping engineers move faster inside a complicated production system without sacrificing accuracy or safety.

---

## HangryBot production context

HangryBot’s stack is no longer small enough for any one engineer to hold in their head. New team members routinely need to understand interactions among:

- ATL ordering and handoff services
- PDK concierge workflows
- refund and credit policies
- the GenAI gateway and retrieval layer
- robot dispatch and telemetry ingestion
- forecasting services and feature pipelines
- infrastructure-as-code and CI/CD templates

Alex wants to build an internal **developer productivity agent** with the Claude Agent SDK. The agent should help engineers:

- explore unfamiliar code paths
- trace legacy logic
- explain how systems fit together
- generate boilerplate safely
- automate repetitive maintenance tasks
- propose changes with the correct file and test scope

---

## A realistic HangryBot request

A new engineer might ask:

> “Find where the support refund threshold is enforced, identify all services and tests that depend on it, and propose a safe way to add a PDK-specific override without breaking ATL passenger rules.”

That is not a pure code-generation task. It combines:

- codebase search
- legacy system understanding
- policy lookup
- cross-file integration analysis
- boilerplate generation
- test impact analysis

This is why the developer productivity scenario naturally sits between **tooling**, **orchestration**, and **context reliability**.

---

## Tool selection and exploration patterns

This scenario should preserve the earlier HangryBot guidance about using the right built-in tool for the job.

Use:

- **Grep** for searching code content such as constant names, error messages, imports, and callers
- **Glob** for locating files by pattern, such as all integration tests or all policy adapters
- **Read** for loading full file contents before reasoning about edits
- **Write** for full-file generation or replacement
- **Edit** for targeted changes only when the anchor text is unique
- **Bash** for tests, linting, or repository-local inspection commands

The key exam lesson is that reliable code exploration is usually incremental:

1. find entry points
2. trace wrappers and exports
3. inspect tests and interfaces
4. form a plan
5. then generate or modify code

An agent that jumps straight to code generation without mapping the dependency chain will often miss hidden coupling.

---

## MCP integration in the developer workflow

The productivity agent should also connect to at least one MCP server so it can look beyond the local repo.

Useful HangryBot MCP integrations include:

- a schema catalog for event payloads and warehouse tables
- a runbook and architecture-doc server
- a Jira or issue-tracker integration
- a deployment status or incident catalog
- a policy repository server

Again, tool descriptions matter. If two tools both seem to “find docs,” the model may choose poorly. Clear descriptions should explain the difference between, for example:

- searching local code
- reading internal architecture docs
- loading structured schema definitions
- looking up open engineering work items

Restrict tool access by role. A code exploration subagent does not need broad deployment controls. A documentation subagent might need read-only doc tools but not Bash.

---

## When to orchestrate with subagents

Most developer requests can be handled by one agent. Some benefit from decomposition.

A strong HangryBot design might create:

- a **code explorer subagent** for tracing logic
- a **test impact subagent** for identifying affected tests
- a **docs subagent** for architecture and policy references
- a **synthesis subagent** that combines findings into a safe implementation plan

The coordinator should spawn these only when the request is broad enough to justify them. Over-decomposition can dilute attention and slow the workflow.

Subagents must receive explicit context because they do not inherit the full parent analysis automatically. That context should include discovered facts such as entry points, file names, relevant policies, and current hypotheses.

---

## Context management for engineering sessions

This scenario is also a good place to study how long sessions decay.

After many turns, an agent may start referencing “the usual refund handler” or “the standard dispatch path” instead of the specific files it actually traced earlier. To avoid that, HangryBot should use:

- scratchpad files with confirmed facts and important paths
- structured summaries between phases of exploration
- forked sessions for comparing alternative approaches
- named session resumption only when the earlier search results remain valid
- explicit notes when previously analyzed files have changed

This is especially important when the agent is helping with legacy systems. Stale context is one of the biggest sources of confident but wrong code suggestions.

---

## Claude Code workflow concepts that still matter here

Even though this scenario is framed as a developer productivity agent, it should still reuse the good Claude Code patterns from the earlier HangryBot work.

That includes:

- project `CLAUDE.md` for universal repo rules
- path-specific `.claude/rules/` for domain-specific conventions
- project slash commands for common flows
- skills with `context: fork` for verbose analysis or codebase mapping
- choosing plan mode for architectural changes and direct execution for narrow fixes

The exam may not ask for every one of these explicitly in this scenario, but a strong answer can still mention them as part of how the productivity agent stays aligned with the repo’s standards.

---

## What a good automation boundary looks like

The developer productivity agent should help engineers accelerate repetitive and exploratory work, but it should not silently make high-risk production decisions.

Good uses include:

- tracing callers and dependencies
- generating boilerplate for a new MCP server or Lambda handler
- explaining a legacy workflow
- drafting tests from existing patterns
- summarizing architectural differences between two implementations

More cautious uses include:

- large refactors touching policy and safety code
- infrastructure changes affecting deployment or IAM
- edits that cross service boundaries with unclear contracts

Those should begin with a plan, not with immediate code generation.

---

## Common exam traps in this scenario

Weak answers often:

- talk only about code generation and ignore exploration
- give the agent too many tools with overlapping purposes
- skip dependency tracing and cross-file analysis
- fail to distinguish local code tools from MCP-backed knowledge tools
- ignore session degradation across long investigations
- treat every request as a candidate for full multi-agent decomposition

Strong answers emphasize:

- disciplined use of Grep, Glob, Read, Write, Edit, and Bash
- precise MCP tool descriptions and scoping
- optional subagent decomposition for broad requests
- scratchpads and summaries for context control
- repo rules and skills as guardrails for generated code

---

## What a strong HangryBot solution looks like

The finished developer productivity agent acts like a smart engineering teammate who can map unfamiliar territory, connect code with docs and schemas, generate safe starting points, and tell the engineer where the real risks are.

That is the point of this merged scenario: the best productivity systems are not just code generators. They are **navigation, reasoning, and automation systems** with controlled tool use and disciplined context handling.
