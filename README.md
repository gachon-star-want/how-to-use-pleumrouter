<div align="center">

# Awesome PleumRouter

**One API key for 200+ AI models — OpenAI-compatible, billed in KRW.**

[Website](https://pleum.ai) · [Docs](https://pleum.ai/docs) · [Models](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[한국어](README.ko.md) | English

</div>

PleumRouter is an AI gateway: one key (`plm_…`), one base URL, 210+ models from 18 providers — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE and more. It speaks **OpenAI Chat Completions**, **Anthropic Messages**, and **OpenAI Responses**, so almost every coding agent, IDE plugin, and SDK connects with a one-line config change. Text, embeddings, image, speech and video all run through the same key.

This repo collects **verified integration recipes**. Every snippet below is tested against the live gateway.

## Getting started

1. [Sign up](https://pleum.ai/signup) → Dashboard → **API Keys** → issue a key (starts with `plm_`).
2. Point your tool at the base URL:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Some agents (OpenCode, Crush) read PLEUM_API_KEY — same key, set both.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Smoke test:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

You get ₩1,000 free credit on signup and a ₩5,000 bonus on your first top-up.

## Integrations

| Category | Tools |
|---|---|
| [⚡ One-command launcher](#-pleum-cli--the-fast-path) | `pleum` CLI |
| [🤖 Terminal coding agents](#-terminal--cli-agents) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE / GUI agents](#-ide--gui-agents) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDKs](#-sdks) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 Multimodal API](#-multimodal--image--audio--video) | Images, TTS, STT, Video, Embeddings |
| [🔌 Everything else](#-more-agents) | OpenRouter-style IDs, LiteLLM proxy, 15+ more agents |

---

## ⚡ pleum CLI — the fast path

The official CLI launches your favorite agent already wired to PleumRouter. No config files touched.

```bash
npm install -g pleumrouter        # or: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # browser login, key auto-issued & saved
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # terminal chat REPL
pleum models                      # list all models with pricing
```

Supported for auto-launch: `claude` · `aider` · `codex` · `goose` · `openhands` (plus config snippets for `opencode` · `crush`). Your existing tool configs are never modified.

---

## 🤖 Terminal / CLI agents

### Claude Code (Anthropic-compatible)

Claude Code and Claude Agent SDK tools connect via the Anthropic-compatible `/v1/messages` endpoint.

```bash
# ANTHROPIC_BASE_URL is the ROOT (no /v1) — the CLI appends /v1/messages itself.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# The official CLI prefers ANTHROPIC_API_KEY; set both to be safe.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ Do **not** put `/v1` in `ANTHROPIC_BASE_URL` — it becomes `/v1/v1/messages` and fails. Tool calls and streaming work end-to-end, even when routed to OpenAI-compatible models.

### Codex CLI (Responses API)

Codex connects via the OpenAI Responses API (`/v1/responses`); the Chat Completions path was removed from Codex in February 2026.

```toml
# ~/.codex/config.toml
# model / model_provider are document-root keys (must be above the [table]).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex appends /responses → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex supports only the Responses API
```

```bash
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx && codex
```

### Aider

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx

aider --model openai/gpt-4.1
```

### OpenCode

```jsonc
// opencode.json   (or: /connect → Other)
{
  "provider": {
    "pleum": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "PleumRouter",
      "options": {
        "baseURL": "https://router.pleum.ai/v1",
        "apiKey": "{env:PLEUM_API_KEY}"
      },
      "models": { "gpt-4.1": {} }
    }
  }
}
```

### Crush

```jsonc
// crush.json
{
  "providers": {
    "pleum": {
      "type": "openai-compat",
      "base_url": "https://router.pleum.ai/v1",
      "api_key": "$PLEUM_API_KEY",
      "models": [{ "id": "gpt-4.1", "name": "gpt-4.1" }]
    }
  }
}
```

### Goose · OpenHands

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx

# Goose / OpenHands: prefix the model id with openai/
#   model = openai/gpt-4.1
```

### Gemini CLI

Upstream Gemini CLI has weak support for external OpenAI-compatible endpoints; you may need an OpenAI-compatible wrapper or fork.

---

## 🖥 IDE / GUI agents

### Cline · Roo Code · Kilo Code · Cursor

Pick **OpenAI Compatible** (or **Custom OpenAI**) as the provider and paste:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Always use the **OpenAI Compatible slot** — the dedicated OpenRouter entry is hardcoded to openrouter.ai and will fail. **Cursor** requires `/v1` in the base URL and a non-empty key field. **Kilo Code** has a known issue (#681) where the custom base URL isn't passed to model listing — enter the model ID manually.

### Continue.dev

```yaml
# ~/.continue/config.yaml
models:
  - name: PleumRouter
    provider: openai
    apiBase: https://router.pleum.ai/v1
    apiKey: plm_xxxxxxxxxxxxxxxx
    model: AUTODETECT
```

With `model: AUTODETECT` Continue pulls the model list automatically.

### Zed

```jsonc
// Zed settings.json
{
  "language_models": {
    "openai_compatible": {
      "PleumRouter": {
        "api_url": "https://router.pleum.ai/v1",
        "available_models": [
          { "name": "gpt-4.1", "max_tokens": 128000 }
        ]
      }
    }
  }
}
```

Field names can vary by Zed version — check the Zed docs.

---

## 📦 SDKs

### OpenAI SDK (Python)

```python
from openai import OpenAI

client = OpenAI(
    base_url="https://router.pleum.ai/v1",
    api_key="plm_xxxxxxxxxxxxxxxx",
)

resp = client.chat.completions.create(
    model="gpt-4.1",
    messages=[{"role": "user", "content": "Hello!"}],
)
print(resp.choices[0].message.content)
```

### OpenAI SDK (JavaScript / TypeScript)

```ts
import OpenAI from "openai";

const client = new OpenAI({
  baseURL: "https://router.pleum.ai/v1",
  apiKey: "plm_xxxxxxxxxxxxxxxx",
});

const resp = await client.chat.completions.create({
  model: "gpt-4.1",
  messages: [{ role: "user", content: "Hello!" }],
});
console.log(resp.choices[0].message.content);
```

### Anthropic SDK

```python
import anthropic

client = anthropic.Anthropic(
    base_url="https://router.pleum.ai",   # root, no /v1 — SDK appends /v1/messages
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # any PleumRouter model works
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Multimodal — image · audio · video

All modalities are OpenAI-compatible HTTP endpoints on the same key. Pick a model that supports the modality from [`GET /v1/models`](https://pleum.ai/models).

```bash
# Image generation
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Text-to-speech (returns audio bytes; cost in X-Cost-Krw header)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Speech-to-text (multipart upload)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# Video generation is async: POST returns a job_id, then poll GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### API surface

| Endpoint | Protocol |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (streaming, tools, vision) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Image generation |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Async video |
| `GET /v1/models` | Model catalog (public) |
| `GET /v1/credits` | Balance |

---

## 🔌 More agents

Most agents not listed here work the same way — set the OpenAI-compatible base URL:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** and more.

Via Anthropic-compatible `/v1/messages`: **claude-code-router** also connects with `ANTHROPIC_BASE_URL`.

**Model IDs**: find them at `GET /v1/models` or on the [models page](https://pleum.ai/models). Cline, Continue, OpenCode and others fetch the list automatically. OpenRouter-format IDs (`openai/gpt-5.5`) are converted automatically.

**LiteLLM proxy** (Aider, OpenHands, Open Interpreter, SWE-agent and gptme are LiteLLM-based and connect directly — but if you keep a LiteLLM proxy):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # openai/ prefix → OpenAI-compat route
      api_base: https://router.pleum.ai/v1           # do NOT append /chat/completions
      api_key: os.environ/PLEUM_API_KEY
```

---

## Contributing

Got PleumRouter working with a tool not listed here? PRs welcome — add a section with a **tested** config snippet (base URL, key env, model ID format, and any gotchas).

## License

[MIT](LICENSE)
