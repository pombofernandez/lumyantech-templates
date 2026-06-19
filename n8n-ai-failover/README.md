# n8n AI Failover — Claude → GPT-4o

Automatic failover workflow for n8n chatbots.
If Claude fails (outage, suspended model, API error),
GPT-4o takes over instantly. The user never notices.

Built by [lumyantech](https://lumyantech.com) — AI automation and infrastructure for businesses that can't afford downtime.

---

## How it works

1. User sends a message to the chatbot
2. Claude (PRIMARY) tries to answer
3. If Claude fails for any reason — the IF node detects no output
4. GPT-4o (FALLBACK) answers with the same system prompt and knowledge base
5. User receives the response — identical behavior, zero downtime

---

## Setup — replace these 6 placeholders before importing

| Placeholder | What to put here |
|---|---|
| `{{TU_EMPRESA}}` | Your company name |
| `{{TU_URL_SYSTEM_PROMPT}}` | URL that returns your chatbot system prompt as JSON |
| `{{TU_CHATBOT_SECRET}}` | Your API secret header value |
| `{{TU_SITIO_WEB}}` | Your website URL |
| `{{TU_TABLA_KB}}` | Your pgvector table name in PostgreSQL |
| `{{AGENTE_HUMANO}}` | Your human agent name (used in override instructions) |

---

## Quick setup (recommended)

Instead of replacing placeholders one by one, run this in your terminal:

**Linux / macOS:**
```bash
sed -i \
  -e 's/{{TU_EMPRESA}}/My Company/g' \
  -e 's/{{TU_URL_SYSTEM_PROMPT}}/https:\/\/mysite.com\/api\/chatbot-config/g' \
  -e 's/{{TU_CHATBOT_SECRET}}/my-secret-here/g' \
  -e 's/{{TU_SITIO_WEB}}/https:\/\/mysite.com/g' \
  -e 's/{{TU_TABLA_KB}}/my_kb_table/g' \
  -e 's/{{AGENTE_HUMANO}}/John/g' \
  Cerebro_DEMO_Failover_TEMPLATE.json
```

**Windows (PowerShell):**
```powershell
(Get-Content Cerebro_DEMO_Failover_TEMPLATE.json) `
  -replace '{{TU_EMPRESA}}', 'My Company' `
  -replace '{{TU_URL_SYSTEM_PROMPT}}', 'https://mysite.com/api/chatbot-config' `
  -replace '{{TU_CHATBOT_SECRET}}', 'my-secret-here' `
  -replace '{{TU_SITIO_WEB}}', 'https://mysite.com' `
  -replace '{{TU_TABLA_KB}}', 'my_kb_table' `
  -replace '{{AGENTE_HUMANO}}', 'John' |
  Set-Content Cerebro_DEMO_Failover_TEMPLATE.json
```

Then import the modified file into n8n.

---

## Credentials to assign in n8n after import

- **Anthropic API key** → node `Claude (modelo PRIMARY)`
- **OpenAI API key** → nodes `GPT-4o Fallback`, `Embeddings KB (Primary)`, `Embeddings KB (Fallback)`
- **PostgreSQL connection** → nodes `KB (Primary)`, `KB (Fallback)`

---

## Import into n8n

1. Download `Cerebro_DEMO_Failover_TEMPLATE.json`
2. Open n8n → Settings → Import from file
3. Select the JSON file
4. Replace the 6 placeholders in the relevant nodes
5. Assign your credentials
6. Activate the workflow

---

## Requirements

- n8n (self-hosted or cloud)
- Anthropic API key (Claude)
- OpenAI API key (GPT-4o + embeddings)
- PostgreSQL with pgvector extension
- A URL endpoint that returns your system prompt as JSON

---

## Video walkthrough

- Part 1: [My Chatbot Kept Talking When the AI Model Died](https://youtu.be/VCLbtwbyoKQ)
- Part 2: The Exact n8n Failover Setup ← *coming soon, link after publish*

---

## License

MIT — use it, modify it, deploy it.
