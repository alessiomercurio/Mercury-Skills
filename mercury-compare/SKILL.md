---
name: mercury-compare
description: "Compare scientific papers in a local collection using their Markdown analyses or PDFs. Use for source-grounded comparison of objectives, methods, and reported results; this skill alone does not cover independent critical appraisal, recommendations, or external literature research."
---

# Mercury Compare

Produce a source-grounded comparative synthesis of papers in one local collection. This workflow can follow `mercury-analyze`, but does not require that skill or pre-existing analyses. Use only local files actually read. Do not browse, retrieve external cited works, add knowledge from memory, or propose research directions, experiments, improvements, or recommendations.

For requests combining source-grounded explanation or comparison with independent critique or recommendations, apply this skill to the source-grounded portion. Keep any separately requested evaluation clearly distinguished, with its own reasoning and evidence. Do not silently omit that part of the user's request or present independent judgments as findings reported by the papers. The restrictions on independent judgments below apply to the source-grounded portion; place any explicitly requested evaluation in a separate, clearly labeled section after it.

## Select and read the local corpus

Use the folder identified by the user or the current workspace when it clearly contains the collection. Ask for the folder only if the intended corpus cannot be determined. Respect any requested topic or subset; otherwise include all identifiable papers in that folder. Include nested folders only when they belong to the same collection.

Inventory candidate Markdown analyses and paper PDFs. Match them by title, authors, year, version, and source metadata rather than filename alone. Treat a paper and its analysis as one work; retain distinct versions when their differences matter. Exclude unrelated Markdown, instructions, and previous comparative outputs from the evidence corpus.

Reuse the shared paper metadata from existing analyses when available. Check it against the sources actually consulted and preserve paper identifiers and version distinctions in the report or plan.

Older analyses without this block remain usable: reconstruct only the metadata needed for the task from available evidence, without requiring the analysis to be rewritten.

Choose sources per paper, including in mixed collections:

- Prefer its existing Markdown analysis, reading the relevant sections in context. An analysis from another workflow is acceptable if its paper and evidence can be identified.
- Read the local PDF when no corresponding analysis exists, or when the Markdown omits, ambiguously describes, or contradicts information needed for the comparison. Inspect tables, figures, captions, and equations directly when extraction loses meaning. If PDF content and its analysis disagree, use the PDF for the disputed point and document the discrepancy.
- If the PDF is unavailable or unreadable, retain only what the Markdown actually supports and identify the verification limit. Do not silently fill omissions. If only a portion of a source is readable, describe coverage precisely.

When local PDFs are available, directly verify the numerical results and evaluation conditions that support the report's principal comparisons, even when the Markdown appears complete. This is a targeted check, not a requirement to reread every paper in full.

If direct verification is unavailable, identify the affected comparisons as supported only by the consulted analyses and preserve that limitation in the synthesis.

Use local text search to find candidate passages, then read their surrounding explanations and conditions; isolated matches are not sufficient evidence. Papers merely cited inside a local source are not additional consulted papers. Attribute secondhand descriptions to the source actually read.

If fewer than two distinct papers are usable, state that a cross-paper comparison cannot be completed and identify the missing input without inventing a comparison.

## Evidence rules

Preserve each paper's shared Paper ID. A short report alias such as P1 may be used if explicitly mapped to that ID and version. Link each identifier to the actual local file or files used. Support every substantive comparison, explanation, number, and assessment with a precise locator adjacent to the statement:

- For PDFs: paper identifier, PDF page, and section, table, figure, equation, or appendix when relevant. Distinguish printed page numbers from PDF page indices when they differ.
- For Markdown: paper identifier, filename, heading and line range or other unambiguous passage locator. Preserve embedded paper locators as references reported by the analysis; do not imply direct PDF verification unless it occurred.
- For a comparison between papers, cite the supporting passages from each paper. A citation covering a paragraph or table cell must support every claim in it.

Distinguish authors' stated intentions and interpretations from observed results and descriptive cross-paper comparisons. Explain why methods differ, why choices were made, or why results occurred only when the consulted sources provide those reasons. Otherwise state “not reported in the consulted sources.” Do not infer authors' intentions or causal explanations from architecture or numerical outcomes.

Missing information is not a failure. A strength must be a documented result or an explicitly attributed author claim, preserving that distinction. Do not treat an authors' claimed contribution as demonstrated superiority. Keep conclusions within reported assumptions, tasks, datasets, and evaluation conditions.

## Comparative deliverable

When writing equations in Markdown deliverables or responses, use `$equation$` for inline math and `$$equation$$` for display math. For multiline display equations, put the opening and closing `$$` on separate lines. Do not use `\(...\)` or `\[...\]` as math delimiters, escape the dollar delimiters, or wrap rendered equations in code spans or code fences.

Write in the user's requested language, otherwise the language of their request. Preserve original paper titles, technical identifiers, and metric names. Choose a concise, descriptive report title in the output language that reflects the actual comparison or research scope, such as “Confronto dei metodi di retrieval per RAG”. Use it as the first-level heading and save the complete Markdown report as `<Report Title>.md` in the corpus folder. Honor any user-specified title, filename, or destination. Replace filesystem-invalid characters in the filename while preserving the full title in the heading. Preserve existing files by using a distinguishing suffix when necessary.

Organize the report around the comparison rather than a series of disconnected paper summaries:

1. **Corpus and coverage.** List paper identifiers, titles and available identifying metadata, source links, whether Markdown, PDF, or both were read, and access or completeness limitations. Explain any topic-based exclusions.
2. **Comparison matrix.** Provide a concise cited overview of objectives, methods, intended outcomes, evaluated conditions, principal results, documented failures or limitations, and demonstrated strengths. Mark unavailable or inapplicable information explicitly.
3. **Objectives and methodological differences.** Explain the problems each work addresses, what it seeks to obtain, shared mechanisms and substantive differences in assumptions, components, data, training or reasoning, and outputs. Connect choices to their documented motivations; make absent explanations explicit. Adapt these dimensions to theoretical or non-empirical work.
4. **Results and comparability.** Compare reported findings with their metrics, units, direction, uncertainty, baselines, datasets, splits, and protocols when supplied. Preserve experimental conditions. If protocols or tasks differ, explain the documented differences and present outcomes separately; do not derive a ranking or superiority claim from non-comparable scores. Distinguish observed numerical differences from established statistical significance.
5. **Failures, limitations, and strengths.** Compare negative, mixed, or inconclusive findings, reported failure cases, limitations, ablations, and positive evidence. Distinguish explicit limitations from observed failures and missing evaluations. If failures are not reported, say so without claiming there were none. Explain causes only where sources establish or explicitly interpret them, attributing interpretations.
6. **Evidence-grounded synthesis.** Summarize convergences, divergences, and outcomes supported by the cited sources. Include no personal verdict, proposed next steps, recommendations, or speculative claims, including proposals borrowed from authors' future-work sections.

Scale the matrix and discussion to the corpus without dropping papers silently. All substantive prose must remain anchored to the consulted files, including the final synthesis.

## Verify before delivery

Check that every included paper is represented, each claim has a supporting locator, all compared values preserve their conditions, and claims based only on Markdown are identified accurately. Remove unsupported explanations, generalizations, rankings, and proposals from the source-grounded comparison. If an independent evaluation was requested, verify that it is clearly separated and supported by its own reasoning and evidence. Confirm that the complete report was saved in the intended folder. Return a clickable link with a brief completion message and any material coverage limitation.
