# research-guardian

[![Build & Release Skill](https://github.com/htlin222/research-guardian-skill/actions/workflows/release.yml/badge.svg)](https://github.com/htlin222/research-guardian-skill/actions/workflows/release.yml)
[![GitHub Release](https://img.shields.io/github/v/release/htlin222/research-guardian-skill?include_prereleases&label=skill%20version)](https://github.com/htlin222/research-guardian-skill/releases/latest)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Skills Protocol](https://img.shields.io/badge/protocol-vercel--labs%2Fskills-blue)](https://github.com/vercel-labs/skills)
[![Compatible Agents](https://img.shields.io/badge/agents-40%2B-green)](https://github.com/vercel-labs/skills#supported-agents)

> AI research quality guardian system — automated multi-gate verification for AI-generated research outputs, preventing hallucinations, logic errors, citation fabrication, and novelty misjudgment.

## On Falsifiability and Guardians

> *"In so far as a scientific statement speaks about reality, it must be falsifiable; and in so far as it is not falsifiable, it does not speak about reality."*
> — Karl Popper

Popper drew the sharpest line in the philosophy of science: a claim that cannot, in principle, be shown wrong is not a scientific claim at all. It may be eloquent, internally consistent, even useful — but it does not speak about reality. The trouble with AI-generated research is that it produces statements which *look* falsifiable but have never been subjected to any genuine attempt at falsification. The citations appear checkable but may not exist. The statistics appear rigorous but may rest on design flaws no one audited. The conclusions appear modest but may overreach the evidence by exactly the margin that sounds convincing. In Popper's terms, these are pseudo-scientific outputs wearing the uniform of science. Research Guardian is, at its core, a falsification engine. Each gate is a structured attempt to *break* the claim it receives — to find the missing control group, the fabricated reference, the causal arrow that points the wrong way, the p-value that hides a thousand comparisons. It does not ask "is this well-written?" It asks "can this survive an honest attempt to prove it wrong?" What survives all five gates and the logic chain has not been *verified* — Popper would remind us that verification is not how science works — but it has withstood a serious, multi-angle attempt at refutation. And that is the only warrant any scientific statement can ever have.

## Install

```bash
npx skills add htlin222/research-guardian-skill
npx skills add -g htlin222/research-guardian-skill        # global
npx skills add htlin222/research-guardian-skill --agent claude-code  # specific agent
```

## What it does

Research Guardian is an AI research quality assurance system that automatically performs multi-layer verification when AI agents execute research tasks. It operates as a quality gate in the AI agent pipeline, with 5 independent verification gates plus a cross-cutting logic fallacy chain:

- **Gate 1 — Hypothesis Guard**: Validates research hypotheses against existing literature, checks novelty claims, and detects circular reasoning
- **Gate 2 — Literature Guard**: Verifies citations actually exist, detects hallucinated references, checks for citation ethics violations and predatory journals
- **Gate 3 — Experiment Guard**: Audits experimental design, statistical methodology, power analysis, and reproducibility requirements
- **Gate 4 — Result Guard**: Checks numerical consistency, statistical reporting, overclaim detection, and cross-validates results against methods
- **Gate 5 — Writing Guard**: Validates manuscript structure, cross-section consistency, and language quality
- **Logic Fallacy Chain**: A cross-cutting 5-layer reasoning verification module (formal logic, causal reasoning, statistical reasoning, argument structure, research-specific fallacies) that runs in parallel with all gates

Key architectural principles:
- **Subagent isolation**: The agent that generates content never evaluates its own output — all gates run as independent subagents in clean context
- **Parallel execution**: After pre-scan, all gates run simultaneously (3.4x speedup in FULL mode)
- **Three performance modes**: 🟢 QUICK (10% compute, 80% catch rate), 🟡 STANDARD, 🔴 FULL
- **Standardized issue schema**: All gates output unified JSON with evidence anchoring and confidence scores

## Skill structure

```
research-guardian/
├── references
│   ├── critique-synthesis.md
│   ├── experiment
│   │   ├── figures-tables.md
│   │   ├── math-symbol.md
│   │   ├── ml-experiment.md
│   │   ├── observational.md
│   │   ├── qualitative.md
│   │   └── rct.md
│   ├── experiment-checklist.md
│   ├── extensibility-guide.md
│   ├── hypothesis
│   │   ├── biomedical.md
│   │   ├── cs-ml.md
│   │   └── social-science.md
│   ├── hypothesis-validation.md
│   ├── ingestion
│   │   ├── metadata-validation.md
│   │   └── paper-parser.md
│   ├── issue-schema.md
│   ├── literature
│   │   ├── biomedical.md
│   │   ├── cs-ml.md
│   │   ├── gap-framing.md
│   │   └── social-science.md
│   ├── literature-verification.md
│   ├── logic
│   │   ├── layer1-formal.md
│   │   ├── layer2-causal.md
│   │   ├── layer3-statistical.md
│   │   ├── layer4-argument.md
│   │   └── layer5-research.md
│   ├── logic-fallacy-chain.md
│   ├── metrics/
│   ├── modes/
│   ├── parallel-execution.md
│   ├── performance-metrics.md
│   ├── quick-modes.md
│   ├── red-flag-synthesis.md
│   ├── result/
│   ├── result-integrity.md
│   ├── subagent/
│   ├── subagent-evaluation.md
│   ├── surpass/
│   ├── writing/
│   └── writing-verification.md
├── schemas
│   └── guardian.schema.json
├── scripts
│   └── runner.py
└── SKILL.md

15 directories, 63 files
```

## Protocol

This skill follows the [vercel-labs/skills](https://github.com/vercel-labs/skills) protocol.
Each push to `main` triggers a GitHub Action that packages the skill as a `.skill` file
and creates a release tagged with the commit SHA.

## License

MIT License
