---
name: plm
description: Personalization Lifecycle Modeling skill for extracting traits and generating autobiography + digital twin guides.
user-invocable: true
triggers:
  - /plm
  - 啟動 PLM
  - 建立我的分身
  - 更新我的 PLM
  - 有新資料
---

# PLM Skill

## Compatible runtimes
- Claude Code / Claude Desktop Skills
- Codex AGENTS.md-compatible skill runners

## Skill structure contract
- `SKILL.md` (this file)
- `references/extraction-framework.md`
- `references/output-templates.md`
- `knowledge/data-sources.md`

## Phase 0 — Activation and mode routing

### Activation
Activate when user input includes one of:
- `/plm`
- `啟動 PLM`
- `建立我的分身`
- `更新我的 PLM`
- `有新資料`

### Detect output files
- `autobiography.md`
- `digital-twin-guide.md`

### Routing rules
1. If user input contains `更新我的 PLM` or `有新資料`:
   - If either output file exists: run **update-mode**
   - If none exists: fallback to **first-run**
2. If input is `/plm`, `啟動 PLM`, or `建立我的分身`:
   - If files do not exist: run **first-run**
   - If files exist and message contains new material (inline text or attached source path): run **update-mode**
   - Otherwise default to **first-run**

## Phase 1 — Source loading (first-run)
1. Read `knowledge/data-sources.md`.
2. Iterate sources one by one.
3. For each source:
   - If exists and extension is `.md` or `.csv`: load content.
   - If missing: append to `not_found_sources` and log line exactly as:
     - `not found: <path>`
4. Continue processing even when files are missing.

## Phase 2 — Extraction and confidence scoring
1. Use `references/extraction-framework.md`:
   - Three validations: cross-domain replication, generativity, exclusivity
   - Confidence tags:
     - `⚙️` = passes all validations
     - `🧪` = fails one or more validations
2. Apply source-family dedup before evidence counting (avoid `.csv` + `_all.csv` double count).
3. Promotion rule:
   - A `🧪` item can be upgraded to `⚙️` only when evidence count reaches **3+ unique evidence events**.

## Phase 3 — Generate `autobiography.md`
1. Use `references/output-templates.md` autobiography template.
2. Must output exactly 6 sections:
   - Personality Traits
   - Thinking Frameworks
   - Life Timeline & Key Decisions
   - Expertise Map
   - Work Style
   - Boundary Map
3. Every statement must be prefixed `⚙️` or `🧪`.
4. Every section must include a `Sources:` line.
5. If a section has no data, print exactly:
   - `Data not available — run update mode with additional sources to fill this section`

## Phase 4 — Generate `digital-twin-guide.md`
1. Use `references/output-templates.md` digital twin template.
2. Must output 5 modules:
   - Module 1: SOUL.md Template
   - Module 2: AI Configuration
   - Module 3: Memory Seed Files
   - Module 4: Expression DNA
   - Module 5: Behavior Boundary
3. Module 2 must include both:
   - `### For Claude (CLAUDE.md)`
   - `### For Codex (AGENTS.md)`

## Phase 5 — Summary output
Print:
- Total traits extracted
- `⚙️` count
- `🧪` count
- Output paths

Format:
`Extracted <total> traits: <confirmed> ⚙️ confirmed, <hypothesis> 🧪 hypotheses → autobiography.md, digital-twin-guide.md`

## Update mode implementation

### Inputs
- Existing `autobiography.md`
- Existing `digital-twin-guide.md`
- Newly loaded sources from Phase 1

### Merge contract
1. Parse existing traits with tag and section.
2. Canonical identity:
   - `trait_id = normalize(section + statement)`
3. Keep all prior `⚙️` by default.
4. If new evidence explicitly contradicts prior `⚙️`:
   - Downgrade to `🧪`
   - Annotate inline:
     - `Contradicted by: <source>, <YYYY-MM-DD>`
5. Add newly extracted traits.
6. Do not overwrite unchanged prior traits.

### Changelog prepend
For both output files:
1. Ensure there is a single top-level `## Changelog`.
2. Prepend one new entry under it:
   - `### <YYYY-MM-DD>: <N> traits added, <M> modified`
3. Never duplicate `## Changelog` header.

## Security and robustness checks (audit discipline)
- Reject unsupported source extensions.
- Treat empty/zero values as invalid evidence, not as confirmed.
- If source parsing fails, emit explicit parse error per file and continue with remaining files.
- Never silently swallow contradiction events; always annotate output.
