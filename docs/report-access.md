# Report Access Strategy (Draft)

## Goal
Make reports easy to access without digging through chat history.

## Access Surfaces

### 1. In-Discord Delivery (MVP)
- Post digest in configured destination channel/thread
- Pin latest report message
- Include quick links to previous report messages

### 2. Report Index Command (MVP)
`/distill reports channel:#channel limit:10`
- Returns list of recent reports with date/window
- Includes jump links to report messages

### 3. Export Artifacts (MVP+)
For each run, store:
- canonical JSON report
- markdown rendering

Expose:
- `/distill report id:<run_id>`
- `/distill latest channel:#channel`

### 4. Web Dashboard (Phase 2)
- Per-workspace auth
- Channel filter + date range
- Search across report items
- Download JSON/Markdown

## UX Rules
- Fast retrieval over fancy formatting
- Every report has deterministic run id
- Every bullet links to source message(s)
- If no signal found, still emit run artifact for traceability

