# n8n AI Failover — Claude → GPT-4o

Automatic failover workflow for n8n chatbots. 
If Claude fails (outage, suspended model, API error), 
GPT-4o takes over instantly. The user never notices.

## Setup

Replace these 6 placeholders before importing:

| Placeholder | What to put here |
|---|---|
| `{{TU_EMPRESA}}` | Your company name |
| `{{TU_URL_SYSTEM_PROMPT}}` | URL that returns your system prompt JSON |
| `{{TU_CHATBOT_SECRET}}` | Your chatbot API secret header value |
| `{{TU_SITIO_WEB}}` | Your website URL |
| `{{TU_TABLA_KB}}` | Your pgvector table name |
| `{{AGENTE_HUMANO}}` | Your human agent name |

Then assign your credentials in each node:
- Anthropic API key → Claude node
- OpenAI API key → GPT-4o node + both Embeddings nodes
- PostgreSQL connection → both KB nodes

## Import

n8n → Settings → Import from file → select the JSON → done.

## Video walkthrough

[My Chatbot Kept Talking When the AI Model Died](#) ← link al video 2
[The Exact n8n Failover Setup](#) ← link al video 3 cuando publiques
