# research-guardian

[![Build & Release Skill](https://github.com/htlin222/research-guardian-skill/actions/workflows/release.yml/badge.svg)](https://github.com/htlin222/research-guardian-skill/actions/workflows/release.yml)
[![GitHub Release](https://img.shields.io/github/v/release/htlin222/research-guardian-skill?include_prereleases&label=skill%20version)](https://github.com/htlin222/research-guardian-skill/releases/latest)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Skills Protocol](https://img.shields.io/badge/protocol-vercel--labs%2Fskills-blue)](https://github.com/vercel-labs/skills)
[![Compatible Agents](https://img.shields.io/badge/agents-40%2B-green)](https://github.com/vercel-labs/skills#supported-agents)

> AI 研究品質防護系統——在 AI agent 執行研究任務時，自動進行多重驗證、事實查核、文獻交叉比對、實驗設計檢查，防止幻覺、邏輯錯誤、引用錯誤、與 novelty 誤判。

## 關於可否證性與守門人

> *「一個科學陳述若談論現實，就必須是可否證的；若它不可否證，它就沒有在談論現實。」*
> — Karl Popper

Popper 在科學哲學中畫下了最鋒利的一刀：一個原則上無法被證偽的主張，根本不是科學主張。它可能文辭優美、內部自洽、甚至有用——但它沒有在談論現實。AI 生成研究的麻煩在於，它產出的陳述*看起來*可以被否證，卻從未經歷過任何真正的否證嘗試。引用看似可查核，但可能根本不存在。統計看似嚴謹，但可能建立在無人審核的設計缺陷之上。結論看似謙遜，但可能恰好以最令人信服的幅度超出了證據所能支撐的範圍。用 Popper 的話來說，這些是穿著科學制服的偽科學產出。Research Guardian 本質上是一台否證引擎。每一道 Gate 都是一次結構化的嘗試，試圖*打破*它所收到的主張——找出缺失的對照組、捏造的引用、指反方向的因果箭頭、藏著千次比較的 p 值。它不問「這寫得好嗎？」它問「這經得起一次誠實的反駁嘗試嗎？」通過全部五道 Gate 和邏輯鏈的內容，並沒有被*驗證*——Popper 會提醒我們，驗證不是科學的運作方式——但它承受住了一次嚴肅的、多角度的反駁嘗試。而這是任何科學陳述所能擁有的唯一保證。

## 安裝

```bash
npx skills add htlin222/research-guardian-skill
npx skills add -g htlin222/research-guardian-skill        # 全域安裝
npx skills add htlin222/research-guardian-skill --agent claude-code  # 指定 agent
```

## 功能說明

Research Guardian 是一套 AI 研究品質保障系統，在 AI agent 執行研究任務時自動進行多層驗證。它作為 AI agent pipeline 中的品質閘門，包含 5 道獨立驗證 Gate 與一條橫切的邏輯謬誤鏈：

- **Gate 1 — 假設防護**：驗證研究假設是否與既有文獻一致、檢查 novelty 宣稱、偵測循環論證
- **Gate 2 — 文獻防護**：驗證引用是否真實存在、偵測幻覺引用、檢查引用倫理違規與掠奪性期刊
- **Gate 3 — 實驗防護**：審核實驗設計、統計方法、統計檢定力分析、可重現性要求
- **Gate 4 — 結果防護**：檢查數值一致性、統計報告、過度宣稱偵測、結果與方法的交叉驗證
- **Gate 5 — 寫作防護**：驗證稿件結構、跨章節一致性、語言品質
- **邏輯謬誤鏈**：橫切 5 層推理驗證模組（形式邏輯、因果推理、統計推理、論證結構、研究特有謬誤），與所有 Gate 平行運行

核心架構原則：
- **Subagent 隔離**：產生內容的 agent 永遠不能評估自己的輸出——所有 Gate 在乾淨 context 中由獨立 subagent 執行
- **平行執行**：Pre-scan 之後所有 Gate 同時啟動（FULL 模式 3.4 倍加速）
- **三種效能模式**：🟢 QUICK（10% 算力，80% 攔截率）、🟡 STANDARD、🔴 FULL
- **標準化 Issue Schema**：所有 Gate 輸出統一 JSON 格式，含 evidence anchoring 與 confidence 分數

## 技能結構

```
research-guardian/
├── references
│   ├── critique-synthesis.md
│   ├── experiment/
│   ├── experiment-checklist.md
│   ├── extensibility-guide.md
│   ├── hypothesis/
│   ├── hypothesis-validation.md
│   ├── ingestion/
│   ├── issue-schema.md
│   ├── literature/
│   ├── literature-verification.md
│   ├── logic/
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

## 協議

本技能遵循 [vercel-labs/skills](https://github.com/vercel-labs/skills) 協議。
每次推送至 `main` 分支都會觸發 GitHub Action，將技能打包為 `.skill` 檔案，
並以 commit SHA 建立版本標籤。

## 授權

MIT License
