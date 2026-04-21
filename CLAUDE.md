# CLAUDE.md — Wiki Schema

這是 LLM Wiki 的 schema 設定檔。每次新對話開始時，請先讀取此檔案以了解 wiki 的結構與工作流程。

---

## 目錄結構

```
vault/
├── CLAUDE.md          ← 本檔案，schema 設定
├── wiki/              ← LLM 負責維護的知識庫（你寫，我不改）
│   ├── index.md       ← 所有頁面的目錄
│   ├── log.md         ← 操作記錄（只增不減）
│   ├── concepts/      ← 概念頁面
│   ├── entities/      ← 實體頁面（人物、組織、產品等）
│   ├── sources/       ← 來源摘要
│   └── synthesis/      ← 綜合分析、比較、洞察
│   └── daly           ← 每日總結  
└── raw/               ← 原始資料（不修改）
    └── assets/        ← 圖片等附件
```

---

## 頁面格式

每個 wiki 頁面的 YAML frontmatter 格式：

```yaml
---
title: 頁上標題
type: concept | entity | source | synthesis
tags: [tag1, tag2]
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: [來源頁面連結]
---
```

---

## 工作流程

### Ingest（消化新來源）
1. 使用者把新資料丟進 `raw/` 或提供連結
2. 我閱讀來源，與使用者討論重點
3. 在 `wiki/sources/` 建立摘要頁面
4. 更新相關的 `wiki/concepts/` 和 `wiki/entities/` 頁面
5. 在 `wiki/index.md` 新增條目
6. 在 `wiki/log.md` 新增記錄

### Query（查詢）
1. 我先讀取 `wiki/index.md` 找相關頁面
2. 讀取相關頁面後綜合回答
3. 有價值的答案可以存為 `wiki/synthesis/` 頁面

### Lint（健康檢查）
定期執行，檢查：
- 孤立頁面（沒有其他頁面連結到它）
- 過時的資訊
- 矛盾的內容
- 缺少頁面的重要概念

---

## 慣例

- 頁面間連結使用 Obsidian wikilink 格式：`[[頁面名稱]]`
- 來源引用格式：`[[sources/來源名稱]]`
- 中文為主要語言，技術術語可保留英文


---

## 工作日誌補充規則（2026-04-14 新增）

### 工作進行中 — 即時寫入原則

每完成一個具體動作後，**立即更新** `wiki/worklog.md`，不要等到對話結束才補寫。

**以下動作完成後，必須立即寫 寫入：**
- 建立新檔案
- 修改現有檔案
- 刪除檔案
- 執行搜尋並找到有價值的結果
- 完成一個子任務
- 遇到錯誤或無法完成某件事

**進度備註格式（任務項目下方加時間戳記）：**
```
- [x] 建立 wiki/sources/xxx.md
  - ✅ HH:MM 完成
- [ ] 整理 raw/yyy.pdf
  - 🔄 HH:MM 進行中：已提取文字，正在整理格式
  - ❌ HH:MM 失敗：PDF 為掃描檔，無法提取文字，建議改用 OCR 工具
```

**錯誤記錄規則：**
遇到無法完成的任務時，必須記錄：失敗原因、嘗試過的方法、建議的替代方案。

**結果摘要規則：**
每個大任務完成後，主動寫入「結果摘要」，不等使用者說結束：
```
### 結果摘要
完成時間：HH:MM / 完成項目：N 個 / 未完成：N 個 / 備註：...
```
