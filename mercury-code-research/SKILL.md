---
name: mercury-code-research
description: "Plan and implement local code grounded in scientific papers, using existing Markdown analyses or local PDFs. Use when implementing, reproducing, adapting, or integrating a paper's methodology, algorithm, or framework for a coding request; not for analysis or comparison alone."
---

# Mercury Code Research

Translate the parts of scientific papers relevant to the user's request into a grounded implementation plan, resolve material decisions, then implement locally using `mercury-agents`. Support one paper or a collection; prior analysis is optional.

## Establish scope and evidence

Respect the user's selected methodology or paper sections, requested behavior, language, framework, repository, data, and compute constraints. Distinguish faithful reproduction, a targeted component, and adaptation. Do not expand a component request into a full reproduction. Ask only for missing decisions that materially affect the work.

Identify the local corpus and target codebase from the request and workspace; ask for their locations if ambiguous. Inspect repository instructions, relevant interfaces, and checks before planning. Read sources and code and save the plan before editing implementation code. Resolve material decisions as described below.

Match PDFs and Markdown by paper title, authors, version, and source metadata rather than filename alone. Reuse relevant outputs of `mercury-analyze`, `mercury-compare`, or other identifiable analyses without rerunning those workflows. Their analysis-only restrictions do not prevent this skill from proposing engineering choices.

Reuse the shared paper metadata from existing analyses when available. Check it against the sources actually consulted and preserve paper identifiers and version distinctions in the report or plan.

Older analyses without this block remain usable: reconstruct only the metadata needed for the task from available evidence, without requiring the analysis to be rewritten.

- Prefer existing Markdown for discovery, context, and documented methodological explanations. Read relevant passages in context.
- When a local PDF is available, directly verify implementation-critical equations, dimensions, objectives, initialization, preprocessing, numerical constraints, and stopping criteria relevant to the requested component, even when the Markdown appears complete.
- Read additional PDF passages when the analysis is missing, ambiguous, or contradictory. Inspect equations, algorithms, figures, tables, and appendices directly when extraction loses meaning. Use available PDF-reading guidance when needed.
- If the PDF is unavailable or unreadable, identify which critical details rely only on the analysis. Proceed when that evidence is sufficient for the requested scope; ask for clarification when unresolved details would materially change behavior.
- Prefer the PDF for a disputed claim about the paper and record discrepancies. If only Markdown is available, disclose the coverage limit; never imply direct PDF verification.
- Keep paper grounding within supplied local sources unless the user authorizes additional research. Technical documentation can inform API usage but is not evidence for the paper's method. A cited work is not a consulted source unless actually read.

Read the requested parts and their methodological dependencies, not every paper indiscriminately. Never invent unreported steps, hyperparameters, or experimental settings.

## Produce the implementation plan

When writing equations in Markdown deliverables or responses, use `$equation$` for inline math and `$$equation$$` for display math. For multiline display equations, put the opening and closing `$$` on separate lines. Do not use `\(...\)` or `\[...\]` as math delimiters, escape the dollar delimiters, or wrap rendered equations in code spans or code fences.

Extract relevant inputs, outputs, assumptions, equations, symbols, processing steps, objectives, and evaluation conditions. Capture shapes, units, initialization, preprocessing, numerical constraints, and stopping criteria where they affect implementation.

Separate **source-reported facts**, **user requirements**, and **engineering choices or unresolved assumptions**. Label deviations as adaptations; do not silently combine incompatible methods. Where missing scientific details materially change behavior, present explicit alternatives or request clarification.

Save one Markdown plan in the target workspace using its planning convention, or `mercury-code-research-plan.md`. Preserve unrelated existing files. Scale detail to the task and include:

1. Outcome, selected components, scope, constraints, and acceptance criteria.
2. Consulted source paths, versions when known, and coverage limitations.
3. A mapping from paper components to planned files or symbols and validation checks. Cite PDF pages and relevant sections, equations, algorithms, or tables. For Markdown cite headings and unambiguous passages; mark embedded paper locators as reported by the analysis unless directly verified.
4. Implementation steps in dependency order, grounded in the actual repository, including interfaces and dependencies.
5. Proposed defaults, adaptations, missing details, and decisions requiring resolution.
6. Feasible verification through mathematical invariants, small reference cases, and integration checks as appropriate. Distinguish local correctness from reproducing benchmark results; identify required datasets, settings, and compute where relevant.

Do not duplicate entire analyses or prewrite the patch as prose. Preserve enough evidence and decisions for implementation to resume from this plan.

## Resolve material decisions before coding

Save the grounded implementation plan before editing implementation code.

Proceed without an additional approval request when the user's instructions or prior approval already settle the methodology, scope, and consequential choices. A request to implement authorizes routine implementation decisions within that scope; it does not resolve missing scientific details that materially change behavior.

When unresolved alternatives would materially affect scientific fidelity, requested behavior, public interfaces, scope, or resource requirements, present the saved plan, explain the specific decision needed, and ask the user before implementing the affected part. Continue independent work that does not depend on that answer. Silence is not approval.

If the user explicitly requests approval before coding, present the plan and wait. For planning-only requests, deliver the plan and stop.

Reuse prior decisions and approvals. Reopen a decision only when new evidence invalidates it or the implementation would exceed the authorized scope.

## Implement using Mercury Agents

Locate `mercury-agents` in the available skills or local collection, commonly a sibling folder. Check availability during planning; read and follow it for execution once material decisions are resolved. If it is unavailable, implement in the current agent with an inspect → implement → verify sequence driven by the saved plan, and state in the final report that `mercury-agents` was not used. Never claim it was invoked when it was not.

Supply the grounded plan and resolved decisions as its existing working brief, together with user constraints, relevant source pointers or formulas, adaptations, target files, and expected checks. Preserve the decision and approval requirements above even when `mercury-agents` would otherwise take an inspect-and-implement shortcut. Reuse the plan rather than generating a duplicate. Follow its execution and verification guidance; using it does not require separate agents when delegation is unavailable or inappropriate.

Keep scientific components traceable through focused code comments or the plan mapping. Preserve paper constraints during implementation and any authorized handoff. Label necessary engineering choices rather than presenting them as paper-derived facts.

## Verify and deliver

Verify behavior against the authorized request and selected methodological mechanisms. Run relevant repository checks and planned methodological checks. Passing a build or synthetic test does not establish reproduction of reported results. Report actual outcomes, unperformed checks, and limitations without inventing metrics.

Update the same plan with implemented file pointers, material deviations, and verification outcomes where needed. Respond in the user's language with links to the plan and principal code, concise run instructions, and unresolved scientific or execution limits.
