---
name: mercury-agents
description: "Plan, implement, and verify code changes with minimal redundant context, using abstract planner, refiner, implementer, and reviewer roles. Use for coding tasks that need repository exploration, a plan, or coordination across agents or models, or when the user asks for token-efficient execution; works in a single agent and with any harness or model."
---

# Mercury Agents

Optimize total tokens across planning, execution, handoffs, and corrections. Preserve correctness, requested scope, and required verification. A cheaper configuration or shorter prompt is useful only if it avoids greater rework.

## Choose the smallest workflow

| Evidence from the task | Workflow |
|---|---|
| Local, obvious change; no interface or design decision | Inspect → implement → verify |
| Related files require exploration; architecture is established | Initial plan → plan refinement → implement → verify |
| Cross-cutting behavior, public interfaces, or unresolved architectural tradeoffs | Architecture plan → plan refinement → implement → verify |

File count alone does not determine complexity. Resolve uncertainty with a targeted inspection before adding a planning stage. Reuse an existing plan after checking its assumptions against current code.

Stages are responsibilities, not mandatory separate agents. Stay in one agent when delegation would duplicate exploration or when delegation is unavailable or disallowed. Delegate only bounded independent work that can proceed alongside useful local work and whose benefit justifies its context overhead; dependent stages remain local when the runtime requires independent subtasks. Avoid overlapping file ownership.

## Roles and model selection

Stages map to four abstract roles. Each describes the capability a stage needs, not a specific model:

| Role | Responsibility | Capability profile |
|---|---|---|
| **Planner** | Initial or architecture plan: strategy, boundaries, invariants, acceptance criteria | Economical for a routine initial plan; strongest reasoning for an architecture plan |
| **Refiner** | Check the plan against actual files and symbols; resolve design decisions | Strong reasoning over code and evidence |
| **Implementer** | Edit code, run deterministic checks, fix findings | Reliable code generation, long context, careful tool use |
| **Reviewer** | Read-only plan-adherence review | Most capable critical reading; never edits |

Choose the model for each role yourself: use the least capable available model that can reliably meet the role's profile and the actual difficulty of the work. Scale by the task, not the role name:

- **Mechanical work** (clear spec, isolated change in one or two files, a plan step with no open decisions): a fast, economical model at low or medium effort.
- **Integration and judgment** (multi-file coordination, debugging, adapting to existing patterns): a standard model at medium or high effort.
- **Architecture, plan refinement with unresolved tradeoffs, and the final plan-adherence review**: the most capable available model at high effort. Do not let these default to the session model when a more capable one is available.

Select only among models and effort levels the current runtime actually offers. Discover them from the runtime's tool definitions, documented aliases, or configuration; never copy model identifiers from memory, older sessions, or other skills. When you dispatch a subagent, set the model explicitly, and set the effort level explicitly as well when the runtime supports it, because an omitted value silently inherits the session's or the model's default.

Explicit bindings take precedence over this choice. If the user, project instructions (such as `AGENTS.md` or `CLAUDE.md`), or runtime configuration assign a model, effort level, or named agent to a role, use that binding exactly. If a chosen or bound model is unavailable, use the closest available tier and mention the substitution.

Model choice applies only to stages you actually delegate; work done locally runs on the current model. When the runtime offers no model selection, perform every role with the current model. Never claim to switch models or dispatch an agent without an actual supported dispatch.

## Acquire evidence once

Start with repository instructions, working-tree state, and the relevant entry points. Search filenames and symbols before reading files. Inspect affected types, callers, tests, and nearby conventions; expand only to answer a concrete unresolved question.

Batch independent searches and bound output to relevant matches or ranges. If output is truncated, narrow the query rather than treating omitted results as absent. Reuse observed facts while their files remain unchanged; recheck touched areas after concurrent edits.

## Plan only unresolved decisions

For the initial plan, identify the strategy, affected boundaries, invariants, compatibility constraints, and acceptance criteria. Keep exact file enumeration for plan refinement.

Refine the plan against actual files and symbols. Repository evidence overrides the initial plan: correct nonexistent abstractions or incompatible assumptions before coding.

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

Assign this review to the Reviewer role, delegated with fresh context on the most capable available model when delegation is available and permitted; otherwise perform the same focused pass locally. The sequence is Planner initial plan → Refiner plan refinement → Implementer implementation and deterministic checks → Reviewer review when warranted. An existing validated plan can replace the planning stages when its assumptions still hold.

Give the reviewer only the user requirements and constraints, validated plan, final diff or its accessible pointer, relevant file access, and check results. Review the actual implementation for omitted requirements, incomplete behavior, scope drift, and consequential verification gaps. Treat the plan as a hypothesis: flag conflicts with repository evidence or user requirements rather than demanding blind compliance. Keep this pass read-only and focused; it does not replace specialized review required by the task.

Return only actionable findings with severity, file/symbol, evidence, and the unmet requirement or invariant. If none are found, state that briefly with any material coverage limits; do not imply proof of correctness or repeat the plan.

Route implementation findings to the Implementer for correction and relevant checks. Recheck affected findings and dependent behavior rather than restarting the entire review. Send invalid planning assumptions or new design decisions to the Refiner; involve the Planner only if the strategy changes. Stop the review loop when findings are resolved and relevant checks pass. If a finding remains blocked or recurs without new evidence, report the unresolved issue instead of cycling through agents.

## Finish

Repeat or broaden checks only after relevant edits, failures, or unresolved concerns. Report the implemented behavior, material deviations, checks and outcomes, and remaining limitations concisely in the user's language. Claim token savings only when measured; otherwise describe the avoided overhead.
