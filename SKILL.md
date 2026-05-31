---
name: plm
description: "個人特質萃取與數位分身指南生成。觸發詞：/plm、啟動 PLM、建立我的分身、更新我的 PLM、有新資料"
disable-model-invocation: true
user-invocable: true
---

# PLM — 個人數位分身萃取

## GATE：強制對焦（不可跳過）

收到任務後，第一步：
1. 複述「我理解你要 ___（首次建立分身 / 更新已有分身）」
2. 問「方向對嗎？」→ 用戶說 OK 才往下

---

## 流程

### 步驟 0：模式路由

觸發詞：`/plm` / `啟動 PLM` / `建立我的分身` / `更新我的 PLM` / `有新資料`

Read knowledge/data-sources.md 取得資料路徑清單。

路由規則：
- 輸入含「更新」或「有新資料」且 autobiography.md / digital-twin-guide.md 已存在 → 進入**更新模式**
- 其餘 → 進入**首次建立**

### 步驟 1：載入資料來源

依 knowledge/data-sources.md 逐一嘗試讀取每個來源：
- 成功：載入內容
- 失敗：記錄 `not found: <path>`，繼續不中斷

> **強制停止點：列出「已載入 / 找不到」清單，等用戶確認（或補充資料）後才繼續。**

### 步驟 2：特質萃取與信心評分

Read knowledge/extraction-framework.md 執行三向驗證（跨域複現、生成力、排他性）。

標記規則：
- 通過全部三驗證 → `⚙️` 確信事實
- 有任一失敗 → `🧪` 暫定假設
- 累積 3+ 獨立證據且三驗證全過 → `🧪` 升級為 `⚙️`，記錄升級日期

去重規則：同根名檔案（如 `trait.csv` 與 `trait_all.csv`）視為同一來源家族，不重複計算證據數。

### 步驟 3：輸出 autobiography.md

Read templates/format.md 套用自傳模板，輸出 6 大區塊：
Personality Traits、Thinking Frameworks、Life Timeline & Key Decisions、Expertise Map、Work Style、Boundary Map

每條陳述必須標 `⚙️` 或 `🧪`；每區塊末尾加 `Sources:` 引用來源。
無資料時輸出：`Data not available — run update mode with additional sources to fill this section`

### 步驟 4：輸出 digital-twin-guide.md

Read templates/format.md 套用數位分身模板，輸出 5 模組：
Module 1: SOUL.md 模板、Module 2: AI 設定（含 CLAUDE.md + AGENTS.md 格式）、Module 3: 記憶種子、Module 4: 表達 DNA、Module 5: 行為邊界

> **強制停止點：兩份文件草稿產出後，等用戶確認無誤才存檔。**

### 步驟 5：品質檢查（必須執行）

| 項目 | 標準 |
|------|------|
| 結構完整 | 6 區塊（自傳）+ 5 模組（分身指南）全部填寫 |
| 信心標記 | 每條陳述都有 `⚙️` 或 `🧪` |
| 來源引用 | 每區塊有 `Sources:` |
| 無矛盾遺漏 | 矛盾事實已標注，未靜默忽略 |

### 步驟 6：摘要輸出

格式：`提取 <total> 個特質：<confirmed> ⚙️ 確信，<hypothesis> 🧪 假設 → autobiography.md, digital-twin-guide.md`

---

## 更新模式（update-mode）

觸發條件：已有輸出檔 + 新資料輸入

合併規則：
1. 保留所有既有 `⚙️`（除非新資料明確矛盾）
2. 矛盾 → 降級為 `🧪`，標注 `Contradicted by: <source>, <YYYY-MM-DD>`
3. 新特質直接加入
4. 兩份輸出檔各自 prepend changelog 條目：`### <YYYY-MM-DD>：<N> 個特質新增，<M> 個修改`，不得重複 `## Changelog` 標題

## PLM Skill 本身的更新

若 PLM Skill 有新版本發布，執行以下步驟讓本機安裝保持最新：

```bash
# 進入你的 PLM 安裝目錄
cd /path/to/plm

# 拉取最新版本
git pull origin main
```

更新後重啟 AI Agent，新版 SKILL.md 即生效。

---

## 完成條件

- [ ] GATE 已通過，模式已確認
- [ ] 資料載入清單已給用戶確認
- [ ] 兩份輸出草稿已給用戶確認
- [ ] 品質檢查全部通過
- [ ] 摘要已輸出

---

## 安全與健壯性規則

- 拒絕不支援的來源副檔名（非 .md / .csv）
- 空值或零值不算有效證據
- 來源解析失敗 → 輸出明確錯誤訊息並繼續其餘來源
- 矛盾事件必須標注，禁止靜默忽略
