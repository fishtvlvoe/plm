# Changelog

所有版本的變更紀錄。格式遵循 [Keep a Changelog](https://keepachangelog.com/zh-TW/1.0.0/)，版本號遵循 [Semantic Versioning](https://semver.org/spec/v2.0.0.html)。

---

## [0.0.2] — 2026-05-31

### 新增
- templates/ 目錄：將 TEMPLATES.md 拆分為獨立目錄
  - `templates/format.md`：格式規範（原 TEMPLATES.md）
  - `templates/example-autobiography.md`：真實自傳範例（40 個特質，⚙️ 32 / 🧪 8）
  - `templates/example-digital-twin-guide.md`：真實數位分身指南範例
- knowledge/interview-questions.md：25 題採訪問題集，分 5 主題群，含使用說明與追問原則

### 變更
- SKILL.md：路徑引用從 `TEMPLATES.md` 更新為 `templates/format.md`；Phase 1 停止點加入採訪問題觸發邏輯
- example-autobiography.md：從哲學底層文件（BGO 框架、種子原則等）補充 12 個深層特質

### 資料來源
首次以真實個人資料執行完整萃取流程，成功讀取 9 個來源（CSV + Markdown），
整合哲學思維框架文件後達 40 個特質。

---

## [0.0.1] — 2026-05-31

### 新增
- SKILL.md：PLM 首個 SSC Gen-3 合規版本，含 GATE、強制停止點、品質檢查、完成條件
- knowledge/data-sources.md：21 個個人資料來源路徑設定
- knowledge/extraction-framework.md：三向驗證框架（跨域複現、生成力、排他性）
- TEMPLATES.md：autobiography.md 與 digital-twin-guide.md 標準輸出格式
- LICENSE：MIT 授權
- README.md：繁體中文 + 英文雙語說明，白話安裝與使用指南
- CHANGELOG.md：本文件

### 輸出產物規格
- autobiography.md：6 區塊自傳（Personality / Thinking / Timeline / Expertise / Work Style / Boundary）
- digital-twin-guide.md：5 模組數位分身指南（SOUL / AI Config / Memory Seeds / Expression DNA / Behavior Boundary）
