---
name: math-guideline
description: Behavioral guidelines to reduce common LLM mistakes in mathematical explanation. Use when writing, reviewing, or explaining mathematical content to avoid undefined notation, goal-free exposition, word-over-math substitution, and open-ended tangents.
license: Apache-2.0
---

# Math-Guide

Behavioral guidelines for mathematical exposition, modeled on the Karpathy Guidelines for code. These are derived from observed failure modes in LLM-driven mathematical explanation, with a concrete case study.

**Tradeoff:** These guidelines bias toward precision and completeness over speed. For a quick sanity check or a one-liner definition, use judgment.

---

# Common Pitfalls in LLM Mathematical Exposition

## Pitfall 1: Treating the Reader as a Definition Collector

**Assume the reader is mathematically competent. Do not over-define. Do not under-define.**

The failure mode is often: LLMs either re-explain elementary concepts the reader already knows (wasted words), or introduce new objects mid-derivation without announcement (broken causality). The target reader of a math explanation is a competent peer that seek to understand cross-domain concepts. Explain like a oral presentation.

Concretely:
- Do not define standard objects unless the question signals unfamiliarity with them
- Do state the non-standard or context-specific definition of any object you introduce, even if it has a familiar name
- Derivation steps that collapse an expression are not definitions. Writing $\nabla \cdot (\rho \nabla \log \rho) = \Delta \rho$ is a derivation step; it does not excuse skipping a definition of what $\Delta$ acts on.

The test: for every symbol in your response, ask whether the reader has been given a definition (or can be assumed to know one).

---

## Pitfall 2: Explaining Without a Proof Goal

**State the proposition before the derivation. Never derive toward an unannounced conclusion.**

The most common failure in LLM mathematical text is a derivation that never names its target. The reader sees a sequence of manipulations and only learns the conclusion at the end.

Before any derivation:
- State the object to be proved or derived.
- Name which definition, lemma, or formula the derivation will apply.
- If the derivation introduces an intermediate object, say so before introducing it.

A block of math without a preceding goal statement is, at best, a calculation exercise. It is not an explanation.

---

## Pitfall 3: Word Substitution for Obvious Math

**If a statement has a concise mathematical form, write that form. Prefer notation over paraphrase.**

LLMs habitually describe what an expression does in English prose, rather than writing the expression itself. This is the dominant pathology in mathematical AI text. It reads like a transcript of someone who has memorized results but avoids blackboards.

Examples of the failure:
- "The pushforward condition means that sampling from the source and applying the map gives the target distribution" -- write $T_\# \rho_0 = \rho_1$, then define it via $\int f(y)\, d\rho_1(y) = \int f(T(x))\, d\rho_0(x)$ if precision is needed.
- "The plan is concentrated on pairs of the form source point and its image" -- write $\pi^\star = (\operatorname{id}, T)_\# \rho_0$.

The rule: any claim that can be written as a formula in under one line should be written as a formula. Prose goes after, as a reading aid, not before as a substitute.

---

## Pitfall 4: Ending on Open Questions Instead of Closing the Asked One

**Close the question that was asked before opening any new concern.**

LLMs tend to end mathematical responses by gesturing at generalizations, limitations, open problems, or adjacent topics. The result is a response that partially answers the original question and then branches into three loosely connected subtopics, none of which was requested.

This is particularly damaging in math because the reader often cannot distinguish "this is a genuine open question" from "this is background the LLM is padding with".

The discipline:
- Identify the exact question asked. Close that question with a complete, self-contained answer.
- If a natural follow-on exists and is genuinely illuminating, add it as a single clearly marked remark, not as a full new section.
- Do not introduce new notation, new objects, or new proof obligations in a closing paragraph. A closing insight should refer only to objects already in scope.

---

# Patterns for Correct Mathematical Exposition

## Pattern 1: Causality - Every Object Must Have an Antecedent

**Every formula, operator, or object introduced must trace back to a prior definition or result in the same response.**

This is the structural backbone of correct mathematical exposition. It is also the easiest to violate when generating text based only on correlations.

Implementation:
- Before writing any formula, ask: have all symbols appearing in it been defined in this response, or can they be assumed known?
- If a new operator is introduced mid-derivation, stop and introduce it explicitly before using it.
- Cross-reference is good practice, not redundancy.

Causality is the mathematical analogue of Karpathy's "every changed line traces to the request." Every introduced symbol traces to an introduction.

---

## Pattern 2: The DDI Workflow - Definition, Derivation, Insight

**Structure every mathematical block as: state the object, derive the result, draw the insight. Do not interleave these.**

This is the core workflow.

At the local level:
- **Definition:** Name and formally state the object or relation.
- **Derivation:** Carry out the steps. This is where the algebra, calculus, or combinatorics lives. Keep it tight, annotate each non-trivial step.
- **Insight:** State what the derivation means. This is one sentence or one boxed statement.

At the global level, multiple DDI blocks should appear in dependency order: the insight of block $k$ may become the definition used in block $k+1$.

---

## Pattern 3: The DSA Analogy - Definition is Data Structure, Derivation is Algorithm, Insight is Comment

**A clean definition determines the derivation. If the derivation is complicated, the definition is probably imprecise.**

This analogy sharpens the DDI workflow. In software, a well-chosen data structure makes the algorithm short and obvious. In mathematics, a well-stated definition makes the derivation mechanical. If you find yourself writing a long derivation, ask whether a cleaner definition would collapse it.

Applied to the OT case:
- Define $W_2^2$ as the infimum of kinetic energy over continuity-equation-constrained curves. This definition immediately encodes transport cost as kinetic energy; the definition *is* the transport problem.
- From that definition, the Wasserstein gradient of a functional $\mathcal{F}$ follows by a one-line duality argument.
- The heat equation then drops out mechanically by substituting $\mathcal{F} = \operatorname{Ent}$.

Insight should be sparse. A good definition and a clean derivation are self-documenting. Insight text is for pointing at the non-obvious or globally connecting consequence.

---

## Pattern 4: Incremental Exposure - Front-Load the Accessible, Defer the Hard

**Write so that complexity accumulates toward the end. The first paragraph must be readable; the last may require full machinery.**

Mathematical responses should be structured as a gradient, not a uniform density of difficulty. A reader who stops at any point should have learned something correct and usable. A reader who reaches the end has the full picture.

Implementation:
- Open with the key statement in its simplest correct form (e.g. the TL;DR).
- Proceed to the formal setup: the objects, their definitions, the theorem to be proved.
- Carry out the derivation.
- Place extensions, analogues, and generalizations last.
- For material that genuinely requires more background than the response can supply, place a forward pointer: "a full treatment requires the Riemannian structure on $(\mathcal{P}_2, W_2)$; see [Jordan-Kinderlehrer-Otto 1998]." Do not attempt to derive it inline.
