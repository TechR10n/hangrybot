# HangryBot Merged Scenario 1: Customer Support Resolution Agent

## Why this merged scenario exists

This scenario consolidates the original **Customer Support Resolution Agent** exam setup with the earlier HangryBot materials on:

- Claude Agent SDK agent loops for ATL and PDK operations
- MCP tool design and selection reliability
- long-session context management during storm-day incidents
- escalation and human-in-the-loop decision patterns
- structured extraction of case details from messy support inputs

The result is a single exam-ready scenario that preserves all of those concepts inside one believable production story.

---

## HangryBot production context

Six months after launch, HangryBot has proven that people will order disruption-driven meals in the **ATL terminal pilot zone** and that **PDK FBO partners** will use concierge catering recommendations for private flights. What has not scaled cleanly is support.

Ryan’s team now handles a messy mix of requests:

- ATL passengers asking for refunds or credits because robot-delivered meals arrived late
- passengers reporting missing items, allergy mistakes, or incorrect pickup instructions
- billing disputes from travelers who ordered during weather disruptions and were charged twice after retries
- PDK FBO desk agents requesting premium catering exceptions for charter clients
- executive assistants asking for invoice corrections or manual adjustments
- ambiguous cases where a service failure might have been caused by weather, robot congestion, kitchen delay, or a bad handoff

Leadership wants **80% or better first-contact resolution**, but only if the system knows when *not* to act on its own.

---

## The specific problem you are solving

You are building a **customer support resolution agent** with the **Claude Agent SDK**. The agent must reason through incomplete, high-ambiguity requests and interact with backend systems through **custom MCP tools**.

A typical customer message might be:

> “My order at ATL never showed up, your robot app kept changing the ETA, and I want a human unless you can actually fix this right now.”

Or:

> “Our PDK catering order changed after cutoff because the charter passenger count changed. Can you override the premium bundle rule?”

The system must distinguish among:

- resolvable routine cases
- cases that need more data
- cases blocked by policy
- cases where the customer explicitly wants a human
- cases where the agent cannot make meaningful progress

---

## Core toolset and MCP design

A clean HangryBot support toolset might include:

- `get_customer_or_partner`
- `lookup_order`
- `lookup_robot_delivery`
- `lookup_policy_article`
- `lookup_airport_incident_context`
- `issue_credit`
- `process_refund`
- `escalate_to_human`
- `extract_case_details`

The most important design principle is that **tool descriptions must clearly differentiate similar tools**. For example, `lookup_order` should be for transactional order state, while `lookup_airport_incident_context` should be for weather, kitchen, robot, or queue-level disruptions. If both tools vaguely say “get information about customer problems,” the model will misroute.

Each tool should return **structured error responses** instead of generic failures. A strong MCP error shape includes:

- `isError: true`
- `errorCategory`: `transient`, `validation`, `permission`, or `business`
- `isRetryable`: `true` or `false`
- `message`: human-readable explanation
- `attemptedAction`
- `partialResults`

This matters because the agent should retry a timeout differently than a policy violation. A refund blocked because it exceeds an approval limit is not the same as a temporary database failure.

---

## The agentic loop you are expected to understand

This scenario is ideal for demonstrating a **complete Claude Agent SDK loop**.

A strong implementation does the following:

1. Send the user request to Claude.
2. Inspect `stop_reason`.
3. If `stop_reason` is `tool_use`, execute the requested tool.
4. Append the tool result to the conversation history.
5. Send the updated conversation back to Claude.
6. Continue until `stop_reason` becomes `end_turn`.

The loop should **not** rely on parsing assistant text like “I’m done” or “no further action needed.” It should also avoid arbitrary iteration caps as the main completion mechanism.

In HangryBot, tool results must be appended in a way that preserves the facts the next step depends on:

- customer or partner ID
- order ID
- airport and location
- timestamps
- amount charged
- compensation already issued
- robot mission status
- policy article reference

If these facts are not preserved, the model may answer based on “typical” support flows rather than the actual incident.

---

## Session management and context reliability

Support incidents often take multiple turns and accumulate noisy tool outputs. That is why this scenario also inherits the earlier HangryBot context-management patterns.

A good design keeps a structured **case facts block** separate from the raw conversation history. That block should persist core transactional facts such as:

- customer or partner identifier
- order number and current status
- airport and service mode
- amounts, refunds, credits, and policy thresholds
- explicit customer preferences such as “wants human now”
- unresolved questions

For long investigations, the agent should also maintain a **scratchpad** or session record that stores only the relevant normalized fields instead of entire raw JSON payloads. This avoids the classic failure mode where huge order lookups and robot telemetry crowd out the actual problem.

A good PostToolUse normalization layer can convert:

- Unix timestamps into ISO 8601
- numeric status codes into readable labels
- internal compensation enums into customer-safe language

That normalization makes the model’s reasoning more reliable and reduces wasted tokens.

---

## When to spawn subagents

Most cases should be handled by a single support agent. Some cases should trigger **subagent delegation** through the `Task` tool.

Example: a high-value ATL case may include three concerns at once:

- a refund request
- possible robot fleet failure
- uncertainty about whether a weather policy exception applies

A coordinator agent can decompose that into:

- a policy subagent
- an order and billing subagent
- an ops incident subagent

The coordinator must pass context explicitly because subagents do **not** inherit the parent conversation automatically. The prompt should include structured facts, not just a vague summary.

The coordinator should then aggregate results, look for gaps, and decide whether it has enough information to resolve or escalate.

---

## Escalation and human-in-the-loop rules

This scenario must preserve the earlier HangryBot escalation logic.

The agent should escalate when:

- the customer explicitly asks for a human
- policy is ambiguous or silent
- multiple customers match the provided identifiers and clarification is required
- the requested refund exceeds the auto-approval threshold
- a safety or allergy incident is reported
- tool failures prevent meaningful progress
- the model’s confidence is low or the evidence conflicts

The agent should **not** escalate just because the user sounds frustrated if the issue is straightforward and policy-supported. It should acknowledge frustration while still offering a resolution path when appropriate.

The best design uses **deterministic gates**, not just prompts, for sensitive actions. For example:

- block `process_refund` above a threshold through a tool interception hook
- require verified customer identity before applying monetary compensation
- redirect policy-gap cases to `escalate_to_human`

When escalating, the system should create a **structured handoff summary** that includes:

- customer or partner ID
- root cause analysis so far
- order status
- proposed resolution
- blocked action or policy gap
- recommended next step

That way a human agent does not need the entire conversation transcript to continue.

---

## Common exam traps in this scenario

A weak answer will often:

- let the model guess which of several matched customers is correct
- treat all tool failures the same
- use prompt instructions instead of programmatic gates for refund rules
- forget to append tool results back into the conversation
- keep full raw tool outputs in context until the session becomes incoherent
- escalate based only on sentiment instead of explicit rules and policy gaps

A strong answer will emphasize:

- the `tool_use` / `end_turn` loop
- structured tool errors
- normalized case facts
- selective use of subagents
- deterministic escalation rules
- human-review summaries
- context trimming and scratchpads

---

## What a strong HangryBot solution looks like

The finished support system is not just a chatbot. It is a **policy-aware resolution agent** that can investigate ATL passenger issues, PDK partner exceptions, and billing disputes with reliable tool use and disciplined context management.

It resolves routine cases autonomously, asks for clarification when identifiers are ambiguous, delegates when a case spans billing plus operations plus policy, and escalates cleanly when policy or safety boundaries require human judgment.

That combination is exactly what makes this scenario such a strong exam case: it forces you to connect **agent loops, MCP design, reliability patterns, and human oversight** in one production setting.
