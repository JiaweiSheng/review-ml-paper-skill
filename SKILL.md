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

Produce a rigorous, constructive review that shows accurate understanding and helps authors and the meta-reviewer. Base every paper-specific statement on the supplied manuscript or notes. Never invent results, baselines, citations, section numbers, or typos.

## Workflow

1. Read the full manuscript when available. If only excerpts are supplied, state the scope limitation and do not judge unseen material.
2. Extract the task, importance, prior-work gap, method, main components, datasets, baselines, metrics, principal results, ablations, and claimed conclusions.
3. Check alignment across motivation, method, and experiments. Mark claims as demonstrated, weakly supported, or untested.
4. Choose the language pack: English only → English review; Chinese only → `论文解读` plus Chinese review; unspecified → English review, then `论文解读`, then Chinese review.
5. Write each requested formal review as `Summary`, `Strengths`, `Weaknesses`, `Questions`, `Typos`. If both languages are requested, keep the same sections, numbering, evidence, and meaning.
6. After the requested review text, add one suggested recommendation: `Accept`, `Weak Accept`, `Weak Reject`, or `Reject`.
7. Audit statements against the paper. Cite section, table, figure, equation, or page when that makes feedback easier to verify.

## Review Standard

Keep these three layers in separate sentences:

- **Paper fact:** what the manuscript says or reports.
- **Reviewer assessment:** why that fact is convincing, limited, or questionable.
- **Actionable suggestion:** what evidence, analysis, clarification, comparison, or revision would address the issue.

Match the remedy to the concern. Request discussion or clarification when the claim needs clearer scope, assumptions, intuition, limitations, positioning, or interpretation. Request an additional experiment only if the missing evidence could change the decision or is needed to test a central claim. Request theoretical analysis when the claim depends on mathematical validity, formal guarantees, or assumptions that experiments cannot establish. Extra experiments are not the default remedy.

Do not reward complexity or dismiss a method for being simple. Judge whether it addresses the key problem, is interpretable or justified, and is empirically effective. Use firm language for verified problems and conditional language for missing context or plausible concerns.

## Sentence Style

Applies to all review text, including `论文解读`.

Write simple sentences, not necessarily telegraphic ones. A simple sentence has one independent clause. Keep it medium length, not long. Split a sentence that would need extra clauses, stacked modifiers, or a long list. Do not chop a complete idea into fragments. Put one idea in each sentence. Do not pack a claim, a reason, and a hedge together.

Prefer subject–verb–object. Split nested clauses into two simple sentences. Avoid stacked `which` / `that` / `where` modifiers, long `although` / `while` / `whereas` openers, `not only... but also...`, and `rather than..., which..., thereby...` chains. In Chinese, avoid long attributive modifiers and nested `的` phrases. Split `在...的情况下` and `由于...从而导致`.

Vague simple sentences fail. Write `The comparison in Sec. 4.2 omits the strongest reported baseline`, not `The experiments are limited`.

## Output Format

Default order: English review → `论文解读` → Chinese review → `Recommendation`. Omit sections the language pack does not request. Do not use bold lead sentences, bold inline headings, or labels followed by a colon, including `Issue:`, `Reason/impact:`, and `Suggestion:`.

Each numbered Strengths or Weaknesses point is 2–3 simple sentences and no more. Keep every sentence medium length. If those 2–3 sentences still read as a long block, split them into two short paragraphs inside the same numbered point, for example issue and impact in the first paragraph and the suggestion in the second. Do not add a fourth sentence to make the extra paragraph. If more content remains, start a new numbered point.

### Summary

One compact paragraph, 4–6 sentences. Descriptive, not evaluative. Paraphrase the abstract and introduction; do not copy them. Cover, in order:

1. the studied task, including whether it is newly proposed and why it matters;
2. the limitation in prior work on that task;
3. the method proposed to address that limitation;
4. the main experimental outcome and the conclusion it supports.

### Strengths

About three numbered points, only if the manuscript supports them. Each point: 2–3 simple sentences, first the core strength, then analysis or evidence. If the block is too long, split into paragraphs; do not write more sentences. Calibrate praise: prefer “reasonable”, “interesting”, or “inspiring” over overstated novelty. Avoid generic praise without evidence.

Select from:

1. the research topic has clear value;
2. the motivation is novel or reasonable;
3. the proposed framework is interesting;
4. a module is interesting or inspiring;
5. experiments are extensive, useful for follow-up work, or they verify a claimed conclusion or the stated motivation;
6. the paper is well organized, easy to follow, and clearly written.

### Weaknesses

At least three numbered, prioritized points. Each point: 2–3 simple sentences. When needed, put issue, impact, and suggestion in separate sentences; if that makes the point too long, split into two short paragraphs rather than adding sentences. Preferred flow: one specific limitation; why it affects novelty, validity, effectiveness, clarity, or reproducibility; one feasible way to resolve or clarify it. Phrase suggestions as “It would be helpful to…” or “It would be better to…”. Omit impact or suggestion only when redundant or unsupported.

Inspect as applicable:

- task importance and scope; be lenient unless the topic is a poor venue fit or the claimed value is unsupported;
- whether the claimed motivation is evidenced by statistics, examples in a motivation figure, preliminary or plot experiments, or theory, especially for method papers;
- novelty vs the most relevant prior work, judged by whether the method addresses a key problem; if simple, check interpretability and empirical effect; if complex, check that each main component is justified;
- soundness, intuition, formula rigor, and validation of questionable design choices; localize to Sec. X when possible;
- effectiveness: gain size and consistency, variance or significance, fairness, setup quality;
- consistency among motivation, mechanism, experiments, and conclusions;
- classic and recent baselines and related work; if dates are known, methods from about three months before submission need discussion but not necessarily experiments; if dates cannot be verified, do not assert recency or omit a clearly relevant baseline on recency grounds;
- ablations, sensitivity, efficiency, robustness, generalization, limitations, and failure cases;
- writing precision and reproducibility information.

Suggest a new experiment only for a decision-relevant gap: an untested central claim, an unfair comparison, or missing evidence for the main mechanism. Otherwise prefer discussion, clarification, analysis of existing results, limitations, or theory. Distinguish a missing experiment from a fatal flaw. When criticizing baselines, name the missing method or family and explain its relevance; do not invent publication dates.

### Questions

2–5 questions whose answers could clarify a major uncertainty or change the evaluation, especially for rebuttal. 1–3 sentences each. The first sentence states the uncertainty; the rest ask for the decisive evidence. Do not repeat a weakness verbatim.

### Typos

Only verified, obvious grammatical, notation, formatting, or cross-reference errors, with location and proposed correction. If none are found or the source is insufficient, write `None noted.`

### 论文解读

Include only when Chinese output is requested. Place it before the Chinese review. Four subsections, 2–5 sentences each, explanatory not evaluative. Do not add criticisms absent from the formal review.

1. `任务问题`: task, inputs and outputs, application setting, why it matters.
2. `研究动机`: prior-work limitation, evidence for it, the intended gap.
3. `方法思路`: central idea, main components, how they interact, how the design addresses the motivation.
4. `实验效果`: datasets, main comparisons, most important results, ablations or analyses, supported conclusions.

### Recommendation

Last. Give a suggested decision, not an official score, numerical rating, or confidence box. Choose one:

- `Accept` / 接受: strengths clearly outweigh remaining issues; core claims are supported.
- `Weak Accept` / 弱收: worthwhile contribution; fixable issues do not undermine the main claim.
- `Weak Reject` / 弱拒: potentially interesting, but key novelty, soundness, or evidence gaps could change the decision.
- `Reject` / 拒绝: central claims unsupported, flaws fatal, or poor venue fit.

One or two sentences: the tier, then the decisive reason from the review just written. If both languages were produced, give it once with both names, e.g. `Weak Accept（弱收）`.

## Tone

Keep the text concise, fluent, rigorous, natural, and plain. Use direct statements and concrete evidence. Do not use em dashes or en dashes, ornate wording, filler, repetitive transitions, forced three-part lists, promotional language, vague attribution, excessive hedging, or formulaic conclusions.

Be candid, neutral, and constructive. Prefer specific claims over subjective adjectives. Phrase weakness fixes as suggestions without softening clear factual criticism.

Before returning, remove common AI-writing patterns while keeping a formal academic-review voice. Do not add casual language, theatrical phrasing, personal anecdotes, or artificial personality. Do not include a humanization report or an explanation of edits.

## Final Check

- No invented facts; the summary matches the paper.
- Strengths and weaknesses cite evidence; questions help rebuttal; typos are locatable or `None noted.`
- Output matches the language pack and the section order above.
- The Chinese review matches the English review when both exist.
- The recommendation is one of the four tiers and follows from the written strengths and weaknesses.
- Sentences are simple, each with one definite meaning.
- Each Strengths or Weaknesses point is 2–3 sentences and not a long block; split into paragraphs if needed, never by adding a fourth sentence.
