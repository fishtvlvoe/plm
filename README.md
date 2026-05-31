# PLM — 個人數位分身萃取工具

[English Version](#english-version)

你只需要把你的個人筆記、工作習慣、CSV 資料丟進來，AI 會自動幫你整理出兩份東西：

- **`autobiography.md`**：你是什麼樣的人（6 個面向的自傳）
- **`digital-twin-guide.md`**：怎麼讓 AI 扮演你（可直接貼進 Claude、Codex 的設定檔）

---

## 怎麼開始用

### 安裝（只要做一次）

```bash
git clone https://github.com/fishtvlvoe/plm.git
cd plm
```

把你的個人資料路徑填進 `knowledge/data-sources.md`（照裡面的表格格式填）。

### 觸發

在支援 Skill 的 AI Agent（Claude Code、Claude Desktop）輸入以下任一：

| 你說的 | 發生什麼事 |
|--------|-----------|
| `/plm` | 啟動，AI 自動判斷首次或更新 |
| `啟動 PLM` | 同上 |
| `建立我的分身` | 強制首次建立 |
| `更新我的 PLM` | 把新資料合進既有分身 |
| `有新資料` | 同上 |

### AI 會怎麼做

1. 掃描你設定的資料路徑，列出哪些有找到、哪些找不到
2. 等你確認（或補充缺少的資料）
3. 萃取特質，每條標記信心等級：`⚙️` = 確定、`🧪` = 還在驗證
4. 產出兩份文件草稿，等你確認後存檔

### 更新（保持最新版）

```bash
cd plm
git pull origin main
```

---

## 這個 Skill 怎麼運作

採用 **SSC Gen-3（Super Skills Creator 世代 3）** 規範建構，把邏輯拆成四個獨立檔案：

| 檔案 | 用途 |
|------|------|
| `SKILL.md` | AI 的執行流程（它看這個跑） |
| `knowledge/data-sources.md` | 你的個人資料路徑設定 |
| `knowledge/extraction-framework.md` | 特質怎麼驗證、怎麼評分 |
| `TEMPLATES.md` | 輸出文件的格式規範 |

**信心標記說明：**

- `⚙️` **確信事實**：同一個特質在你不同面向的資料都出現過，而且具有預測性、不是每個人都這樣
- `🧪` **暫定假設**：目前只有一兩個地方提到，需要更多資料驗證

---

## 版本紀錄

見 [CHANGELOG.md](CHANGELOG.md)

---

## 授權

MIT License © 2025 fishtv

---

<a name="english-version"></a>

## English Version

Just drop your personal notes, habit files, and CSV exports into the config, and PLM will generate two documents:

- **`autobiography.md`** — who you are across 6 trait dimensions
- **`digital-twin-guide.md`** — ready-to-paste config for Claude, Codex, and other AI agents

### Install

```bash
git clone https://github.com/fishtvlvoe/plm.git
cd plm
```

Edit `knowledge/data-sources.md` with your personal file paths.

### Trigger

Send any of these to a compatible AI Agent:

| Input | Effect |
|-------|--------|
| `/plm` | Auto-detects first-run or update |
| `啟動 PLM` | Same as above |
| `建立我的分身` | Force first-run |
| `更新我的 PLM` | Merge new data into existing files |
| `有新資料` | Same as above |

### Update PLM Itself

```bash
cd plm
git pull origin main
```

### How It Works

Built on **SSC Gen-3 (Super Skills Creator Generation 3)** architecture, which separates instructions, data configs, and heuristics into distinct files. Each file can be updated independently without breaking the others.

**Confidence levels:**
- `⚙️` confirmed fact — appears across multiple life domains, predictive, and distinctive
- `🧪` working hypothesis — limited evidence, needs more data to confirm

### License

MIT License © 2025 fishtv
