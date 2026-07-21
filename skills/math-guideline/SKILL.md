---
name: math-guideline
description: >
  Produce, audit, or repair mathematical explanations, proofs, derivations, and
  solution writeups. Use whenever a response contains non-trivial mathematics or
  the user asks to explain, verify, formalize, derive, prove, audit, or improve a
  mathematical argument. Apply this skill before drafting mathematical content,
  including short answers when a hidden assumption, domain restriction, or notation
  ambiguity could change the result.
license: Apache-2.0
author: MoonshineTP
---

# Math Guideline

Write mathematical content as a verifiable, human-readable argument for a competent
reader. Preserve the user's intended notation, requested depth, and proof style.

## Execution Contract

Establish the following before deriving anything:

1. **Target**: state the proposition, quantity, or question to resolve.
2. **Setting**: give the domain, assumptions, and conventions that affect truth.
3. **Dependencies**: introduce non-standard notation before first use and name
   the definitions, lemmas, or identities used.
4. **Boundary**: answer only the requested question. Treat extensions as an
   optional final remark.

Use an agentic task frame when the request concerns an artifact or repository:

```text
Starting state: [given theorem, draft, code, or source]
Target state: [claim to establish or correction to make]
Scope: [allowed notation, sources, files, and depth]
Acceptance criteria: [facts that the final argument must establish]
Stop condition: [the requested claim is closed]
```

Do not claim a result that depends on unstated regularity, existence, convergence,
boundary, or heuristic assumptions.

## Default Workflow

### 1. State the result

Lead with the answer in its simplest correct form. For a proof or derivation,
state the exact target before the first calculation. For a verification request,
state the claim being checked and the criterion for failure.

### 2. Build the local vocabulary

Define only symbols that are non-standard, overloaded, local to the argument,
or likely to be ambiguous. Keep standard material implicit for the stated
audience. Declare conventions such as row versus column vectors, positive directions,
index ranges, logarithm base, norm base, or inner-product convention when they matter.

Every displayed formula must be readable from prior context. If a symbol cannot
be defined compactly, introduce it in prose immediately before the formula.

### 3. Derive in dependency order

Use this local sequence for each argument block:

1. **Definition or premise**: state the usable relation.
2. **Operation**: apply one named rule, theorem, or algebraic step at a time.
3. **Justification**: annotate steps that are not immediate for the intended reader.
4. **Conclusion**: state the result obtained and its role in the target.

Prefer a concise formula when it carries the claim precisely. Follow it with
prose that interprets the formula; do not replace a one-line mathematical claim
with a paragraph of prose.

### 4. Close the request

Restate the answer in the user's terms. Do not introduce fresh notation, a new
proof obligation, or an unrelated generalization after the target is settled.

## Output Modes

Choose the smallest mode that satisfies the request.

| Request | Required structure |
| --- | --- |
| Definition or intuition | Answer, notation needed to parse it, one consequence or example. |
| Derivation | Target, setup, numbered transformations with justifications, conclusion. |
| Proof | Proposition, assumptions, proof, explicit conclusion. |
| Counterexample | False claim, construction, verification of each required property, violated conclusion. |
| Review or debug | Claim under review, first invalid step or missing assumption, corrected statement or repair path. |
| Computation | Formula, substitutions, units or domains, result, sanity check where cheap. |

## Edge Cases and Fallbacks

### Missing assumptions

If the conclusion is true only under additional assumptions, state the weakest
assumptions you can justify and continue conditionally. If their status cannot
be determined, write the conditional result and mark the unresolved premise.
Do not silently select a convenient interpretation.

### Ambiguous notation

Use the user's established convention. If none exists and conventions change the
answer, state the convention at first use. If two readings yield materially
different results, give both concise results or ask one focused question before
committing.

### Omitted proof step

Compress routine algebra. Expand a step when it changes a sign, exchanges a
limit or derivative, invokes a theorem, divides by a possibly zero quantity, or
uses a property not already established. When the full proof exceeds scope,
identify the exact theorem needed and what it would establish.

### Invalid or incomplete claim

Do not repair a false statement by changing it without notice. Give a
counterexample when practical; otherwise identify the failing implication.
Then state the nearest correct version and the additional hypothesis it needs.

### Insufficient source material

Separate derivable facts from source-dependent facts. Do not fabricate a lemma,
citation, numerical value, or proof. State the precise missing item and provide
the strongest conditional conclusion available from the supplied material.

### Numerical or symbolic uncertainty

Check dimensions, signs, endpoints, and exceptional values. If a computation
depends on unstable floating-point arithmetic, report an interval, tolerance, or
conditioning caveat instead of unsupported exactness.

### Overlong request

Provide the requested main result and the first dependency-complete slice. Name
the next prerequisite without pretending the full development was supplied.

## Preflight Checklist

Run this before finalizing:

```text
[ ] The opening states the requested result, not only background.
[ ] Every non-standard symbol is defined before first use.
[ ] Domains, quantifiers, and conventions are explicit where they affect truth.
[ ] Each non-routine transformation has a valid justification.
[ ] No division by zero, invalid interchange, sign change, or boundary case is hidden.
[ ] The conclusion matches the stated target and does not overclaim.
[ ] New material after the conclusion is omitted or clearly optional.
[ ] Claims tied to a source are supported by that source or marked unresolved.
```

## Failure Patterns

- Do not derive toward an unstated conclusion.
- Do not use notation as a substitute for definition.
- Do not explain elementary material at the cost of omitting the decisive step.
- Do not equate an analogy, heuristic, or numerical observation with a proof.
- Do not add adjacent topics merely because they are mathematically related.

For an extended example of these failure modes in optimal transport, read
[samples/Antisample.md](samples/Antisample.md) only when it helps diagnose a
similar exposition problem.
