# AI Nodes

LangChain-powered AI nodes for agents, chat models, and embeddings.

## Contents
- [AI Agent](#ai-agent)
- [OpenAI Chat Model](#openai-chat-model)
- [OpenAI Embeddings](#openai-embeddings)
- [Connection Pattern](#connection-pattern)

---

## AI Agent

```json
{
  "id": "ai-agent-1",
  "name": "AI Agent",
  "type": "@n8n/n8n-nodes-langchain.agent",
  "typeVersion": 1.7,
  "position": [650, 300],
  "parameters": {
    "promptType": "define",
    "text": "={{ $json.body.message }}",
    "hasOutputParser": true,
    "options": {
      "systemMessage": "You are a helpful assistant. Answer questions concisely."
    }
  }
}
```

**Important:** The AI Agent requires a chat model connected via `ai_languageModel` input.

---

## OpenAI Chat Model

```json
{
  "id": "openai-chat-1",
  "name": "OpenAI Chat Model",
  "type": "@n8n/n8n-nodes-langchain.lmChatOpenAi",
  "typeVersion": 1.2,
  "position": [450, 500],
  "parameters": {
    "model": {
      "__rl": true,
      "mode": "list",
      "value": "gpt-4o",
      "cachedResultName": "gpt-4o"
    },
    "options": {
      "temperature": 0.7
    }
  },
  "credentials": {
    "openAiApi": {
      "id": "cred-id",
      "name": "OpenAI API"
    }
  }
}
```

**Available models:** `gpt-4o`, `gpt-4o-mini`, `gpt-4-turbo`, `gpt-3.5-turbo`

---

## OpenAI Embeddings

```json
{
  "id": "embeddings-1",
  "name": "Embeddings OpenAI",
  "type": "@n8n/n8n-nodes-langchain.embeddingsOpenAi",
  "typeVersion": 1.1,
  "position": [450, 500],
  "parameters": {
    "model": "text-embedding-3-small",
    "options": {}
  },
  "credentials": {
    "openAiApi": {
      "id": "cred-id",
      "name": "OpenAI API"
    }
  }
}
```

---

## Connection Pattern

AI Agent with Chat Model connected:

```json
{
  "connections": {
    "Webhook": {
      "main": [[{ "node": "AI Agent", "type": "main", "index": 0 }]]
    },
    "OpenAI Chat Model": {
      "ai_languageModel": [[{ "node": "AI Agent", "type": "ai_languageModel", "index": 0 }]]
    }
  }
}
```

**Note:** The chat model uses `ai_languageModel` connection type, not `main`.
