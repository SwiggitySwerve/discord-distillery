# Signal Scoring Rubric (Draft)

## Purpose
Classify Discord messages as **signal** (include in report) or **noise** (exclude), with confidence.

## Scoring Model
Score each message from **0 to 100**.

- **70-100:** Include (high-value signal)
- **50-69:** Maybe include (needs context aggregation)
- **0-49:** Exclude (low signal/noise)

## Positive Features (+)

### Decision Content (+30)
- Explicit team decisions, approvals, rejections
- Example cues: "we should", "decided", "approved", "ship this"

### Actionability (+25)
- Tasks with owner and/or due date
- Example cues: "I'll handle", "TODO", "by Friday"

### Blockers / Risks (+20)
- Mentions impediments, dependencies, incidents
- Example cues: "blocked", "can't proceed", "risk"

### Novel Insight (+15)
- New finding, root cause, strategy insight, technical discovery

### Evidence / Context (+10)
- Link + explanation, metric + implication, log + interpretation

## Negative Features (-)

### Pure Social / Banter (-35)
- Memes, jokes-only, greetings-only, low-content chatter

### Repetition / Echo (-20)
- Restates prior points without net-new info

### Ambiguous One-Liners (-15)
- "yeah", "do it", "same", without context

### Off-topic Drift (-20)
- Content unrelated to channel/project objective

## Overrides

### Hard Include
Always include if message clearly contains:
- final decision
- explicit blocker
- assigned action item

### Hard Exclude
Always exclude if message is:
- emoji-only/reaction-only text
- obvious spam
- unrelated meme content

## Aggregation Rules
Single messages can be low-signal but become meaningful in clusters.

- Combine adjacent messages by same author within short window (e.g., 2-5 min)
- Resolve references/replies before final scoring
- Promote score when message adds evidence to an active decision thread

## Confidence
For each extracted item, emit:
- `confidence`: `high | medium | low`
- `evidence_count`: number of source messages supporting the item

