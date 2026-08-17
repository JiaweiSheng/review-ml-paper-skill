---
name: review-ml-paper
description: Review machine learning, data mining, AI, and computer science research papers in the user's preferred structure and tone. Use when asked to read a manuscript, PDF, abstract, introduction, experimental results, or existing review notes and produce or revise a peer review containing Summary, Strengths, Weaknesses, Questions, and Typos, especially for conference review or rebuttal workflows. Use for 审稿, 论文评审, peer review, ML paper review.
license: MIT
compatibility: Any agent that supports Agent Skills, including Cursor, Codex, and Claude Code.
metadata:
  version: "1.0.0"
  author: JiaweiSheng
---

# Review ML Paper

Produce a rigorous, constructive review that demonstrates accurate understanding and helps both authors and the meta-reviewer. Base every paper-specific statement on the supplied manuscript or notes. Never invent results, baselines, citations, section numbers, or typos.

## Workflow

1. Read the full manuscript when available. If only excerpts are supplied, state the scope limitation and avoid judging unseen material.
2. Extract the task, importance, prior-work gap, proposed method, main components, datasets, baselines, metrics, principal results, ablations, and claimed conclusions.
3. Check alignment across motivation, method, and experiments. Identify which claims are demonstrated, weakly supported, or untested.
4. Choose the language pack. If the user asks for English only, write only the English review. If the user asks for Chinese only, write the Chinese `论文解读` and the Chinese review. If the user does not specify, write all three: English review, `论文解读`, and Chinese review.
5. Draft each requested formal review in this order: `Summary`, `Strengths`, `Weaknesses`, `Questions`, `Typos`. When both languages are requested, keep the same sections, numbering, evidence, and meaning.
6. When Chinese output is included, write `论文解读` before the Chinese review, organized as `任务问题`, `研究动机`, `方法思路`, and `实验效果`.
7. After the requested review text, add a suggested recommendation: `Accept`, `Weak Accept`, `Weak Reject`, or `Reject`.
8. Audit all statements against the paper. Use section, table, figure, equation, or page references when they make feedback easier to verify.

## Review Standard

Separate three layers:

- **Paper fact:** what the manuscript explicitly says or reports.
- **Reviewer assessment:** why that fact is convincing, limited, or questionable.
- **Actionable suggestion:** what evidence, analysis, clarification, comparison, or revision would address the issue.

Distinguish the type of support needed for each concern:

- Use a discussion or clarification request when the claim mainly needs clearer scope, assumptions, intuition, limitations, positioning, or interpretation.
- Request an additional experiment only when the missing evidence could materially change the review decision or is necessary to test a central claim.
- Request theoretical analysis or proof when a central claim depends on mathematical validity, formal guarantees, or assumptions that empirical evidence alone cannot establish.

Do not treat experiments as the default remedy. A focused discussion, clearer argument, existing result analysis, or theoretical justification may provide sufficient support. State which form of support is appropriate and why.

Do not reward complexity by itself or dismiss a method merely for being simple. Judge whether it addresses the key problem, is interpretable or justified, and is empirically effective. Calibrate certainty: use firm language for directly verified problems and conditional language for missing context or plausible concerns.

## Output Format

### Summary

Write one compact paragraph, normally 4–6 sentences. The aim is to show authors that the reviewer understood the paper and to give the meta-reviewer a fast overview. Draw from the abstract and introduction, but paraphrase rather than copying either. Keep this section descriptive, not evaluative. Cover, in order:

1. the studied task, including whether it is newly proposed and why it matters;
2. the limitation in prior work on that task;
3. the method proposed to address that limitation;
4. the main experimental outcome and the conclusion it supports.

### Strengths

Give about three numbered points, selecting only strengths supported by the manuscript. Write 2–3 sentences per point. Use the first sentence to summarize the core strength and the remaining sentence or two to give concrete analysis or evidence. Start directly with the substance; do not use a bold lead sentence, bold inline heading, or label followed by a colon. Calibrate praise: prefer “reasonable”, “interesting”, or “inspiring” over overstated novelty claims.

Select from these dimensions when the manuscript supports them:

1. the research topic has clear value;
2. the motivation is novel or reasonable;
3. the proposed framework is interesting;
4. a module is interesting or inspiring;
5. experiments are extensive, useful for follow-up work, or they verify a claimed conclusion or the stated motivation;
6. the paper is well organized, easy to follow, and clearly written.

Avoid generic praise without evidence.

### Weaknesses

Give at least three numbered, prioritized points. Write 2–3 fluent sentences per point. A point may include an issue, its impact, and a suggestion, but these are ingredients of the prose, not required labels. Do not write `Issue:`, `Reason/impact:`, `Suggestion:`, a bold lead sentence, a bold inline heading, or any label followed by a colon.

Prefer this flow when it fits: first sentence states an objective, specific limitation; the remaining sentence or two explain why it affects novelty, validity, effectiveness, clarity, or reproducibility, and offer a feasible way to resolve or clarify it. Phrase suggestions constructively, such as “It would be helpful to…” or “It would be better to…”. Omit an impact or suggestion only when it would be redundant or unsupported; never pad a point with empty labels.

Inspect these dimensions as applicable:

- task importance and scope; be lenient on importance unless the topic is a poor venue fit or the claimed value is unsupported;
- whether the claimed motivation is evidenced by statistics, examples in a motivation figure, preliminary or plot experiments, or theory, especially for method papers;
- methodological novelty relative to the most relevant prior work, judged by whether it addresses a key problem rather than by subjective impression; do not treat complexity as novelty; if the method is simple, judge whether it addresses the key problem, is interpretable, and is empirically effective; if it is complex, check that each main component is justified;
- methodological soundness, intuition, formula rigor, and validation of questionable design choices; localize concerns to sections when possible, such as a problem or uncertainty in Sec. X;
- effectiveness, whether gains are clear, magnitude and consistency of gains, variance or significance, experimental fairness, and setup quality;
- consistency among motivation, proposed mechanism, experiments, and conclusions: whether the method addresses the motivated problem, and whether the experiments measure the degree of that resolution;
- coverage of classic and recent baselines and completeness of related work; if submission or public dates are known, methods appearing within about three months before submission need not be experimental baselines but should be discussed; if dates cannot be verified, do not assert recency or omit a clearly relevant baseline on recency grounds;
- ablations, sensitivity, efficiency, robustness, generalization, limitations, and failure cases;
- writing precision and information needed for reproducibility.

Do not demand every possible experiment. Suggest a new experiment only for a key issue that could affect the review decision, such as an untested central claim, an unfair comparison, or missing evidence for the main mechanism. For other issues, prefer discussion, clarification, analysis of existing results, limitations, or theoretical justification as appropriate. Make the needed evidence type clear in the prose without adding mechanical labels. Distinguish a missing experiment from a fatal flaw. When criticizing baseline coverage, identify the missing method or method family and explain its relevance; do not invent publication recency.

### Questions

Ask 2–5 concise questions whose answers could clarify a major uncertainty or affect the evaluation, especially for conferences with a rebuttal. Keep each numbered point to 1–3 sentences. When explanation is needed, use the first sentence to state the uncertainty and the remaining sentence or two to ask for the decisive evidence or explanation. Do not add bold lead sentences or repeat a weakness verbatim.

### Typos

List only verified, obvious grammatical, notation, formatting, or cross-reference errors, with location and proposed correction. Keep each point brief and do not add bold lead sentences. If none are found or the source is insufficient, write `None noted.` Never fabricate typos.

## 论文解读

When Chinese output is included, place this section before the Chinese review. In the default three-part output, it sits between the English review and the Chinese review. Omit it for English-only output. Use these four subsections in order:

1. `任务问题`: Explain the task, inputs and outputs, application setting, and why the problem matters.
2. `研究动机`: Explain the limitation in prior work, the evidence for that limitation, and the gap the paper intends to address.
3. `方法思路`: Explain the central idea, main components, how they interact, and how the design addresses the stated motivation.
4. `实验效果`: Summarize the datasets, main comparisons, most important results, ablations or analyses, and the conclusions the evidence supports.

Write 2–5 concise Chinese sentences for each subsection. Select only the most important content needed to understand the review. Keep this section explanatory rather than evaluative, and do not introduce criticisms that are absent from the formal review.

## Recommendation

Place this section last, after all requested review text. The output order is: English review when requested, then `论文解读` when Chinese is included, then the Chinese review when requested, then `Recommendation`. Do not put the recommendation before or inside `Summary`, `Strengths`, `Weaknesses`, `Questions`, `Typos`, or `论文解读`. Give only a suggested decision, not an official conference score, numerical rating, or confidence box.

Choose exactly one of these four tiers:

- `Accept` / 接受: strengths clearly outweigh remaining issues, and the core claims are supported.
- `Weak Accept` / 弱收: a worthwhile contribution with fixable issues that do not undermine the main claim.
- `Weak Reject` / 弱拒: the paper is potentially interesting, but key novelty, soundness, or evidence gaps could change the decision.
- `Reject` / 拒绝: central claims are unsupported, the flaws are fatal, or the topic is a poor venue fit.

Write one or two sentences: the chosen tier, then the decisive reason grounded in the review just written. If both English and Chinese reviews are produced, give the recommendation once at the end, with both names, for example `Weak Accept（弱收）`.

## Tone and Language

Unless the user asks for one language only, write the formal English review first, then the Chinese `论文解读`, and finally a complete corresponding Chinese review. If both formal reviews are produced, preserve the same substance, numbering, level of criticism, and paper references; do not add or omit claims during translation.

Keep the produced text concise, fluent, rigorous, natural, and plain. Prefer short or medium-length sentences and simple syntax. Avoid long sentences, nested clauses, unnecessary abstraction, ornate wording, filler, repetitive transitions, forced three-part lists, promotional language, vague attribution, excessive hedging, and formulaic conclusions. Use direct statements and concrete evidence. Do not use em dashes or en dashes.

Humanize the drafted review text by default before returning it. Remove common AI-writing patterns while preserving an appropriately formal academic-review voice. Vary sentence rhythm naturally, but do not inject casual language, theatrical phrasing, personal anecdotes, or artificial personality. Do not include a humanization report, draft critique, or explanation of edits in the delivered review.

Be candid, neutral, and constructive. Prefer specific claims over subjective adjectives. Phrase weakness fixes as suggestions without weakening clear factual criticism.

## Final Quality Check

Verify that the summary matches the paper; strengths and weaknesses cite concrete evidence; weakness points read as fluent prose without `Issue:` / `Reason/impact:` / `Suggestion:` labels; claims, equations, tables, and baselines are not misrepresented; questions are useful for rebuttal; typos are real and locatable; and no content is invented. Confirm that each major strength and weakness has 2–3 sentences, its first sentence gives the core point, and its remaining sentences provide analysis or a proportionate suggestion when those help. Confirm that experimental requests are limited to decision-relevant evidence, while discussion and theoretical support are used where more appropriate. Check that `论文解读` is included whenever Chinese output is requested, with all four required subsections and 2–5 sentences each; that no point begins with bold text; that the Chinese review faithfully matches the English review when both are produced; and that a single four-tier recommendation appears after the requested review text and is consistent with the written strengths and weaknesses. Run a final humanization pass on the produced languages and remove overlong or unnecessarily complex sentences.
