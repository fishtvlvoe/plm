# PLM Output Templates

## Autobiography template (`autobiography.md`)

```text
## Changelog
### YYYY-MM-DD: N traits added, M modified

# Autobiography

## Personality Traits
- ⚙️ ...
- 🧪 ...
Sources: file-a.md, file-b.csv

## Thinking Frameworks
- ⚙️ ...
- 🧪 ...
Sources: ...

## Life Timeline & Key Decisions
- ⚙️ ...
- 🧪 ...
Sources: ...

## Expertise Map
- ⚙️ ...
- 🧪 ...
Sources: ...

## Work Style
- ⚙️ ...
- 🧪 ...
Sources: ...

## Boundary Map
- ⚙️ ...
- 🧪 ...
Sources: ...
```

### Rules
1. Must include exactly the six sections above.
2. Every statement must start with `⚙️` or `🧪`.
3. Every section must include one `Sources:` line.
4. If a section has no extracted traits, use:
   - `Data not available — run update mode with additional sources to fill this section`

## Digital twin guide template (`digital-twin-guide.md`)

```md
## Changelog
### YYYY-MM-DD: N traits added, M modified

# Digital Twin Guide

## Module 1: SOUL.md Template
### Core Truths
1. ...
2. ...
3. ...
4. ...
5. ...

### Operational Principles
- ...

### Continuity
- Keep identity stable across sessions.
- Preserve confirmed facts (`⚙️`) unless explicitly contradicted.

## Module 2: AI Configuration
### For Claude (CLAUDE.md)
```text
# Identity
- ...
# Behavior
- ...
# Boundaries
- ...
```

### For Codex (AGENTS.md)
```text
# Identity
- ...
# Behavior
- ...
# Boundaries
- ...
```

## Module 3: Memory Seed Files
### core-narrative.md
- ⚙️ ... [first seen: YYYY-MM-DD]
- 🧪 ... [first seen: YYYY-MM-DD]

### expertise-map.md
- ⚙️ ...
- 🧪 ...

## Module 4: Expression DNA
- Tone rules: ...
- Vocabulary rules: ...
- Response rhythm: ...

## Module 5: Behavior Boundary
- Hard boundaries (must not cross): ...
- Soft boundaries (ask before acting): ...
```

### Rules
1. Must include all five modules with exact module headings.
2. Module 1 SOUL.md must follow AIU structure:
   - Core Truths (5-10 items)
   - Operational Principles
   - Continuity
3. Module 2 must include both CLAUDE.md and AGENTS.md blocks with equivalent behavior rules.
4. Module 3 must include `core-narrative.md` and `expertise-map.md`, prefilling `⚙️` facts and keeping `🧪` as hypotheses.

## Output schema checklist

Before finalizing outputs:
- [ ] autobiography has 6 sections
- [ ] every claim has `⚙️` or `🧪`
- [ ] every section has `Sources:`
- [ ] digital twin guide has 5 modules
- [ ] SOUL module has Core Truths + Operational Principles + Continuity
- [ ] AI Configuration has both CLAUDE.md and AGENTS.md
- [ ] memory seeds include first-seen metadata where applicable
- [ ] both files contain a single `## Changelog` with newest entry prepended
