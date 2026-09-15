![Mercury Skills banner](mercury%20skills.png)

# Mercury Skills

A collection of Codex skills for understanding scientific papers, comparing research, and turning methods into working code.

Mercury connects research and implementation through source references, explicit assumptions, and focused verification. Each skill can be invoked separately; use them together when your task spans the full workflow.

## Included skills

| Skill | Purpose | Output |
| --- | --- | --- |
| [mercury-analyze](mercury-analyze/SKILL.md) | Explain a paper's context, methodology, experiments, and conclusions with precise source references. | A detailed Markdown analysis. |
| [mercury-compare](mercury-compare/SKILL.md) | Compare a local collection of papers using PDFs or existing Markdown analyses, preserving experimental conditions. | A Markdown comparison report with a comparison matrix. |
| [mercury-code-research](mercury-code-research/SKILL.md) | Translate selected research methods into a grounded implementation plan and local code changes. | A saved plan, implementation, and verification results. |
| [mercury-agents](mercury-agents/SKILL.md) | Plan, implement, and verify code changes while reducing redundant exploration and handoffs. | Code changes with a concise verification summary. |

`mercury-code-research` requires `mercury-agents`. The analysis and comparison skills are optional inputs to implementation.

## Installation

Replace `alessiomercurio/Mercury-Skills` below with this repository's GitHub owner and name.

### With npx

With Node.js and npm installed, use the [Vercel Labs skills CLI](https://github.com/vercel-labs/skills) to install all four skills for Codex across your projects:

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

Download or clone this repository and copy the four `mercury-*` folders into:

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

Start with `mercury-analyze` for a detailed explanation of one paper, `mercury-compare` for a synthesis across papers, or go directly to `mercury-code-research` when the implementation scope is already clear.

- Supply readable source files or accessible links for analysis, and local PDFs or Markdown for comparison and research implementation.
- PDF extraction, browsing, code execution, and delegation depend on the tools and permissions available in your Codex environment. These skills provide instructions; they do not install those capabilities.
- `mercury-agents` supports single-agent execution. Separate agents and model selection are used only when available and permitted.
- Analysis and comparison distinguish reported findings from independent evaluation. Ask explicitly if you also want critique or recommendations.
- Implementation distinguishes source-reported details from engineering choices. Local checks do not establish reproduction of published benchmark results.
- Reducing redundant context is a workflow objective; no measured token savings or benchmark improvements are claimed.


