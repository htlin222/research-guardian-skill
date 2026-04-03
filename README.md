# research-guardian

[![Build & Release Skill](https://github.com/htlin222/research-guardian-skill/actions/workflows/release.yml/badge.svg)](https://github.com/htlin222/research-guardian-skill/actions/workflows/release.yml)
[![GitHub Release](https://img.shields.io/github/v/release/htlin222/research-guardian-skill?include_prereleases&label=skill%20version)](https://github.com/htlin222/research-guardian-skill/releases/latest)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Skills Protocol](https://img.shields.io/badge/protocol-vercel--labs%2Fskills-blue)](https://github.com/vercel-labs/skills)
[![Compatible Agents](https://img.shields.io/badge/agents-40%2B-green)](https://github.com/vercel-labs/skills#supported-agents)

> AI research quality guardian system — automated multi-gate verification for AI-generated research outputs, preventing hallucinations, logic errors, citation fabrication, and novelty misjudgment.

## On Paradigms and Guardians

Thomas Kuhn taught us that science does not advance by steady accumulation but by rupture — that what we call "normal science" is puzzle-solving within an inherited framework, and that the framework itself is invisible until it breaks. The danger of AI-assisted research is not that it cannot generate hypotheses or draft manuscripts; it is that it does so fluently within whatever paradigm it has absorbed, never sensing the seams. An AI will not notice when its citations are phantoms, when its causal arrows run backward, when its "novel contribution" is a rediscovery dressed in new notation — because it has no crisis, no anomaly that refuses to fit. Research Guardian exists at precisely this juncture: it is the structured anomaly, the deliberate crisis. Each gate asks the question Kuhn said normal science suppresses — *is the framework itself sound?* — and it asks with the discipline of peer review, not the politeness of autocomplete. If paradigm shifts begin when trusted methods produce results that contradict trusted beliefs, then a guardian that forces every claim through independent, adversarial verification is not a brake on discovery. It is the condition for discovery that deserves the name.

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
