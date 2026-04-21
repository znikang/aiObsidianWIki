---
title: Karpathy llm-wiki Schema
type: source
tags: [design, architecture, pattern, llm-wiki]
created: 2026-04-14
updated: 2026-04-14
sources: []
---
# LLM Wiki Pattern (by Karpathy)

此頁面記錄了 Andrej Karpathy 所提出的 LLM Wiki 核心設計模式。

## 核心理念
本模式強調 LLM 不僅僅是檢索 (RAG) 的工具，而是**知識的編寫者 (The Writer)**。

### 關鍵差異：檢索 (Retrieval) vs. 編寫 (Writing)
- **傳統 RAG**：在查詢時從原始文件中檢索碎片，每次都要重新推導，缺乏知識累積。
- **LLM Wiki 模式**：LLM 讀取新來源後，會主動**提取、整合並更新**既有的結構化文件（實體、概念、總結），使知識庫隨資料增加而變得日益豐富。

## 角色定義
- **LLM Agent**：負責主要的苦力活（摘要、建立連結、更新日誌、維護結構）。
- **人類 (User)**：負責提供來源、引導探索、提出問題。
- **Obsidian**：作為知識的 IDE，讓人類可以直觀地檢視、瀏覽連結與圖譜。

## 運作流程 (Operations)
當新資料進入時，LLM 應執行：
1. 讀取來源。
2. 與使用者討論重點。
3. 建立摘要頁面。
4. 更新相關的實體 (Entities) 與概念 (Concepts) 頁面。
5. 更新索引與日誌。
