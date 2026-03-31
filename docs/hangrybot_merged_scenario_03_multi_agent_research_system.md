# HangryBot Merged Scenario 3: Multi-Agent Research System

## Why this merged scenario exists

This scenario rewrites the exam’s **Multi-Agent Research System** into HangryBot’s world and merges in the earlier HangryBot work on:

- Claude Agent SDK orchestration patterns
- MCP tool design and subagent tool scoping
- context management for long, source-heavy investigations
- structured claim-source mappings and report synthesis
- escalation and human review for ambiguous findings

The result is a scenario about research that is broad enough for exam preparation but specific enough to reflect real production work.

---

## HangryBot production context

Maya, the product and partnerships lead, wants a decision memo on the next place HangryBot should invest after stabilizing ATL and PDK. She wants a report comparing:

- expanding the ATL pilot zone
- adding another PDK FBO partner
- promoting **BOS**, **TPA**, or **SJU** from feeder/reference market to live deployment market

The report must combine:

- public airport and partner information
- HangryBot’s internal incident summaries
- operational metrics from ATL and PDK
- support burden and compensation trends
- deployment complexity and partner readiness

A single agent can produce a shallow answer. The company needs a **multi-agent research system** that can produce a comprehensive, cited report.

---

## The agent roles

The exam version names four agent roles, and HangryBot can preserve them cleanly:

- a **web research subagent** that looks for current public facts
- a **document analysis subagent** that reads partner docs, internal runbooks, incident summaries, and contracts
- a **synthesis subagent** that merges claims, resolves or annotates conflicts, and identifies gaps
- a **reporting subagent** that turns structured findings into an executive-ready output

A **coordinator agent** sits above them and decides which subagents to invoke, what context to pass, and whether the final result is complete enough to present.

---

## The orchestration pattern that matters

This scenario is really about getting the **hub-and-spoke pattern** right.

The coordinator should:

1. inspect the query and determine which subagents are needed
2. spawn parallel subagents through the `Task` tool when possible
3. pass explicit context, because subagents do not inherit the full parent session automatically
4. collect structured findings rather than raw narrative outputs
5. evaluate whether coverage is sufficient
6. re-delegate targeted follow-up work if gaps remain
7. send the final structured findings to the reporting agent

A strong answer explicitly notes that the coordinator should **not** always invoke every subagent for every request. If the question is narrowly about concession readiness, the system may not need the full pipeline. Dynamic decomposition is better than rigid over-orchestration.

---

## How context should be passed

This scenario inherits the earlier HangryBot context-management guidance.

The coordinator should not pass giant verbatim logs into every subagent. It should pass:

- the precise research question
- scope boundaries
- structured background facts
- relevant source lists or excerpts
- required output schema
- quality criteria such as citation requirements or conflict annotation rules

Subagents should return **structured claim-source mappings**. For each important claim, the output should include:

- the claim text
- source URL or document name
- date of publication or collection
- excerpt or evidence pointer
- confidence or support level
- notes on conflict or uncertainty

This is how HangryBot avoids losing attribution during summarization. It is also how the synthesis agent can distinguish a true contradiction from a time gap between sources.

---

## MCP and tool design in this scenario

The research system will likely mix built-in web/document tools with MCP integrations for internal knowledge.

Useful internal resources might include:

- incident report catalogs
- partner document indexes
- airport expansion scorecards
- policy and contract repositories
- archived support trend summaries

Good MCP tool descriptions matter because the coordinator and subagents must know when to use a document lookup tool, when to use a search tool, and when to rely on a resource catalog instead of exploratory calls.

The best tool set is usually **small and role-specific**. A synthesis agent should not be given broad search tools unless there is a frequent, narrow need such as a `verify_fact` tool. Too many tools increase misrouting.

---

## Error handling and recovery

This scenario is a strong place to show that subagents should return **structured error context**, not vague failures.

For example, when a document repository times out, the subagent should report:

- failure type
- attempted query
- whether the error is retryable
- partial results already collected
- possible alternatives

The coordinator can then decide whether to retry, reroute, or continue with a coverage gap note.

That distinction is important because “no relevant SJU concession document found” is different from “document system unavailable.” One is a valid empty result. The other is a failed lookup.

---

## Human review and escalation in the research flow

Not every research report needs human intervention, but some do.

HangryBot should require human review when:

- the final recommendation depends on unresolved source conflicts
- a key source is unavailable
- the report contains policy, legal, or partner-sensitive statements
- the coordinator cannot achieve required coverage
- the output could drive a significant investment decision

In that case, the reporting subagent should still produce a structured draft that clearly separates:

- well-supported findings
- contested findings
- missing evidence
- recommended follow-up questions

That makes the human reviewer more effective and prevents redoing the entire analysis manually.

---

## Common exam traps in this scenario

Weak answers often:

- route every task through every subagent regardless of need
- assume subagents inherit coordinator context automatically
- let subagents return unstructured essays with no citations
- lose publication dates and source locations during synthesis
- suppress missing-data errors as if they were successful empty results
- generate a polished report before checking whether coverage is sufficient

Strong answers emphasize:

- a coordinator with the `Task` tool
- isolated subagent contexts
- structured outputs with claim-source mappings
- iterative refinement loops
- role-specific tool sets
- structured error propagation
- human review for ambiguous or decision-critical reports

---

## What a strong HangryBot solution looks like

In the best version of this scenario, the coordinator asks only the right subagents to work, those subagents return structured, attributable findings, the synthesis layer identifies unsupported claims before they make it into the report, and the final report shows not just conclusions but also where the evidence came from and where gaps remain.

That is what turns a generic multi-agent demo into a credible HangryBot research system: it respects **orchestration discipline, source attribution, and context boundaries** while still producing something useful enough for a real expansion decision.
