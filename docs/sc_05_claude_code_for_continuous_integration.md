# HangryBot Merged Scenario 5: Claude Code for Continuous Integration

## Why this merged scenario exists

This scenario rewrites the exam’s **Claude Code for Continuous Integration** setup for HangryBot and merges in the earlier HangryBot work on:

- prompt engineering for code review and ops reliability
- Claude Code repository configuration
- explicit review criteria and few-shot examples
- multi-pass review architectures for large changes
- structured outputs for automated pipelines

It is designed to feel like a real CI/CD workflow inside a production system where false positives are costly and missed issues are worse.

---

## HangryBot production context

HangryBot now runs code changes through a CI pipeline that touches customer-facing systems, robot operations, policy logic, and GenAI services. The team wants Claude Code in CI to help with three tasks:

- automated code review on pull requests
- targeted test generation and coverage-gap detection
- actionable feedback posted back to engineers

The company cannot afford a noisy reviewer. If the automated review comments are full of low-value suggestions, developers will stop trusting them. If the tool misses real issues in refund policy or robot fallback logic, production risk increases.

---

## The pull request type you should picture

A representative HangryBot pull request might change:

- the ATL robot dispatch fallback rules
- a PDK compensation path for concierge catering
- a retrieval prompt used by Ryan’s support copilot
- an API contract in the GenAI gateway
- associated tests and deployment configuration

This is exactly the kind of change where **multi-pass review** beats a single giant review prompt.

---

## How Claude Code should run in CI

A strong solution uses Claude Code in **non-interactive mode** so the pipeline never hangs waiting for input. The run should produce **machine-parseable structured output**, not free-form prose, so the CI system can post inline comments or summarize findings predictably.

The review job should be given:

- the changed files
- relevant project instructions from `CLAUDE.md`
- any path-specific rules for touched files
- existing test files or coverage context when asking for new tests
- prior review findings when re-running after an updated commit

That last point matters because otherwise the tool may repeatedly report already-addressed issues.

---

## Prompt engineering principles for this scenario

This merged scenario should preserve the earlier HangryBot prompt-engineering lessons.

### 1. Use explicit review criteria
Do not tell the model to “be conservative” or “only report high-confidence issues.” Those instructions are vague.

Instead, define exactly what to report, such as:

- logic changes that can break refund eligibility
- missing tests for safety-critical robot fallback behavior
- contradictions between policy comments and actual code
- API changes that alter structured output or error handling

Also define what *not* to report, such as:

- minor style preferences
- already-established local patterns that are intentional
- speculative performance concerns with no evidence

### 2. Use few-shot examples
A few strong examples are especially helpful for ambiguous review categories like:

- when a missing test is serious enough to comment on
- when a docstring mismatch is a true bug risk versus harmless wording drift
- when an ops prompt change introduces a policy risk rather than just a phrasing difference

### 3. Split the review into passes
A good HangryBot review pipeline often works best as:

- per-file local analysis passes
- then a separate cross-file integration pass

This reduces attention dilution and helps the system catch interface mismatches that a single per-file pass would miss.

---

## Structured outputs and schema design

CI is one of the clearest cases for **structured output**. A finding record should usually include:

- file path
- location or line range
- issue title
- severity
- rationale
- suggested fix or verification step
- category, such as logic bug, missing test, contract change, or policy regression
- optional `detected_pattern` field for later analysis of false positives

The point is not just syntax safety. Structured outputs let HangryBot measure which categories are noisy, which few-shot examples are working, and which findings developers dismiss most often.

---

## Test generation in CI

The same system may also generate tests, but that should be done carefully.

Good practice includes:

- passing existing test files into the context so the model avoids duplicates
- defining the test framework and fixture conventions in `CLAUDE.md`
- asking for tests that cover business-relevant edge cases, not generic boilerplate only
- reviewing generated tests independently from the session that suggested the code change

The exam often rewards the idea that **the same session that generated code is not the best reviewer of that code**.

---

## When to use synchronous versus batch processing

This scenario is also a good place to mention **Message Batches API** tradeoffs.

For HangryBot:

- **blocking pre-merge reviews** should use synchronous workflows
- **overnight audit jobs**, large documentation sweeps, or bulk test generation may use batches

Batch processing can save cost, but it does not fit workflows that need immediate feedback. That distinction is important.

---

## Common exam traps in this scenario

Weak answers often:

- rely on vague prompt instructions instead of explicit criteria
- use a single giant review prompt for complex multi-file changes
- ignore the value of few-shot examples
- let the generator session review its own output
- return prose instead of structured findings
- run batch workflows for latency-sensitive pre-merge checks
- fail to include repo-specific standards in `CLAUDE.md`

Strong answers emphasize:

- explicit categories and severity rules
- few-shot examples for ambiguous cases
- multi-pass review design
- independent review sessions
- structured output schemas
- careful test-generation prompts with existing tests in context
- synchronous vs batch tradeoffs

---

## What a strong HangryBot solution looks like

The finished CI design gives engineers concise, high-signal review comments, better test suggestions, and less noise. It knows the difference between a style nit and a real logic regression. It uses repo-specific standards, reviews large changes in multiple passes, and posts structured findings that the pipeline can consume automatically.

That is the real lesson of this scenario: **prompt quality and workflow architecture matter as much as model capability** when Claude Code becomes part of continuous integration.
