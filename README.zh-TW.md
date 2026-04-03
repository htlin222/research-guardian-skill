# research-guardian

[![Build & Release Skill](https://github.com/htlin222/research-guardian-skill/actions/workflows/release.yml/badge.svg)](https://github.com/htlin222/research-guardian-skill/actions/workflows/release.yml)
[![GitHub Release](https://img.shields.io/github/v/release/htlin222/research-guardian-skill?include_prereleases&label=skill%20version)](https://github.com/htlin222/research-guardian-skill/releases/latest)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Skills Protocol](https://img.shields.io/badge/protocol-vercel--labs%2Fskills-blue)](https://github.com/vercel-labs/skills)
[![Compatible Agents](https://img.shields.io/badge/agents-40%2B-green)](https://github.com/vercel-labs/skills#supported-agents)

> AI 研究品質防護系統——在 AI agent 執行研究任務時，自動進行多重驗證、事實查核、文獻交叉比對、實驗設計檢查，防止幻覺、邏輯錯誤、引用錯誤、與 novelty 誤判。

## 關於典範與守門人

Thomas Kuhn 告訴我們，科學不是穩步積累的過程，而是斷裂式的躍遷——他稱之為「常態科學」的，不過是在既有框架內解謎，而框架本身在崩塌之前是隱形的。AI 輔助研究的危險不在於它無法生成假說或撰寫稿件；而在於它在所吸收的任何典範內都流暢自如，卻永遠感知不到接縫。AI 不會注意到它的引用是幻覺、它的因果箭頭指反了、它的「新穎貢獻」只是換了符號的舊發現——因為它沒有危機，沒有拒絕被收編的異例。Research Guardian 恰恰存在於這個接合處：它是結構化的異例，是刻意製造的危機。每一道 Gate 都在追問 Kuhn 說常態科學所壓抑的那個問題——*框架本身站得住腳嗎？*——而且它以 peer review 的紀律來追問，而非自動補全的禮貌。如果典範轉移始於可信賴的方法產出了與可信賴的信念相矛盾的結果，那麼一個迫使每個主張通過獨立、對抗性驗證的守門人，就不是對發現的阻礙。它是讓發現配得上這個名字的前提條件。

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
