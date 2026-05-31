# PLM (Personal Lab Manager) Skill — 數位分身萃取工具

[English Version Below](#english-version)

本專案為 `plm` Skill 的核心配置與參考庫。PLM 是一個專為「個人特質萃取」與「數位分身指南構建」設計的宣告式 Skill（Declarative Skill），採用 **SSC (Super Skills Creator) 世代 3** 規範進行開發。

---

## 繁體中文說明

### 1. Skills 的建立模式 (SSC Gen-3)
本 Skill 遵循 SSC 世代 3 的架構合約建立，將工作流、資料來源與提取邏輯嚴格解耦：
- **`SKILL.md` (主體流程)**：定義了 Phase 0 至 Phase 5 的階段式工作流、激活觸發詞、以及增量更新（Update Mode）的路由機制。
- **`knowledge/data-sources.md` (資料路徑)**：配置用戶個人資料的實體檔案路徑，定義了模糊欄位比對與容錯加載機制。
- **`references/extraction-framework.md` (提取框架)**：定義了個人特質提取的三向驗證邏輯，用於自動標記 `⚙️ 確信事實` 或 `🧪 暫定假設`。
- **`references/output-templates.md` (輸出模板)**：規範了輸出產物 `autobiography.md` 與 `digital-twin-guide.md` 的標準格式。

### 2. 使用方式
PLM 支援兩種執行模式，會根據環境狀態自動路由：
- **首次運行模式 (First-run)**：若本地未檢測到自傳與指南，AI 會載入 `knowledge/data-sources.md` 中列出的所有個人 CSV 與 Markdown 檔案，自動完成首次提取與檔案寫入。
- **增量更新模式 (Update-mode)**：若已存在輸出檔案，當用戶輸入新資料或提及「有新資料」時，AI 會與現有特質進行語意比對。若新資料與既有事實衝突，將降級為 `🧪` 並加上衝突備註，最後在 Changelog 中 prepend 變更記錄。

### 3. 如何使用這項工具
#### 步驟 1：配置個人資料來源
將你的個人說明書、MBTI、工作習慣、商業槓桿等 CSV 或 Markdown 檔案路徑填入 `knowledge/data-sources.md`。
*例如：*
```markdown
| Path | Format | Type |
|---|---|---|
| `/path/to/工作習慣.csv` | csv | work-style |
```

#### 步驟 2：觸發 AI 執行
在支援該 Skill 的 AI Agent 中，輸入以下任一觸發詞啟用：
- `/plm`
- `啟動 PLM`
- `建立我的分身`
- `更新我的 PLM`
- `有新資料`

#### 步驟 3：AI 自動運行與萃取
AI 會接管並依照 Phase 0 ~ 5 的步驟執行：
1. **加載資料**：讀取配置的 21 個資料來源，處理 fuzzy column matching。
2. **三向驗證**：對特質進行「跨域複現 (Cross-domain replication)」、「生成力 (Generativity)」與「排他性 (Exclusivity)」驗證。
3. **計算確信度**：符合驗證或累積 3+ 次獨立證據者標記為 `⚙️`，其餘標記為 `🧪`。
4. **輸出產物**：將生成的自傳與分身指南自動存檔。

### 4. 如何協助用戶操作與具體步驟
當用戶與 AI 對話並啟用 PLM 後，AI 將扮演 **PLM 執行器**，引導用戶完成以下步驟：
1. **檢索與診斷**：主動掃描 `data-sources.md` 列出的路徑，並列出 `Successfully loaded` 與 `not found` 的檔案清單。
2. **主動引導補齊**：若核心區塊缺乏數據，AI 會主動對話提問。例如：「*我發現你缺少商業槓桿的 CSV 檔案，能否請你告訴我，你目前在商業上可以用來交換的資源有哪些？*」
3. **生成自傳 (`autobiography.md`)**：
   - 提取並輸出以下 6 大區塊：Personality Traits, Thinking Frameworks, Life Timeline & Key Decisions, Expertise Map, Work Style, Boundary Map。
4. **生成數位分身指南 (`digital-twin-guide.md`)**：
   - 輸出 5 大模組：SOUL.md 模板、AI 設定檔（包含 CLAUDE.md 與 AGENTS.md 格式）、記憶種子（core-narrative / expertise-map）、表達 DNA（語調與節奏）、行為邊界。
5. **增量維護**：在用戶日後有新經歷、想法或設定變更時，接收輸入並自動更新兩份檔案的 Changelog。

---

<a name="english-version"></a>

## English Instructions

### 1. Skill Creation Paradigm (SSC Gen-3)
This skill is developed using the **Super Skills Creator (SSC) Gen-3** specification. It strictly decouples instructions, data inputs, and heuristics into distinct modules:
- **`SKILL.md` (Workflow Engine)**: Coordinates the phase-based logic (Phase 0 to Phase 5), handles triggers, and routes requests to either first-run or update execution.
- **`knowledge/data-sources.md` (Source Map)**: Catalogs user data files, columns mappings, and loading mechanisms.
- **`references/extraction-framework.md` (Verification Logic)**: Implements the "three-validation check" to label traits as either `⚙️ confirmed fact` or `🧪 hypothesis`.
- **`references/output-templates.md` (Markdown Schema)**: Establishes strict schemas for `autobiography.md` and `digital-twin-guide.md`.

### 2. Usage & Activation
The skill supports two primary running states:
- **First-run Mode**: Triggered when no autobiography files exist. The AI loads all local files configured in `knowledge/data-sources.md` to bootstrap the model.
- **Update Mode**: Triggered when existing files are found and new materials are provided. The AI merges incoming traits with past records, processes semantic contradictions, and logs modifications in the Changelog.

### 3. Step-by-Step Guide to Using PLM
#### Step 1: Configure Your Data Paths
Add paths of your personal manuals, CSV exports, or Markdown logs into the table in `knowledge/data-sources.md`.

#### Step 2: Trigger the Skill
Send one of the following prompts to your AI Agent:
- `/plm`
- `啟動 PLM` (Activate PLM)
- `建立我的分身` (Build My Twin)
- `更新我的 PLM` (Update My PLM)
- `有新資料` (New Data Available)

#### Step 3: Automated Processing
The AI will systematically process through:
1. **Source Loading**: Parsing Markdown and CSVs using column fuzzy matching.
2. **Three-Validation Verification**: Testing traits against *Cross-domain replication*, *Generativity*, and *Exclusivity*.
3. **Confidence Level Assignment**: Tagging proven traits with `⚙️` and unproven theories with `🧪`.

### 4. How the AI Assists the User
When the PLM Skill is triggered, the AI leads the user through:
1. **Diagnostic Verification**: Identifying which files loaded successfully and listing missing sources.
2. **Context Gap-Filling**: Interviewing the user if critical modules lack data (e.g., "I notice that your Work Habits CSV is empty. Can you tell me your preferred meeting slots?").
3. **Creating the Autobiography (`autobiography.md`)**: Writing a comprehensive 6-section character model prefixed with `⚙️` or `🧪`.
4. **Creating the Digital Twin Guide (`digital-twin-guide.md`)**: Constructing the 5-module guide containing ready-to-use `SOUL.md`, `CLAUDE.md`, and `AGENTS.md` templates.
5. **Long-Term Handoff**: Archiving files to the user's local directory and managing incremental updates on user demand.
