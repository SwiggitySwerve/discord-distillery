# Implementation Roadmap

## Phase 1: Foundations
- TypeScript project scaffold (discord.js)
- Slash command skeleton: `/distill`
- SQLite schema with `workspace_id` on all tables
- Message ingestion for one channel + time window

## Phase 2: Distillation Core
- Rubric scorer
- Section extractor (decisions, actions, blockers, insights, resources, questions)
- JSON artifact generation
- Markdown renderer

## Phase 3: Delivery + Retrieval
- Post report to destination thread/channel
- Persist report artifacts
- Add `/distill latest` and `/distill reports`

## Phase 4: Scheduled Runs
- Per-channel cadence config
- Daily/weekly automated runs
- Failure handling + retry policy

## Phase 5: Feedback Tuning
- thumbs up/down on extracted bullets
- threshold tuning from feedback data

## Definition of Done (MVP)
- Can target any server bot is installed in
- Data remains isolated per guild
- Channel-level report runs produce sectioned digest
- Reports are retrievable by command and linked in Discord

