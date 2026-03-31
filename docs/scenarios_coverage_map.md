# HangryBot Consolidated Scenario Map: 13 Original Scenarios into 6 Exam-Aligned Scenarios

This index shows how the **6 exam-style scenarios** were rewritten to absorb the earlier **7 HangryBot-specific scenarios** so that the concepts and technology were preserved instead of dropped.

## New consolidated scenario set

1. **Customer Support Resolution Agent**  
   File: `hangrybot_merged_scenario_01_customer_support_resolution_agent.md`

2. **Code Generation with Claude Code**  
   File: `hangrybot_merged_scenario_02_code_generation_with_claude_code.md`

3. **Multi-Agent Research System**  
   File: `hangrybot_merged_scenario_03_multi_agent_research_system.md`

4. **Developer Productivity with Claude**  
   File: `hangrybot_merged_scenario_04_developer_productivity_with_claude.md`

5. **Claude Code for Continuous Integration**  
   File: `hangrybot_merged_scenario_05_claude_code_for_continuous_integration.md`

6. **Structured Data Extraction**  
   File: `hangrybot_merged_scenario_06_structured_data_extraction.md`

---

## Coverage mapping

| Original source scenario | Where it now lives | Key concepts preserved |
|---|---|---|
| Exam Scenario 1: Customer Support Resolution Agent | New Scenario 1 | Claude Agent SDK loop, support resolution, MCP tools, escalation |
| Exam Scenario 2: Code Generation with Claude Code | New Scenario 2 | CLAUDE.md, rules, slash commands, skills, plan mode vs direct execution |
| Exam Scenario 3: Multi-Agent Research System | New Scenario 3 | coordinator/subagent design, Task tool, synthesis, citation workflows |
| Exam Scenario 4: Developer Productivity with Claude | New Scenario 4 | built-in tools, MCP integration, codebase exploration, automation |
| Exam Scenario 5: Claude Code for Continuous Integration | New Scenario 5 | code review, test generation, feedback pipelines, false-positive control |
| Exam Scenario 6: Structured Data Extraction | New Scenario 6 | tool-use schemas, validation-retry loops, optional fields, downstream integration |
| Prior Scenario 1: Claude Agent SDK agent loop for ATL/PDK ops | New Scenarios 1 and 3 | tool loop lifecycle, orchestration, session management, ops context |
| Prior Scenario 2: Claude Code setup for the HangryBot repo | New Scenarios 2, 4, and 5 | config hierarchy, path rules, skills, MCP setup |
| Prior Scenario 3: MCP tool design and selection reliability | New Scenarios 1, 3, and 4 | clear tool descriptions, scoped tool access, structured errors |
| Prior Scenario 4: Structured extraction pipeline for catering and incident intake | New Scenarios 1 and 6 | extraction schemas, validation, operational document normalization |
| Prior Scenario 5: Prompt engineering for code review and ops reliability | New Scenarios 2 and 5 | few-shot examples, explicit criteria, multi-pass review |
| Prior Scenario 6: Context management during long storm-day investigations | New Scenarios 1, 3, 4, and 6 | scratchpads, structured facts, context trimming, long-session reliability |
| Prior Scenario 7: Escalation and human-in-the-loop workflows | New Scenarios 1, 3, and 6 | escalation triggers, policy gaps, human review summaries, confidence routing |

---

## Why the merge works

The six new scenarios were chosen because they match the exam’s structure while still covering the HangryBot-specific material:

- **Scenario 1** absorbs support, tool calling, reliability, and escalation.
- **Scenario 2** absorbs repository setup, Claude Code workflow design, and config discipline.
- **Scenario 3** absorbs multi-agent orchestration, synthesis, and source-preserving research.
- **Scenario 4** absorbs practical engineering assistance with built-in tools and MCP systems.
- **Scenario 5** absorbs review prompting, structured findings, CI integration, and test generation.
- **Scenario 6** absorbs extraction, schema design, retry loops, batching, and confidence-based routing.

Together, the six new scenarios preserve all thirteen source scenarios without scattering the same ideas across too many overlapping files.

---

## Recommended study order

1. Start with **Scenario 1** to lock in the Claude Agent SDK loop and escalation rules.
2. Read **Scenario 2** and **Scenario 4** together for Claude Code, repo setup, and developer workflows.
3. Read **Scenario 3** for coordinator/subagent orchestration and citation-preserving synthesis.
4. Read **Scenario 5** for prompt engineering, code review precision, and CI patterns.
5. Finish with **Scenario 6** for structured extraction, validation, batching, and human review.
