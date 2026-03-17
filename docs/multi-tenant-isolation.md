# Multi-Tenant Isolation Plan (Draft)

## Goal
Support multiple Discord servers (guilds) with strict isolation so one server's data, settings, and reports never leak into another.

## Isolation Model
Use a first-class **workspace key**:
- `workspace_id = discord:<guild_id>`

Every persisted row must include `workspace_id`.

## Data Boundaries
Partition by workspace for:
- channel configs
- distillation runs
- extracted report items
- prompt templates
- feedback signals
- API tokens / integration settings

## Security Rules
- Never query without `workspace_id` filter
- Never render report items whose source rows differ in `workspace_id`
- Enforce at repository/service layer and validate again at API/command boundary

## Deployment Modes

### Single Bot, Multi-Guild
- One bot process in many guilds
- Strict row-level partitioning by `workspace_id`

### Optional Dedicated Worker per Workspace (later)
- Queue and workers partitioned by `workspace_id`
- Better noisy-neighbor isolation for scale

## Suggested Storage Keys
- `workspaces(id, guild_id, name, created_at)`
- `channels(id, workspace_id, channel_id, channel_name, cadence, enabled)`
- `runs(id, workspace_id, channel_id, window_start, window_end, status, stats_json)`
- `report_items(id, workspace_id, run_id, section, item_json)`
- `artifacts(id, workspace_id, run_id, type, content)`

## Access Control
Only allow command invocations where:
1. user belongs to guild
2. command executed within the same guild
3. target channel belongs to same guild

