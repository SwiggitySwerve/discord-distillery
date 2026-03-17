# Report Schema (Draft)

## JSON Canonical Schema

```json
{
  "guild_id": "string",
  "channel_id": "string",
  "channel_name": "string",
  "window": {
    "start": "ISO-8601",
    "end": "ISO-8601"
  },
  "summary": {
    "messages_scanned": 0,
    "messages_included": 0,
    "signal_ratio": 0.0
  },
  "sections": {
    "decisions": [
      {
        "item": "string",
        "confidence": "high",
        "sources": ["discord_message_url"]
      }
    ],
    "action_items": [
      {
        "item": "string",
        "owner": "string|null",
        "due": "string|null",
        "confidence": "high|medium|low",
        "sources": ["discord_message_url"]
      }
    ],
    "blockers_risks": [
      {
        "item": "string",
        "impact": "string|null",
        "confidence": "high|medium|low",
        "sources": ["discord_message_url"]
      }
    ],
    "key_insights": [
      {
        "item": "string",
        "confidence": "high|medium|low",
        "sources": ["discord_message_url"]
      }
    ],
    "resources_shared": [
      {
        "url": "string",
        "why_it_matters": "string",
        "sources": ["discord_message_url"]
      }
    ],
    "open_questions": [
      {
        "item": "string",
        "owner": "string|null",
        "confidence": "high|medium|low",
        "sources": ["discord_message_url"]
      }
    ]
  }
}
```

## Markdown Rendering Template

1. **Window**: time span and channel
2. **Signal Ratio**: included vs scanned
3. **Decisions Made**
4. **Action Items**
5. **Blockers / Risks**
6. **Key Insights**
7. **Resources Shared**
8. **Open Questions**

Each bullet includes a source link.

## Output Quality Rules
- No section should invent content
- If a section has no signal, emit "None detected"
- Every non-empty item must contain at least one source URL

