# HangryBot Merged Scenario 2: Code Generation with Claude Code

## Why this merged scenario exists

This scenario takes the exam’s **Code Generation with Claude Code** setup and folds in the earlier HangryBot work on:

- configuring Claude Code for a real repository
- using `CLAUDE.md` and path-specific rules
- creating project skills with frontmatter such as `context: fork` and `allowed-tools`
- integrating MCP servers into daily engineering work
- managing long context during large refactors
- applying prompt-engineering techniques to code generation and review

The goal is to make the scenario feel like real software development inside HangryBot, not a generic coding exercise.

---

## HangryBot production context

Six months after launch, the prototype phase is over. HangryBot now has a production codebase that spans:

- ATL terminal ordering services
- PDK concierge and partner workflows
- the GenAI gateway
- MCP servers for internal tools and policy lookup
- retrieval pipelines and vector indexing jobs
- robot dispatch services
- data science training code
- AWS infrastructure and deployment templates

Engineers use **Claude Code** for generation, refactoring, debugging, documentation, and architecture exploration. The challenge is not whether Claude Code can help. The challenge is how to configure it so it helps *consistently* without violating domain rules around safety, refunds, airport operations, and partner contracts.

---

## The development situation

Alex asks the team to migrate the support stack from a proof-of-concept implementation to a maintainable production standard.

At the same time:

- Emma is updating feature-engineering code for delay-driven meal forecasts
- Liam is changing robot route fallback logic in the ATL pilot zone
- Ryan’s team is revising support prompts and compensation workflows
- a new engineer must trace the legacy refund path without breaking PDK partner exceptions

This is where **Claude Code configuration** becomes part of the product, not just a personal preference.

---

## What the repository needs

A strong HangryBot setup uses a **configuration hierarchy**.

### Project-level guidance
A project `CLAUDE.md` should define universal expectations such as:

- never bypass refund policy gates
- never change robot safety thresholds without updating tests
- preserve source attribution in retrieval features
- prefer structured outputs and typed interfaces for GenAI boundaries
- do not remove audit logging from customer-support flows

### Path-specific rules
Use `.claude/rules/` files with path scoping to load only the rules relevant to the files being edited.

Examples:

- `services/robot-dispatch/**/*` -> rules for safety, geofencing, and fallback behavior
- `services/support/**/*` -> rules for compensation policy and escalation
- `infrastructure/**/*` -> rules for IAM least privilege, deployment rollback, and observability
- `**/*.test.ts` or `**/*.spec.py` -> testing conventions and fixture guidance

This avoids stuffing every instruction into one giant file and reduces irrelevant context.

### Skills and slash commands
HangryBot should also define reusable commands and skills such as:

- `/trace-refund-flow`
- `/storm-readiness-review`
- `/generate-mcp-tool`
- `/write-incident-tests`

Skills should use frontmatter intentionally:

- `context: fork` to isolate verbose exploration
- `allowed-tools` to limit risky actions
- `argument-hint` to prompt for required parameters

That keeps exploratory work from polluting the main session and makes team workflows reproducible.

---

## MCP integration for real engineering work

Claude Code in HangryBot should not be limited to local files. Engineers also need access to shared systems.

A realistic project might connect at least one MCP server for:

- Jira issues or sprint tickets
- internal architecture docs and runbooks
- database schema catalogs
- policy repositories
- incident summaries or partner documentation

The important lesson is that **MCP tool descriptions and resources matter**. If the internal doc tool is vaguely described, Claude may ignore it and rely on incomplete local context. Strong MCP descriptions should say exactly what data is available, what inputs they accept, and when to use them instead of built-in file tools.

HangryBot should prefer project-scoped `.mcp.json` for shared team integrations and reserve user-scoped configs for personal experiments.

---

## Plan mode vs direct execution

This scenario should explicitly test when to use **plan mode** and when to use **direct execution**.

### Use plan mode when:
- the change spans many files
- architectural choices are still open
- you are migrating a service boundary
- there are safety, policy, or infrastructure implications
- the engineer does not yet understand the legacy code path

Example: migrating the GenAI gateway from a single-model path to a routed abstraction that supports fallback providers, structured outputs, and audit logging.

### Use direct execution when:
- the change is small and well understood
- the file boundary is narrow
- the failure is obvious
- there is a clear test or stack trace to guide the fix

Example: adding a null check to prevent a robot ETA service from crashing when a battery metric is missing.

A common exam mistake is treating plan mode as always better. The correct answer is to match the mode to the uncertainty and blast radius of the change.

---

## Code exploration patterns you should mention

This merged scenario should retain the practical file-navigation patterns from the earlier HangryBot materials.

Use:

- **Grep** to search code content such as function names, error messages, imports, and policy constants
- **Glob** to find files by name or extension patterns
- **Read** to inspect full files before editing
- **Edit** only when the target anchor is unique
- **Write** after Read when Edit is ambiguous or unreliable

A strong answer usually emphasizes *incremental exploration*:

1. find the entry point
2. trace imports and callers
3. inspect tests and interfaces
4. map the change
5. then implement

That is better than reading dozens of files up front or letting the model guess the architecture.

---

## Context management during long coding sessions

Claude Code sessions degrade if they accumulate stale tool outputs, old code snippets, and obsolete assumptions.

HangryBot engineers should use:

- **forked sessions** for comparing approaches
- named session resumption only when prior results are still valid
- fresh sessions with structured summaries when the code has changed materially
- scratchpad notes for discovered facts such as entry points, invariants, test gaps, and blocked dependencies
- `/memory` or equivalent checks to verify which instruction files are loaded

The crucial concept is that context should be treated as a managed asset. Large refactors often fail not because the model cannot code, but because the session is carrying too much stale discovery output.

---

## Prompting for better generated code

This scenario should also preserve the earlier prompt-engineering guidance.

Better HangryBot code-generation prompts include:

- concrete examples of expected transformations
- explicit constraints such as “do not change public API shape” or “preserve policy logging”
- references to existing fixtures and test patterns
- review criteria for acceptable versus unacceptable changes

Few-shot examples are especially useful when generating or refactoring code that touches ambiguous business logic, such as refund eligibility or robot fallback conditions.

---

## Common exam traps in this scenario

Weak answers tend to:

- put everything into one monolithic `CLAUDE.md`
- ignore path-scoped rules
- use user-level config for team-critical instructions
- resume stale sessions without telling Claude which files changed
- let Claude perform wide refactors in direct execution mode without planning
- connect too many MCP tools without clear descriptions
- treat skills and slash commands as interchangeable with always-loaded project rules

Strong answers emphasize:

- the config hierarchy
- path-specific rules
- skills with `context: fork`
- MCP integration with precise tool descriptions
- plan mode for architectural work
- direct execution for contained fixes
- disciplined context management across long sessions

---

## What a strong HangryBot solution looks like

In the best version of this scenario, Claude Code becomes part of the team’s engineering operating model. New engineers can safely explore the repo. Risky files load the right rules automatically. Repetitive tasks become reusable skills. MCP integrations expose tickets, docs, and schemas without forcing engineers to leave the workflow. Large changes start with planning, small changes go straight to implementation, and context is managed deliberately instead of being allowed to decay.

That is the real lesson of this scenario: **Claude Code works best when the repository itself is configured as a teaching and control surface**.
