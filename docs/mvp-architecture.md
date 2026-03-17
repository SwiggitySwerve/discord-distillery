# MVP Architecture (Draft)

## Objective
Build a Discord bot/service that ingests channel messages for a time window and outputs high-signal, sectioned reports.

## Core Components

1. **Ingestion Layer**
   - Pull messages by channel + time range
   - Preserve metadata: author, timestamp, thread linkage, message URL

2. **Preprocessing Layer**
   - Normalize text (mentions, links, emoji handling)
   - Group adjacent/reply-linked messages into context chunks

3. **Scoring + Extraction Layer**
   - Apply signal rubric to messages/chunks
   - Extract candidate items for each report section
   - Attach source message URLs and confidence

4. **Report Composer**
   - Build canonical JSON output
   - Render markdown report for human consumption

5. **Delivery Layer**
   - Post digest into target channel/thread
   - Optional: save artifacts to storage for history/search

## Proposed Tech (MVP)
- Runtime: Node.js + TypeScript
- Discord: discord.js
- Data: SQLite (runs, windows, extracted items)
- LLM: provider-agnostic adapter (OpenAI/Anthropic), with deterministic prompts

## Commands (MVP)
- `/distill channel:#name window:24h`
- `/distill channel:#name start:<timestamp> end:<timestamp>`
- `/distill config channel:#name cadence:daily`

## Guardrails
- Require source URL on every extracted bullet
- Redact sensitive tokens by default
- Hard cap token usage per run
- If low confidence dominates, emit warning and reduce claims

## Milestones

### Milestone 1
- Manual run command for one channel and window
- Produce JSON + markdown report

### Milestone 2
- Scheduled daily digests per configured channel
- Persistent run history and replay

### Milestone 3
- Feedback loop: thumbs up/down on extracted bullets
- Tune rubric thresholds based on feedback

