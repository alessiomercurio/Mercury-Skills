![Mercury Skills banner](mercury%20skills.png)

# Mercury Skills

A collection of Codex skills for understanding scientific papers, comparing research, maintaining a research wiki, and turning methods into working code.

Mercury connects research and implementation through source references, explicit assumptions, and focused verification. Each skill can be invoked separately; use them together when your task spans the full workflow.

## Included skills

| Skill | Purpose | Output |
| --- | --- | --- |
| [mercury-analyze](mercury-analyze/SKILL.md) | Explain a paper's context, methodology, experiments, and conclusions with precise source references. | A detailed Markdown analysis. |
| [mercury-compare](mercury-compare/SKILL.md) | Compare a local collection of papers using PDFs or existing Markdown analyses, preserving experimental conditions. | A Markdown comparison report with a comparison matrix. |
| [mercury-research-wiki](mercury-research-wiki/SKILL.md) | Build and maintain a source-grounded Markdown wiki of papers, concepts, syntheses, and papers' reference implementations. | Linked wiki pages with provenance, an index, and an operation log. |
| [mercury-code-research](mercury-code-research/SKILL.md) | Translate selected research methods into a grounded implementation plan and local code changes. | A saved plan, implementation, and verification results. |
| [mercury-agents](mercury-agents/SKILL.md) | Plan, refine, implement, and verify code changes while reducing redundant exploration and handoffs. | Code changes with a concise verification summary. |

`mercury-code-research` requires `mercury-agents`. Analysis, comparison, and the research wiki can be used independently or as inputs to implementation.

## Installation

Replace `alessiomercurio/Mercury-Skills` below with this repository's GitHub owner and name.

### With npx

With Node.js and npm installed, use the [Vercel Labs skills CLI](https://github.com/vercel-labs/skills) to install all five skills for Codex across your projects:

```bash
npx skills add alessiomercurio/Mercury-Skills --agent codex --skill '*' --global
```

Omit `--global` to install into the current project.

To choose which skills to install interactively:

```bash
npx skills add alessiomercurio/Mercury-Skills --agent codex --global
```

To install only the research implementation workflow and its required dependency:

```bash
npx skills add alessiomercurio/Mercury-Skills --agent codex --skill mercury-code-research mercury-agents --global
```

To list available skills without installing:

```bash
npx skills add alessiomercurio/Mercury-Skills --list
```

`npx` runs the third-party `skills` installer published by Vercel Labs, which downloads the skill folders directly from GitHub. Once this repository is published and accessible, these commands can use it immediately: no separate Mercury npm package or repository registration is required. Private repositories require Git authentication.

### Manual installation

Download or clone this repository and copy the five `mercury-*` folders into:

- `~/.agents/skills/` for personal use across projects.
- `.agents/skills/` inside a repository for project-specific use.

Each installed skill folder must contain its `SKILL.md` and `agents/openai.yaml`. Codex detects skill changes automatically; restart it if a skill does not appear.

See the [official skill documentation](https://learn.chatgpt.com/docs/build-skills) for discovery locations and installation guidance.

## Usage

Invoke a skill by name in Codex and provide the relevant files, locations, and desired outcome. Responses follow your requested language, or the language of your request.

### Understand a paper

```text
$mercury-analyze Explain papers/example.pdf in Italian and save the analysis as Markdown.
```

### Compare papers

```text
$mercury-compare Compare the papers in ./papers, focusing on their methods,
evaluation protocols, results, and reported limitations.
```

### Maintain a research wiki

```text
$mercury-research-wiki Initialize an empty research wiki here, then ingest
./papers/example.pdf and map its verified reference implementation.
```

### Implement a research method

```text
$mercury-code-research Implement the retrieval method from ./papers/example.pdf
in this repository. Use the existing Python interfaces and verify it on a small reference case.
```

### Work on a codebase

```text
$mercury-agents Fix the pagination bug in this repository and run the relevant checks.
```

## Workflow and requirements

Start with `mercury-analyze` for a detailed explanation of one paper, `mercury-compare` for a synthesis across papers, or `mercury-research-wiki` to accumulate sourced findings and map papers to their reference code. Go directly to `mercury-code-research` when the implementation scope is already clear.

- Supply readable source files or accessible links for analysis, and local PDFs or Markdown for comparison and research implementation.
- PDF extraction, browsing, code execution, and delegation depend on the tools and permissions available in your Codex environment. These skills provide instructions; they do not install those capabilities.
- `mercury-research-wiki` can start empty, ingest papers over time, and answer from its linked pages. It maps papers' reference implementations, not the user's application code.
- `mercury-agents` prefers `gpt-6-astra` at low effort for the initial plan, `gpt-6-sol` at medium effort for plan refinement, and `gpt-6-luna` at xhigh effort for implementation and verification. It supports single-agent execution; separate agents and model selection are used only when available and permitted.
- Analysis and comparison distinguish reported findings from independent evaluation. Ask explicitly if you also want critique or recommendations.
- Implementation distinguishes source-reported details from engineering choices. Local checks do not establish reproduction of published benchmark results.
- Reducing redundant context is a workflow objective; no measured token savings or benchmark improvements are claimed.

