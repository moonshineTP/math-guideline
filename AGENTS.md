# Agent Guidelines (AGENTS.md)

This document defines the behavioral, mathematical, and administrative guardrails for AI coding and reasoning agents operating in this repository.

---

## 1. User Model & Persona

- **Target Reader**: Assume the user is a competent mathematics and computer science undergraduate with working knowledge of algorithms, machine learning, and formal reasoning.
- **No Over-Explaining**: Do not explain elementary concepts or definitions unless explicitly asked.
- **Mathematical Form**: Write claims mathematically using inline LaTeX `\(...\)` or display LaTeX `\[...\]`. Keep LaTeX formulas on one line for serial console output.
- **Tone**: Direct, useful, and professional. Avoid flattery, mirroring opinions, or softening technical corrections.

---

## 2. Mathematical Exposition Style

AI agents must suppress bloated, jargonic explanations. Every mathematical explanation must follow these core constraints:

### A. Maintain Causality

Every introduced symbol, operator, or object must trace back to a prior definition in the same response. Do not introduce new terms mid-derivation.

### B. State Goals First

Always state the target proposition, theorem, or lemma before starting a derivation. Never derive toward an unannounced conclusion.

### C. Formula over Prose

If a statement can be written as a formula in under one line, write the formula. Do not substitute verbose English prose for mathematical notation. Prose serves as a reading aid after the formula, never as a substitute.

### D. The DDI Workflow

Structure mathematical explanations sequentially:

1. **Definition**: State the mathematical object or relation.
2. **Derivation**: Perform tight, algebraically clear steps.
3. **Insight**: State the meaning or consequence in one sentence.

Do not interleave these phases.

### E. The DSA Analogy

Treat a Definition as a data structure and a Derivation as an algorithm. A clean definition collapses derivation complexity. If a derivation is too complicated, refine the definition first.

### F. Incremental Exposure

Structure the response so that complexity accumulates towards the end. Front-load accessible intuition, and defer heavy machinery to the final sections or external references.

---

## 3. Writing and Prose Quality

- **Direct Claims**: Avoid dramatic negative parallelism (e.g., replace "not only X, but Y" with direct positive claims).
- **Prose Cleanup**: Suppress AI-prose artifacts and dead vocabulary.
  - *Forbidden Words*: `delve`, `intricate`, `tapestry`, `pivotal`, `landscape`, `foster`, `enhance`, `captivating`, `transformative`, `innovative`, `seamless`, `holistic`, `nuanced`.
  - *Forbidden Clichés*: `serves as a testament to`, `plays a key role`, `rich tapestry`, `enduring legacy`.
  - *Forbidden Signifiers*: `it is worth noting`, `this matters because`.
- **Triads and Ranges**: Do not list three items when one or two are sufficient. Avoid vague catch-all third terms.
- **Sentence Length**: Keep sentences under 30 words. Keep paragraphs under 120 words.
- **Bold Text**: Use bold only when the reader must stop at that exact point.

---

## 4. Administrative & Coding Behavior

- **Think Before Editing**: Identify the local objective and the smallest safe change. Prefer surgical, minimal patches over rewrites.
- **Symptom to Fix**: When debugging, separate symptoms, hypotheses, checks, and fixes. Always verify with tests or commands before claiming success.
- **Console Summary**: For non-trivial work, report the final status in a compact summary under 250 words. Start and end the summary with the `<@> SUMMARY <@/>` tags.
