# PLM Extraction Framework

## Objective
Extract traits from heterogeneous personal sources and assign confidence tags:
- `⚙️` confirmed fact
- `🧪` working hypothesis

## Three-validation rules

A trait is `⚙️` only when it passes all checks:

1. **Cross-domain replication**
   - The trait appears in at least two distinct domains (for example work + life, or business + collaboration).
2. **Generativity**
   - The trait can predict future behavior or decision patterns.
3. **Exclusivity**
   - The trait is personally distinctive, not generic advice that applies to almost everyone.

If any check fails, tag as `🧪`.

## Confidence tagging format
- `⚙️ <trait statement>`
- `🧪 <trait statement>`

Each extracted trait record should include:
- `section` (Personality Traits / Thinking Frameworks / Life Timeline & Key Decisions / Expertise Map / Work Style / Boundary Map)
- `tag` (`⚙️` or `🧪`)
- `sources` (list of files)
- `evidence_count` (unique evidence events)
- `first_seen` (`YYYY-MM-DD`)
- `notes` (optional contradiction or uncertainty)

## Evidence normalization and dedup

To prevent duplicate evidence inflation:

1. Create source family:
   - Remove `_all` suffix and extension from filename.
   - Example: `工作習慣 ...csv` and `工作習慣 ..._all.csv` are one family.
2. Keep one evidence event per family + normalized statement pair.
3. Evidence count uses **unique events**, not total matched rows.

## Hypothesis promotion threshold

A `🧪` hypothesis can be promoted to `⚙️` only when:
- it accumulates **3+ unique evidence events**, and
- all three-validation checks pass.

Promotion should append note:
- `Promoted on: <YYYY-MM-DD>`

## Contradiction handling (update mode)

When new data contradicts an existing `⚙️` trait:
1. Downgrade to `🧪`.
2. Keep original statement (do not delete history).
3. Add annotation:
   - `Contradicted by: <source file>, <YYYY-MM-DD>`
4. Increase modified count for changelog.

## Extraction workflow
1. Parse each source into candidate statements.
2. Normalize statements (trim, normalize punctuation, collapse spaces).
3. Assign section by semantic mapping:
   - behavior/process -> Work Style
   - principles/decision logic -> Thinking Frameworks
   - timeline events -> Life Timeline & Key Decisions
   - skills/domain competence -> Expertise Map
   - limits/non-negotiables -> Boundary Map
   - identity/preferences -> Personality Traits
4. Run three-validation.
5. Apply tag and store evidence metadata.
