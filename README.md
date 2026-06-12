# Math Guideline

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Antigravity](https://img.shields.io/badge/Built%20with-Antigravity-blue?logo=google)](https://deepmind.google)
[![Claude Skills](https://img.shields.io/badge/Uses-Claude%20Skills-DA7857?logo=anthropic)](https://github.com/dmccreary/claude-skills)
[![GitHub](https://img.shields.io/badge/GitHub-moonshineTP%2Fmath--guideline-blue?logo=github)](https://github.com/moonshineTP/math-guideline)

An agentic memory system designed to suppress bloated, jargonic LLM mathematical explanations. This repository defines
guidelines and workflows for AI agents to deliver mathematical exposition that is definitive, rigorous, insightful,
and beginner-friendly.

---

## Overview

Mathematical communication between AI agents and human users is often plagued by specific failure modes. Large
Language Models tend to over-explain elementary concepts, introduce undefined symbols mid-derivation (breaking
causality), substitute verbose English prose for concise formulas, and wander off into open-ended tangents instead
of closing the question at hand.

Inspired by the Andrej Karpathy guidelines for code (which promote simplicity, surgical changes, and goal-driven
execution), **Math Guideline** provides a corresponding framework for mathematics. It equips AI coding and reasoning
agents with concrete rules to keep explanations clean, structured, and mathematically sound.

Key components of this system include:

- **The DDI Workflow**: Separates mathematical content into Definition, Derivation, and Insight, rather than
  interleaving them.

- **The DSA Analogy**: Treats Definitions as data structures and Derivations as algorithms, enforcing the
  open-closed principle in exposition.

- **Mathematical Causality**: Enforces that every symbol, operator, or notation has a clear, prior definition.

- **Incremental Exposure**: Front-loads accessible, intuitive explanations and defers heavy mathematical machinery.

---

## Reporting Issues

Found a bug, typo, or have a suggestion for improving the guidelines or scripts? Please open an issue on GitHub:

[GitHub Issues](https://github.com/moonshineTP/math-guideline/issues)

When reporting issues, please include:

- A description of the issue or improvement suggestion.
- A concrete metric of degradation/improvement surrounding a reproducible task.
- A TLDR and/or rationale for lengthy PRs.

---

## Acknowledgements

This project acknowledge the usage of:

- **[Andrej Karpathy](https://karpathy.ai/)** and the **[multica-ai/andrej-karpathy-skills](https://github.com/multica-ai/andrej-karpathy-skills)** repository - For pioneering project-level behavioral rules for coding agents.
- **[Dan McCreary](https://github.com/dmccreary)**, creator of the **[readme-generator](https://github.com/dmccreary/claude-skills)** skill - For the structure of self-contained tool and guideline folders and automated README generation workflow.

---

## License

This project is licensed under the Apache License 2.0. See [./LICENSE](./LICENSE) for full details.
