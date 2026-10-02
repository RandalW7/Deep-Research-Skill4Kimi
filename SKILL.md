---
name: deep-research-extended
description:
    Utilizes a suite of tools to facilitate exhaustive, evidence-based deep research and long-form report engineering. Supports multi-dimensional research with iterative search, recursive reflection, quantitative visualization, and structured outputs in multiple formats (Markdown, docx, pdf, xlsx, pptx, webapp). Adds a per-round non-paper source pass (technical blogs, lab sites, forums) alongside the standard scholarly/web search, a dedicated adversarial counterevidence round attacking the report's central premise, formal derivations with proven/assumed/conjectured labeling, pre-mortems written as executable decision rules, and an operational-realism audit for proposed methods.
---

# Deep Research

Conduct thorough, multi-dimensional research on complex questions using file creation and editing, search engines and browsers, code execution, image and multimedia generation, slide creation, website deployment, and visual processing of tool outputs. Think critically, use the current date as the temporal reference, verify uncertain information proactively, and deliver comprehensive, well-structured, rigorously grounded findings.

## Research & Discovery Phase (The 10+ Step Loop)

1.  **Read Attached Files**: Start by checking any attachments to understand the background information.
2.  **Clarify Intent**: Ask targeted clarification questions **via the `ask_user` tool** to ensure you fully understand their goals before proceeding.
3.  **Iterative Search**: Perform **at least 10 search steps** to ensure comprehensive coverage across multiple dimensions. Avoid keyword redundancy; ensure each round brings substantial new information.
    - **Two-track rounds**: Organize the search into topic rounds. Every topic round has two halves — (a) the standard scholarly/web track (arXiv, Scholar, general web) and (b) a **non-paper source pass over the same topic** (see *Non-Paper Source Pass* below). Never defer all non-paper searching to a single end-of-run pass: blogs and lab posts found early reshape the research plan for later rounds.
    - **Adversarial round**: Once the working thesis is formed enough to be attackable (typically after ~half the rounds), run at least one dedicated **Adversarial Evidence Round** (see below) whose explicit goal is to overturn it — plus a second, shorter adversarial pass over the final draft's central claims before delivery.
4.  **Credibility & Verification**: Prioritize authoritative sources (government sites, academic databases, peer-reviewed journals). **Never fabricate data.** Every statistic and claim must be accurate and traceable.
    - **First-party technical sources are primary sources**: A large share of valuable research — especially in AI/ML — is published only on technical blogs, lab sites, and forums, never as papers. Do not discount a source for low domain authority, and do not require a paper version to exist; evaluate content and authorship, not search ranking. When a result exists both as a first-party post and an arXiv/aggregator mirror, cite the original post's URL.
5.  **Recursive Reflection**: After EACH search round, output a **Thinking Process** and a **Summary**.
    - **Thinking**: Reflect on content found, identify unmet needs, and plan the next specific step. Always answer: **which premise of my current outline did this round threaten or support?** If a round threatened nothing, it was confirmatory — sharpen the attack or the gap-hunting angle in the next round.
    - **Summary**: Concise recap of key findings.
    - *Constraint*: Both sections must be **short and concise**.
6. **Quantitative Analysis**: Use **Python** for calculations, data cleaning, statistical analysis, and verification when precision is required. 
7. **Visualization Planning**: Based on the report content, create necessary, content-relevant visualizations and follow the **Visualization Workflow** for chart/diagram authoring, rendering, embedding, and visual consistency.

## Non-Paper Source Pass

Much valuable research appears only on technical blogs, lab sites, and forums, never as papers; search ranking will not surface these low-authority sites — name and fetch them explicitly. This pass **supplements** the standard pipeline; never narrow, reorder, or replace it.

**In every topic round**, after that round's standard track:

- **Fetch index pages / RSS feeds directly** (e.g., Python `requests` with a browser User-Agent). `site:` queries silently fail for these domains in this environment; 403/429/timeout = anti-bot, not absence of content — retry via browser tools.
- **Skim before judging**: relevance decisions for papers are made at the abstract level; for blog posts, titles alone are insufficient — a post's connection to the topic is often architectural or methodological rather than lexical (e.g., a post whose title names an unrelated application may still describe exactly the architecture, evaluation protocol, or training technique your topic needs). Open and skim every plausibly relevant post's body before deciding to skip it; never reject a post on its title alone.
- **Chase reverse citations**: from the reference lists of relevant papers, extract links to independent (non-arXiv, non-journal) domains and fetch them.
- **Recency patch**: for current-year material, check site homepages / latest-posts indexes directly; search indexing lags by days to weeks.

**Core list** (check every round, fetching directly):

- Lab research: anthropic.com/research (+ /engineering; also hosts the transformer-circuits.pub interpretability series), openai.com/research, deepmind.google/discover/blog, machinelearning.apple.com, bair.berkeley.edu/blog, huggingface.co/blog
- Evals & data: epoch.ai, metr.org, apolloresearch.ai
- Forums & review: lesswrong.com, alignmentforum.org, openreview.net
- Practice & analysis: simonwillison.net, semianalysis.com

**Extend per topic** as needed: independent researcher blogs (e.g., gwern.net, lilianweng.github.io, karpathy.github.io), lab GitHub orgs and release notes (e.g., deepseek-ai, MoonshotAI, QwenLM), and research newsletters (e.g., Interconnects, Import AI).

## Adversarial Evidence Round (Premise Attack)

A limitations section written after the fact cannot rescue a wrong central premise. Dedicate at least one full search round to **overturning the report's working hypothesis**, not supporting it:

- **Attack the premise, not the details**: state the report's single most load-bearing claim in one sentence, then search directly for evidence against it — null results, failed replications, recovery/improvement results under stronger baselines, "X is under-elicited" or "X is a measurement artifact" posts, and stronger incumbent methods that would make the proposed contribution unnecessary.
- **Search the counterclaim itself**: query the opposing position directly rather than searching for weaker versions of your own claim, and include non-paper sources — null, negative, and recovery results disproportionately live in lab posts, competition retrospectives, and researcher blogs rather than in papers.
- **Harvest consequences, not disclaimers**: every piece of counterevidence must end in an operational consequence — a baseline the report must now match, a control the proposal must add, or a claim that must be narrowed. Feed these into the Pre-Mortem decision table (below), not into prose caveats.
- **Survive or revise**: if the central claim survives the round, say which specific attacks it survived; if not, revise the thesis before writing, never around it.

## Report Engineering Standards

### 1. Structural Logic & Opening

- **Conditional TL;DR**: Provide a **short direct answer** at the beginning **only if** the user's question can be answered in a few sentences. 
- **Style Adaptation**:
    - If a specific style is implied (e.g., story, interview, case narrative), adhere to it.
    - **Default**: Strict academic report format.
    - Omit generic Introduction/Background sections unless explicitly required.

### 2. Depth and Analysis (Mode-Based)

- **Academic/Survey Mode**:
    - Prioritize comprehensive fact-based detail. Include full definitions, formulas, statistical indicators (CI, metrics), and baseline comparisons.
    - Avoid speculative interpretation; ensure all statements are supported by references. Where the report does interpret or extrapolate, mark it at the sentence level (see Claim-Level Epistemic Labels below) rather than omitting it.
    - Apply the **Formalization Pass**, **Pre-Mortem Decision Rules**, and **Operational Realism Pass** below — they are the difference between a survey that summarizes and a report that advances the question.
- **Lifestyle/Practical Mode**:
    - Incorporate observations, human insights, Pros/Cons, and actionable trade-offs.
    - Reflect on implications and explain why certain patterns matter.

### 2.1 Formalization Pass (Mathematical Essence)

For technical and research reports: identify the **2–4 claims where informal prose hides a checkable structure**, and derive them explicitly with intermediate steps shown. Three recurring patterns:

- **Confound algebra**: for every headline empirical pattern the report relies on, derive the null model that would produce the *same* pattern without the proposed mechanism (chain-rule decompositions, base-rate arithmetic, aggregation and selection effects), and state which measurement would distinguish mechanism from artifact.
- **Identifiability limits**: for any metric, probe, or training objective the report leans on, state what it *cannot in principle* establish — ideally as a short proof or counterexample construction (a symmetry or relabeling argument showing an objective cannot certify the intended semantics; an information argument bounding what one signal can add over a cheaper one).
- **Exact proposal definitions**: when the report proposes a method, define it as a formula — variables, objective, constraints — and derive its immediate properties (dimension checks, identity limits, degenerate cases, feasibility conditions), so the proposal is falsifiable as written rather than plausible as prose.

Label every step **[proven]** (derived under stated assumptions), **[assumed]**, **[approximate]**, or **[conjectured]**. Cut any derivation that changes no downstream conclusion, measurement plan, or design choice; narrow any claim that resists all three patterns and survives only as rhetoric.

### 2.2 Pre-Mortem as Decision Rules

Before finalizing, assume the report's central explanation and proposed method are **wrong**, and write the pre-mortem as an executable table — not a disclaimer list. For each load-bearing premise, predeclare:

| If this is observed | The warranted conclusion is | The next decision is |

Cover at minimum: a matched-baseline result that erases the gap (stronger baselines at equal compute and information budget); a proxy-metric success that fails independent verification; a **measurement–causality split** (a signal predicts the outcome but acting on it fails, or vice versa); and an **evaluation-artifact explanation** (checker or judge false positives, evaluator-pleasing shortcuts, self-graded judgments). Each row names its triggering observation *in advance*. A conclusion the report is unwilling to place in this table is a conclusion the report has not actually tested.

### 2.3 Operational Realism Pass

For reports proposing experiments, methods, or systems: audit the proposal as the engineer who must implement it. Check ambiguous indices, units, and conventions (numbering schemes, normalization, dimension matching); state semantics (what an action at one step can and cannot retroactively change); label provenance (who produced the ground truth, and whether the same instrument is being optimized); label timing (a label derived from a completed outcome can corrupt intermediate supervision); power arithmetic for proposed sample sizes (e.g., worst-case CI half-width at the planned *N*); and a stated cost budget. Resolve each finding as an explicit implementation condition in the report body, not a footnote.

### 3. Length and Paragraph Constraints

- **Total Volume**: As a default target, the report should generally reach long-form report scale.
- **Paragraph Rules**:
    - Each paragraph must be **at least 100 words** (max 1,000 words). Each paragraph should be substantial and well developed, without becoming mechanically overextended.
    - **Subsection Rule**: Every subsection (e.g., `## 3.1`) MUST contain **more than one paragraph**.
- **Natural Transitions**: In English writing, avoid rigid patterns like "First, second, third" or "Firstly, secondly, lastly."
- **Expansion Rule**: If the draft is still underdeveloped, expand the logically relevant existing sections rather than adding disconnected filler.

### 4. Mandatory Table Architecture

- **Usage**: Use tables as the primary structural tool to replace or shorten long prose for comparisons, workflows, or results.
- **Centralized Comparison**: Aggregate recurring entities, models, or metrics from across different sections into single, coherent comparison tables.
- **Source Integration**: **Do not include a separate "Source" column**. Place inline source links (e.g., `([Source Name](URL))`) directly within the data cells.

### 5. Revision and Completion

- **Completion Standard**: The report must ultimately be complete, well-structured, and fully compliant with all content, formatting, and length requirements.
- **Final Verification**: Before finalizing, verify that the report fully satisfies all structure, depth, table, citation, and length requirements, especially that it has developed into a sufficiently substantial long-form report rather than a brief or compressed write-up. Additionally confirm: the Adversarial Evidence Round was actually run and its consequences incorporated; the Pre-Mortem decision table is present with named triggering observations; each derivation carries proven/assumed/approximate/conjectured labels; and the Operational Realism Pass was applied to every proposed method or experiment. For non-Markdown exports, open the final file and confirm that mathematical notation and tables actually rendered (no missing variables, no broken table markup).
- **Rigor must not cost readability**: hedges and epistemic labels belong in subordinate clauses and inline tags, never stacked ahead of the conclusion they qualify. Keep the Executive Summary, bold topic sentences, quantitative anchors, and figures intact; a correct report the reader cannot navigate is a failed deliverable. When adding rigor sections, state the conclusion first and the qualification second.
- **Targeted Revision**: If the report remains insufficient in scope or depth, strengthen it by elaborating underdeveloped sections, adding missing evidence or comparisons, or introducing additional analytical dimensions where appropriate.
- **Integrated Improvement**: Any necessary revision must be incorporated into the logically relevant existing section, rather than appended as a disconnected add-on or catch-all section.
- **Substance over Filler**: Prioritize substantive depth, specificity, and analytical value over repetition, redundancy, or filler.

### 6. Formatting & Citation Rules

- **Citation Format**: Every fact, statistic, or claim in formal writing must carry an inline citation in the format `([Source Name](URL))`, placed immediately after the statement and **before punctuation**. Max **two citations per sentence**.
    - *Example*: The global AI data market reached $84.5 billion in 2025 ([IIM](https://www.iim.net.cn/75/view-300067-1.html)).
    - *Note*: The source short-name must be a real site, institution, or report name, kept short (1–3 words, e.g., `[Statista]`, `[WHO]`).
    - *Note*: The URL must be the real, accessible original source address — for research first published on a blog or lab site, link the original post, not an arXiv or aggregator mirror.
    - *Note*: If citing multiple sources together, place the links inside one pair of parentheses, separated by a comma: `([Source A](URL_A), [Source B](URL_B))`.
    - *Note*: Do not use citations for creative/non-formal writing.
- **Claim-Level Epistemic Labels**: Mark every claim that is not a direct restatement of one cited source: `[synthesis]` (composed across sources), `[speculative]` (extrapolation beyond cited evidence), `[thin literature]` (few or weak sources), and for derivations `[proven]` / `[assumed]` / `[approximate]` / `[conjectured]`. Place the tag on the sentence carrying the claim — never rely on a single global disclaimer.
- **No End References Section**:
    - Do **not** include any end-of-report **"References"**, **"Reference"**, **"Sources"**, or similar bibliography/list of sources.
- **Bolding Strategy**: 
    - Bold **important keywords, critical numbers, major conclusions, and key insights**.
    - **Avoid redundant bolding**: Do not repeatedly bold the same entity within a short span.
- **High-Stakes Disclaimer**: For medical, legal, financial, or other high-stakes topics, end the response with a clear statement that the content is for general informational purposes only and does not constitute professional advice.
- **Visuals**: Incorporate diagrams, charts, or photographs generated or found during research to support arguments.

### 7. Visualization Workflow

- **Generation**: Cover both **data-driven charts** (built from verified, cited data — **never fabricate values**) and **conceptual diagrams** (framework, flow, architecture, or relationship schematics that make the report's structure and logic easier to follow). Build with **ECharts by default**, using **Python** (e.g., via IPython) when ECharts cannot faithfully express the intended visual.
- **Rendering & Embedding**: For an HTML presentation, charts may stay as native ECharts/HTML. For a `.md` or any other static-format report, ECharts and Python charts alike MUST be exported to static images and embedded with `![caption](path)`; never paste raw option objects, `<script>` blocks, or interactive HTML into the report body. **Note**: Static output format is **not** a reason to switch from ECharts to Python/matplotlib. When ECharts can faithfully express the intended visual, even for static reports, author the chart in ECharts first because it generally produces more polished, presentation-ready visuals; then render it to a static `.png`, `.jpg`, or supported `.svg` image and embed it in the report.
- **Quality Bar** (dimensions carry equal weight): **Correctness** — the visual matches its source: data charts reflect the underlying numbers, and diagrams stay faithful to the described structure, prose, and tables. **Chart-type fit** — reach for the type that fits the relationship, using ECharts' full repertoire rather than only bar/line/pie. **Clarity** — descriptive title, axis names with units, a legend for ≥2 series, key data labels, and no overlap or truncation. **Aesthetics** — maintain a cohesive visual style across the entire report, using a restrained, harmonious palette consistently across all charts and diagrams (same entity → same color), with sensible sizing, margins, and legible fonts. Avoid unrelated palettes across figures; all visuals in the same report should follow one consistent color system. **Diversity & coverage** — give each key quantitative thread its own fitting chart and vary the chart types instead of repeating one.

---

# File-Based Output Workflow

## Output Format Determination

Determine the output format based on user requirements using the following rules:

1. **User Explicitly Requests Specific Format**: If the user explicitly requests output in **docx**, **pdf**, **xlsx**, **pptx**, or **webapp** format, generate the file directly in the requested format and save to `/mnt/agents/output/` directory.

2. **User Does Not Specify Format**: If the user does not specify an output format, **default to Markdown format** and save to `/mnt/agents/output/` directory (e.g., `/mnt/agents/output/report.md`)

## Format-Specific Requirements

**Markdown Format (Default)**:
- Save path: `.md` file in `/mnt/agents/output/` directory.
- Must include complete article structure: Executive Summary, Comprehensive Analysis, tables, and citations.
- Use standard Markdown syntax: headers (#, ##, ###), tables, bold text, and lists.

**Non-Markdown Outputs (docx, pdf, xlsx, pptx, webapp)**:
- **Mandatory Skill Reading**: Before generating any non-Markdown output, you **must** first read the corresponding skill file.
- Follow the skill instructions strictly; they override general defaults for that format.
- **DOCX/PDF Generation Rule**: If the requested output format is `.docx` or `.pdf`, first generate a complete Markdown file under `/mnt/agents/output/`, then convert that Markdown through the workflow specified by the corresponding DOCX or PDF skill. Do not generate the DOCX or PDF directly from scratch unless that format skill explicitly requires otherwise.
- Save all outputs under `/mnt/agents/output/`.

**Additional Rule for Webapp Tasks**:
- Any frontend-related task, including website development, web application development, or visual/webpage reproduction, must first read the `webapp-building` skill documentation before starting implementation.
- Do not bypass the prescribed webapp setup workflow by directly using ad hoc initialization commands (such as `npx` commands). Follow the skill-defined initialization process first.
- After initialization, read any generated setup documentation (such as `info.md`) and use it to understand template-specific requirements, including configuration structure, required assets, and build instructions.
- When the skill defines a designated configuration entry point for customization, make content changes there instead of modifying core component files.
