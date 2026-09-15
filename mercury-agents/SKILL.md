---
name: mercury-agents
description: "Plan and implement code changes with minimal redundant context and reasoning. Use when optimizing coding token usage or coordinating repository exploration, planning, and implementation across agents; also supports single-agent execution."
---

# Mercury Agents

Optimize total tokens across planning, execution, handoffs, and corrections. Preserve correctness, requested scope, and required verification. A cheaper model or shorter prompt is useful only if it avoids greater rework.

## Choose the smallest workflow

| Evidence from the task | Workflow |
|---|---|
| Local, obvious change; no interface or design decision | Inspect → implement → verify |
| Related files require exploration; architecture is established | Repository plan → implement → verify |
| Cross-cutting behavior, public interfaces, or unresolved architectural tradeoffs | Architecture decision → repository plan → implement → verify |

File count alone does not determine complexity. Resolve uncertainty with a targeted inspection before adding a planning stage. Reuse an existing plan after checking its assumptions against current code.

Stages are responsibilities, not mandatory separate agents. Stay in one agent when delegation would duplicate exploration or when delegation is unavailable or disallowed. Delegate only bounded independent work that can proceed alongside useful local work and whose benefit justifies its context overhead; dependent stages remain local when the runtime requires independent subtasks. Avoid overlapping file ownership.

When model selection is supported and permitted, the source workflow's preferred roles are Astra at low effort for architecture, Sol at medium for repository planning, and Terra at medium for implementation. Treat these as preferences, not required model availability or price rankings. Honor the user's model choice and runtime constraints; use the current model when selection is unavailable. Never claim to switch models without an actual supported dispatch.

## Acquire evidence once

Start with repository instructions, working-tree state, and the relevant entry points. Search filenames and symbols before reading files. Inspect affected types, callers, tests, and nearby conventions; expand only to answer a concrete unresolved question.

Batch independent searches and bound output to relevant matches or ranges. If output is truncated, narrow the query rather than treating omitted results as absent. Reuse observed facts while their files remain unchanged; recheck touched areas after concurrent edits.

## Plan only unresolved decisions

For architecture work, identify the strategy, affected boundaries, invariants, compatibility constraints, and acceptance criteria. Keep exact file enumeration for repository planning.

Ground the implementation plan in actual files and symbols. Repository evidence overrides upstream proposals: correct nonexistent abstractions or incompatible assumptions before coding.

Keep one compact working brief, in context or a workspace artifact when handoff or resumption warrants it:

- **Goal and constraints:** requested behavior, acceptance criteria, scope exclusions.
- **Evidence and changes:** file/symbol pointers, validated facts, intended behavioral changes in dependency order.
- **Checks:** relevant commands and behaviors they establish.
- **Open decisions:** only unknowns that could change implementation.

Omit empty fields. Do not generate a second report that duplicates this brief or prewrite the patch as prose.

## Execute and hand off compactly

Inspect planned code before editing, make the smallest coherent change, and follow repository conventions. Resolve local implementation details directly.

For an authorized handoff, pass the task, relevant constraints, the current brief or its path, owned files, and expected result. Use fresh context where supported. Preserve critical requirements explicitly; reference source files instead of copying entire files, conversations, exploration logs, or discarded reasoning. Confirm referenced artifacts are accessible to the receiving agent.

The recipient returns changed files, behavioral outcome, check results, and blockers. Integrate these facts into the current brief instead of accumulating reports.

If evidence invalidates the plan, pause the affected edits and revisit only the failed assumption. Supply the evidence, current diff, and decision needed. Return to architecture only if boundaries, invariants, or strategy change. Do not repeat an unsuccessful approach without new evidence; report a blocker when progress requires missing input or access.

## Verify against the plan when warranted

Run checks appropriate to the change and repository requirements; inspect the final diff for omissions and unrelated edits. Prefer deterministic tests, type checks, lint, and builds where they establish the needed property.

After these checks, add a focused plan-adherence review when risk or complexity leaves meaningful gaps: interacting changes across components, public-interface or compatibility changes, security/concurrency/transactional behavior, or acceptance criteria poorly covered by automated checks. Skip this extra stage for local, obvious changes adequately verified by those checks. File count alone is not a trigger.

For this review, prefer Luna at high effort when model selection and delegation are supported and permitted; otherwise perform the same focused pass locally. Honor the model and dispatch constraints above. The optional sequence is Sol plan → Terra implementation → deterministic checks → Luna review. An existing validated plan can serve the same role as Sol's output.

Give the reviewer only the user requirements and constraints, validated plan, final diff or its accessible pointer, relevant file access, and check results. Review the actual implementation for omitted requirements, incomplete behavior, scope drift, and consequential verification gaps. Treat the plan as a hypothesis: flag conflicts with repository evidence or user requirements rather than demanding blind compliance. Keep this pass read-only and focused; it does not replace specialized review required by the task.

Return only actionable findings with severity, file/symbol, evidence, and the unmet requirement or invariant. If none are found, state that briefly with any material coverage limits; do not imply proof of correctness or repeat the plan.

Route implementation findings to Terra, or the current implementer, for correction and relevant checks. Recheck affected findings and dependent behavior rather than restarting the entire review. Send invalid planning assumptions or new design decisions to Sol, or the current planner; involve architecture only if the strategy changes. Stop the review loop when findings are resolved and relevant checks pass. If a finding remains blocked or recurs without new evidence, report the unresolved issue instead of cycling through agents.

## Finish

Repeat or broaden checks only after relevant edits, failures, or unresolved concerns. Report the implemented behavior, material deviations, checks and outcomes, and remaining limitations concisely in the user's language. Claim token savings only when measured; otherwise describe the avoided overhead.
