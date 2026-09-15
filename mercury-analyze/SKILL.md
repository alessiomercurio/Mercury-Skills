---
name: mercury-analyze
description: "Produce a detailed, source-grounded explanation of a scientific paper and save it as Markdown. Use for faithful explanation of context, methods, experiments, and findings; this skill alone does not cover independent critical appraisal or recommendations."
---

# Mercury Analyze

Produce a detailed, accessible explanation of the paper grounded entirely in the paper and relevant works it cites. Explain the authors' reasoning and findings without adding personal conclusions, critiques, recommendations, or proposed experiments.

For requests combining source-grounded explanation or comparison with independent critique or recommendations, apply this skill to the source-grounded portion. Keep any separately requested evaluation clearly distinguished, with its own reasoning and evidence. Do not silently omit that part of the user's request or present independent judgments as findings reported by the papers. The restrictions on independent judgments below apply to the source-grounded portion; place any explicitly requested evaluation in a separate, clearly labeled section after it.

## Language and evidence

- Support papers and requests in any language. Write the analysis in the user's requested language; otherwise use the language of their request. Keep the paper's original title and preserve technical names, symbols, and dataset names where translation would reduce precision.
- Use plain language and connected explanations. Define necessary technical terms on first use; explain equations through their variables, purpose, and role in the method. Avoid ornate prose and unnecessary jargon without sacrificing detail.
- Attach a precise source locator to every substantive claim: section and page, equation, figure, table, or appendix as appropriate. A citation may support a paragraph only when it supports all claims in that paragraph. Preserve the paper's reference numbering and distinguish it from your own citations.
- Separate what the authors state, what the experiments report, and explanations taken from cited works. Do not present a plausible rationale as the authors' rationale. If a motivation, detail, or explanation of a result is absent, explicitly say it is not reported.
- Keep claims within the evaluated conditions. Do not turn numerical differences into statistical significance, associations into causes, or benchmark findings into general guarantees unless the sources establish them.

## Read the sources

1. Identify the exact paper and version from the supplied file, URL, DOI, or title. Obtain and read the full text, including relevant appendices, tables, figures, and available supplements. If the paper is ambiguous, ask for identification. If only part is accessible, clearly state the coverage and request the missing material needed for a complete analysis; never fabricate the missing sections.
2. Inspect figures, table headers, captions, and equations directly when extracted text is insufficient. Preserve units, uncertainty, metric direction, and experimental conditions.
3. Follow the paper's citations where needed to explain a methodological component, its origin, or an explicitly stated choice. Read the relevant original sources before using their details, and cite their exact locators and accessible links. Keep this targeted to understanding the focal paper, rather than expanding into an independent literature review.
4. If a cited source is unavailable, identify that limitation. Attribute any usable description to the focal paper and do not imply that the original source was read. A cited work can explain a borrowed mechanism; it does not establish why the focal authors selected it unless they say so.

## Shared paper metadata

Include a compact metadata block at the beginning of the analysis:

- Paper ID: DOI or arXiv identifier when available; otherwise title, first author, and year.
- Version: the version or date explicitly identified in the source; otherwise “not identified.”
- Source: the local path or URL actually consulted.
- Coverage: sections, appendices, and supplements actually read, including access limitations.
- Missing details: unreported or inaccessible information relevant to understanding or implementing the method.

Do not infer missing metadata. Keep the same Paper ID across downstream reports and distinguish versions explicitly.

## Required analysis

Use the following four sections in order, translating their headings into the output language. Adapt subsections to the paper rather than forcing experimental terminology onto theoretical or non-empirical work. Mark unreported or inapplicable elements explicitly.

### 1. Abstract, introduction, related work, and objective

Combine these parts into a coherent summary: the research problem, context, relevant prior approaches, the gap identified by the authors, the paper's objective, and its stated contributions. Explain how the cited prior work positions the proposed contribution. Distinguish claimed novelty from findings demonstrated later in the paper.

### 2. Methodology and reasons for the choices

Explain the method in detail and in its operational order: inputs, assumptions, components, processing or training steps, objectives, and outputs. For each important component, explain what it does, which problem it addresses, how it connects to the other components, and the authors' stated reason for using it. Include relevant mathematical definitions and implementation details when they materially explain the method.

Use the cited works to clarify inherited techniques and distinguish those techniques from the paper's additions or changes. Tie reasons and tradeoffs to explicit evidence; if the authors describe a choice without justifying it, say so. Explain theoretical arguments and their assumptions where they replace or support experiments.

### 3. Experiments, datasets, and results

Explain each main experiment's question, setup, comparisons, metrics, and findings. Cover baselines, ablations, sensitivity analyses, and qualitative examples when present.

- List every dataset used in the reported work, including auxiliary, pretraining, validation, and evaluation datasets where identified. Explain each dataset's role, task, relevant properties, preprocessing, and splits or sample counts when reported. Distinguish datasets actually used from datasets merely mentioned in related work. A compact table is appropriate.
- Explain the evaluation protocol and the meaning and direction of each important metric. Preserve reported values, units, uncertainty, and conditions; do not invent missing settings.
- Analyze what worked, what did not, and under which conditions, including mixed, negative, or inconclusive results. Connect each finding to the methodological component it evaluates and cite the corresponding table, figure, or passage.
- Distinguish direct experimental evidence, such as a reported ablation, from the authors' interpretation. Explain why something worked or failed only when the paper provides that explanation. If no failures are reported, state that rather than inventing them or asserting universal success.

### 4. Conclusions

Summarize what the authors did and the results they obtained, preserving the scope and qualifications in the paper. Include limitations or future work only as explicitly attributed statements by the authors. End with this source-grounded summary; add no independent verdict, proposals, or recommendations.

## Markdown deliverable and verification

When writing equations in Markdown deliverables or responses, use `$equation$` for inline math and `$$equation$$` for display math. For multiline display equations, put the opening and closing `$$` on separate lines. Do not use `\(...\)` or `\[...\]` as math delimiters, escape the dollar delimiters, or wrap rendered equations in code spans or code fences.

Create a UTF-8 file named `<Paper Title>.md` in the user-specified output directory, or the current workspace when none is specified. Use the original title as the filename, replacing only filesystem-invalid characters when necessary; retain the exact title as the first-level heading. Avoid overwriting an unrelated existing file by adding a distinguishing suffix.

Include the shared paper metadata block, the analysis language and any access limitations, all four analysis sections, and a source list for the focal paper and any cited works actually consulted. The file must contain the complete analysis, not a shorter summary or a link back to the conversation.

Before delivering, check that all substantive claims have supporting locators, numeric results match their sources, dataset roles are clear, methodological explanations distinguish reported motivations from missing ones, and no personal conclusions or proposals were introduced into the source-grounded analysis. If an independent evaluation was requested, verify that it is clearly separated and supported by its own reasoning and evidence. Verify that the Markdown file exists and contains the complete analysis. Return a clickable link to it with a brief completion message in the user's language.
