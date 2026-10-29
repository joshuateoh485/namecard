# Grok Bot → Dashboard progress contract

## Status payload

`GET` your sync URL must return JSON:

| Field | Type | Notes |
|-------|------|--------|
| `bots[].id` | string | Stable id (`atlas`, …) |
| `bots[].name` | string | Display name on the floor |
| `bots[].grokName` | string | Exact Grok Bot sidebar name |
| `bots[].role` | string | Job title |
| `bots[].species` | string | Optional: `goldpaw` `shellchart` `tickfin` `owlfolio` `vaultbug` `tidewisp` |
| `bots[].status` | string | `working` `busy` `idle` `alert` `break` |
| `bots[].progress` | number | 0–100 |
| `bots[].task` | string | One-line current work |

## Minimal Worker sketch (optional)

A tiny endpoint your Bot’s MCP tool can `POST` to, and the dashboard `GET`s:

```js
// Pseudocode — store last body in KV / file
export default {
  async fetch(req, env) {
    if (req.method === 'POST') {
      const body = await req.json();
      await env.STATUS.put('bots', JSON.stringify(body));
      return new Response('ok');
    }
    const data = (await env.STATUS.get('bots')) || '{"bots":[]}';
    return new Response(data, { headers: { 'content-type': 'application/json', 'access-control-allow-origin': '*' } });
  }
}
```

Then tell each Grok Bot: “Call our `update_office_progress` MCP tool when you complete a step.”
