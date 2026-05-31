# PLM Data Sources

## Reading rules
1. Read sources in listed order.
2. If file exists, parse by extension:
   - `.md` as Markdown text
   - `.csv` as table rows with header matching
3. If file does not exist, record:
   - `not found: <path>`
4. Continue; missing files must not stop the workflow.

## Source taxonomy
- `personality`
- `work-style`
- `expertise`
- `values`
- `boundary`

## Canonical sources (Personalization workspace)

| Path | Format | Type |
|---|---|---|
| `/Users/fishtv/Development/Personalization/老魚使用說明書 f92c23a8e7334794ad4590782ada65ce.md` | md | boundary, work-style, values |
| `/Users/fishtv/Development/Personalization/個人基本資訊 a583ee1b1f3d499c862f7b0ffeb9882a.csv` | csv | personality |
| `/Users/fishtv/Development/Personalization/操作系统 b2b1d398c2af4f5d9b6695ae568bca8c.csv` | csv | work-style |
| `/Users/fishtv/Development/Personalization/個人喜好 63ced51b3ab645eabbdeb3df2e194144.csv` | csv | personality, values |
| `/Users/fishtv/Development/Personalization/工作習慣 a6d65c9d16f54441b8c9ccf67f5921ee.csv` | csv | work-style |
| `/Users/fishtv/Development/Personalization/相處方式 96325fdf5904401090a5adc181a96181.csv` | csv | work-style, boundary |
| `/Users/fishtv/Development/Personalization/我如何在工作上使用自己 1ce49bf6813f4c86905f9f67777826e3.csv` | csv | expertise, work-style |
| `/Users/fishtv/Development/Personalization/我如何長期保持有優勢的自己 68372e1ea5a644c390e329e68c840b47.csv` | csv | values, work-style |
| `/Users/fishtv/Development/Personalization/Fish 十年以上的事情與經驗 7ac47ffff7d84b61b408697bcf63a9fa.csv` | csv | expertise, life-timeline |
| `/Users/fishtv/Development/Personalization/我在商業可以交換的槓桿 12a91da1e646800c8632eaa0f1509a14.csv` | csv | expertise |
| `/Users/fishtv/Development/Personalization/AIU/SOUL.md` | md | personality, values |
| `/Users/fishtv/Development/Personalization/AIU/aiu-core/memory/core-narrative.md` | md | personality, values |
| `/Users/fishtv/Development/Personalization/AIU/aiu-core/memory/expertise-map.md` | md | expertise |
| `/Users/fishtv/Development/Personalization/AIU/aiu-core/memory/active-patterns.md` | md | work-style |
| `/Users/fishtv/Development/Personalization/AIU/aiu-core/memory/response-strategies.md` | md | work-style |
| `/Users/fishtv/Development/Personalization/AIU/aiu-core/memory/strategic-diagnosis.md` | md | expertise |
| `/Users/fishtv/Development/Personalization/AIU/aiu-core/memory/working-hypotheses.md` | md | personality |
| `/Users/fishtv/Development/Personalization/AIU/aiu-core/memory/proactive-triggers.md` | md | values, boundary |
| `/Users/fishtv/Development/Personalization/AIU/aiu-core/memory/session-context.md` | md | work-style |
| `/Users/fishtv/Development/Personalization/AIU/aiu-core/memory/active-threads.md` | md | expertise |
| `/Users/fishtv/Development/Personalization/AIU/aiu-core/memory/retrieval-manifest.md` | md | work-style |

## Optional fallback sources
- Same basename with `_all.csv` suffix can be read if canonical `.csv` is missing.
- If canonical and `_all.csv` both exist, prefer canonical `.csv` and do not double-read.

## CSV fuzzy column matching

When headers vary, map by token similarity and Traditional Chinese synonyms:

| Target field | Fuzzy keywords (any match) |
|---|---|
| `trait_statement` | 特質, 風格, 傾向, 描述, 說明, 行為 |
| `evidence` | 例子, 證據, 案例, 觀察, 情境 |
| `domain` | 場景, 領域, 工作, 生活, 商業 |
| `value_signal` | 價值觀, 原則, 判斷標準, 信念 |
| `boundary_signal` | 禁區, 地雷, 不接受, 反感, 邊界 |
| `date` | 日期, 時間, year, created_at |
| `source_note` | 備註, note, 註記 |

If no fuzzy match exists for a target field, keep the row as unstructured evidence and mark it `partial-parse`.
