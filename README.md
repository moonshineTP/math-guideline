# Math Guideline

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
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

## Repository Status and Metrics

| Metric | Count |
|--------|-------|
| Skills | 2 |
| Samples | 2 |
| Supporting Scripts | 2 |
| Total Markdown Files | 6 |
| Total Words | ~6,000 |

*Current completion status:* Fully functional reference guidelines and validation suite.

---

## Getting Started

### Installation

To use the math guidelines in your agentic workspace, clone the repository:

```bash
git clone https://github.com/moonshineTP/math-guideline.git
cd math-guideline
```

### Usage

#### 1. Applying Guidelines to AI Agents

To immediately align your AI assistant (e.g., Cursor, Gemini, Claude, or Copilot) with these guidelines, copy the
`AGENTS.md` file from the root of this project into the root directory of your workspace. Coding assistants
automatically parse this file at the start of a session and apply the behavioral guardrails.

#### 2. Running the Supporting Scripts

The repository includes scripts to collect documentation metrics and validate your project's README:

- **Metrics Collection**: Gathers stats on markdown files, word count, equations, lists, and tables.
  ```bash
  python skills/readme-generator/scripts/collect-site-metrics.py /path/to/project
  ```

- **README Validation**: Checks your README for formatting issues, structure, and completeness.
  ```bash
  python skills/readme-generator/scripts/validate-readme.py README.md
  ```

---

## Repository Structure

```text
math-guideline/
├── LICENSE                          # MIT License file
├── README.md                        # This file
├── AGENTS.md                        # Behavioral rules and instruction set for agents
└── skills/                          # Claude AI skills
    ├── math-guideline/              # Core math rules and case study samples
    │   ├── SKILL.md                 # Math exposition pitfalls and patterns
    │   └── samples/
    │       ├── Sample.md            # Correct exposition sample (Vietnamese)
    │       └── Antisample.md        # Pitfalls case study annotation
    └── readme-generator/            # README generation skill
        ├── SKILL.md                 # README generator guidelines
        ├── README.md                # Documentation for readme-generator
        ├── references/
        │   └── badges.md            # Badge styling and layout reference
        └── scripts/
            ├── collect-site-metrics.py  # Script for scanning repo metrics
            └── validate-readme.py       # Script for validating formatting and sections
```

---

## Reporting Issues

Found a bug, typo, or have a suggestion for improving the guidelines or scripts? Please open an issue on GitHub:

[GitHub Issues](https://github.com/moonshineTP/math-guideline/issues)

When reporting issues, please include:

- A description of the issue or improvement suggestion.
- Steps to reproduce (for script bugs).
- An example of mathematical text that violates or conforms to the guidelines.

---

## Contributing

Contributions are welcome to refine the guidelines or expand the validation tooling. To contribute:

1. Fork the repository.
2. Create a feature branch (`git checkout -b feature/amazing-improvement`).
3. Commit your changes (`git commit -m 'Add mathematical pattern X'`).
4. Push to the branch (`git push origin feature/amazing-improvement`).
5. Open a Pull Request.

---

## Acknowledgements

This project is built on the shoulders of giants:

- **[Andrej Karpathy Guidelines](https://github.com/multica-ai/andrej-karpathy-skills)** - For pioneering project-level behavioral rules for coding agents.
- **[Claude Skills](https://github.com/dmccreary/claude-skills)** - For the structure of self-contained tool and guideline folders.
- The open-source community for developing static analysis and LLM behavioral guidelines.

---

## Contact

**moonshineTP**

- GitHub: [@moonshineTP](https://github.com/moonshineTP)
- Project Remote: [math-guideline](https://github.com/moonshineTP/math-guideline)

---

## License

This project is licensed under the MIT License. See [./LICENSE](./LICENSE) for full details.
