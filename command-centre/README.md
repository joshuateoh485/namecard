# Private Command Centre — Grok Bot Floor

Animated family-office dashboard + Pokémon-**inspired** critter agents (original art, not Nintendo IP).

## Open locally

```bash
cd command-centre
python3 -m http.server 8765
```

- Dashboard: http://127.0.0.1:8765/
- Agent Office: http://127.0.0.1:8765/#office

Keep this folder **private**. Do not enable public GitHub Pages if only you should see it.

## Connect your Grok Bots

Grok Bot has **no official public API** to list bots or read chat progress (as of 2026). Supported bridges:

1. **Status JSON URL** (best for this dashboard)  
   Host a small JSON file your bots update (gist, Worker, your server). Shape:

   ```json
   {
     "bots": [
       {
         "id": "atlas",
         "name": "Atlas",
         "grokName": "Atlas",
         "role": "Portfolio Strategist",
         "status": "working",
         "progress": 62,
         "task": "ASEAN equity trim"
       }
     ]
   }
   ```

   In the UI: **Connect** → paste the URL → **Save & sync**. The page polls every 60s.

2. **Paste import**  
   Export or hand-write the same JSON and paste it in **Connect**.

3. **Map names**  
   Set `grokName` to the exact sidebar name of each Grok Bot so the floor stays matched when you rename display labels.

4. **Ask each Bot** (in Grok Bot chat) to remember:  
   “When you finish a milestone, update our family-office status JSON at `<your URL>` with progress 0–100 and a one-line task.”  
   Pair that with an MCP tool or webhook relay you control — Grok Bot can call **your** tools; it cannot be scraped from outside without community/undocumented gateways.

5. **Routine webhooks** only *start* a Bot run (`POST` + bearer). They do not stream progress into this UI by themselves.

## Floor behaviours

Critters will on their own:

- Work / type at desks  
- Talk to each other (speech bubbles)  
- Drink coffee at the lounge bar  
- Play snooker on the lounge table  

Progress bars on the Dashboard drift gently in demo mode and jump when sync JSON updates.
