<div align="center">

# របៀបប្រើប្រាស់ PleumRouter

**API key មួយ សម្រាប់គំរូ AI ជាង 200 — ត្រូវគ្នាជាមួយ OpenAI ចេញវិក្កយបត្រជារូបិយប័ណ្ណ KRW។**

[គេហទំព័រ](https://pleum.ai) · [ឯកសារណែនាំ](https://pleum.ai/docs) · [គំរូ](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · ខ្មែរ · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter គឺជា AI gateway មួយ៖ key មួយ (`plm_…`), base URL មួយ, គំរូជាង 210 មកពី provider ចំនួន 18 — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE និងផ្សេងទៀត។ វាទំនាក់ទំនងតាមប្រព័ន្ធ **OpenAI Chat Completions**, **Anthropic Messages** និង **OpenAI Responses** ដូច្នេះ coding agent, IDE plugin និង SDK ស្ទើរតែទាំងអស់អាចភ្ជាប់បានដោយកែប្រែ config គ្រាន់តែមួយបន្ទាត់។ អត្ថបទ, embeddings, រូបភាព, សំឡេង និងវីដេអូ សុទ្ធតែដំណើរការឆ្លងកាត់ key តែមួយនេះ។

Repo នេះប្រមូលផ្តុំ **រូបមន្តភ្ជាប់ (integration recipes) ដែលបានផ្ទៀងផ្ទាត់រួច**។ snippet ខាងក្រោមនីមួយៗត្រូវបានសាកល្បងជាមួយ gateway ដែលកំពុងដំណើរការជាក់ស្តែង។

## ការចាប់ផ្តើម

1. [ចុះឈ្មោះ](https://pleum.ai/signup) → Dashboard → **API Keys** → ចេញ key មួយ (ចាប់ផ្តើមដោយ `plm_`)។
2. កំណត់ឧបករណ៍របស់អ្នកឱ្យចង្អុលទៅ base URL៖

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Some agents (OpenCode, Crush) read PLEUM_API_KEY — same key, set both.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. សាកល្បងឱ្យប្រាកដថាដំណើរការ៖

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

អ្នកនឹងទទួលបានក្រេឌីតឥតគិតថ្លៃ ₩1,000 ពេលចុះឈ្មោះ និងប្រាក់រង្វាន់ ₩5,000 ពេលបញ្ចូលប្រាក់លើកដំបូង។

## ការភ្ជាប់ជាមួយឧបករណ៍ផ្សេងៗ (Integrations)

| ប្រភេទ | ឧបករណ៍ |
|---|---|
| [⚡ កម្មវិធីចាប់ផ្តើមតែមួយពាក្យបញ្ជា](#-pleum-cli--ផ្លូវលឿនបំផុត) | `pleum` CLI |
| [🤖 Coding agent តាមរយៈ Terminal](#-agent-terminal--cli) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE / Agent ប្រភេទ GUI](#-ide--agent-gui) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK](#-sdk) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 Multimodal API](#-multimodal--រូបភាព--សំឡេង--វីដេអូ) | រូបភាព, TTS, STT, វីដេអូ, Embeddings |
| [🔌 អ្វីៗផ្សេងទៀត](#-agent-ផ្សេងទៀត) | ID ប្រភេទ OpenRouter, LiteLLM proxy, agent ជាង 15 បន្ថែមទៀត |

---

## ⚡ pleum CLI — ផ្លូវលឿនបំផុត

CLI ផ្លូវការនេះនឹងបើក agent ដែលអ្នកចូលចិត្ត ដោយភ្ជាប់ជាមួយ PleumRouter រួចជាស្រេច។ គ្មានការប៉ះពាល់ file config ណាមួយឡើយ។

```bash
npm install -g pleumrouter        # or: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # browser login, key auto-issued & saved
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # terminal chat REPL
pleum models                      # list all models with pricing
```

ការចាប់ផ្តើមស្វ័យប្រវត្តិត្រូវបានគាំទ្រសម្រាប់៖ `claude` · `aider` · `codex` · `goose` · `openhands` (ព្រមទាំង snippet config សម្រាប់ `opencode` · `crush`)។ config ឧបករណ៍ដែលអ្នកមានស្រាប់ គ្មានពេលណាមួយត្រូវបានកែប្រែឡើយ។

---

## 🤖 Agent Terminal / CLI

### Claude Code (ត្រូវគ្នាជាមួយ Anthropic)

ឧបករណ៍ Claude Code និង Claude Agent SDK ភ្ជាប់តាមរយៈ endpoint `/v1/messages` ដែលត្រូវគ្នាជាមួយ Anthropic។

```bash
# ANTHROPIC_BASE_URL is the ROOT (no /v1) — the CLI appends /v1/messages itself.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# The official CLI prefers ANTHROPIC_API_KEY; set both to be safe.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ សូម **កុំ** ដាក់ `/v1` ក្នុង `ANTHROPIC_BASE_URL` — វានឹងក្លាយជា `/v1/v1/messages` ហើយបរាជ័យ។ ការហៅ tool និង streaming ដំណើរការគ្រប់ជាន់ដំបូងដល់ចុងបញ្ចប់ សូម្បីតែពេលបញ្ជូនទៅគំរូដែលត្រូវគ្នាជាមួយ OpenAI ក៏ដោយ។

### Codex CLI (Responses API)

Codex ភ្ជាប់តាមរយៈ OpenAI Responses API (`/v1/responses`); ផ្លូវ Chat Completions ត្រូវបានដកចេញពី Codex ចាប់តាំងពីខែកុម្ភៈ 2026។

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

Gemini CLI ដើមមានការគាំទ្រខ្សោយសម្រាប់ endpoint ខាងក្រៅដែលត្រូវគ្នាជាមួយ OpenAI; អ្នកប្រហែលជាត្រូវការ wrapper ឬ fork ដែលត្រូវគ្នាជាមួយ OpenAI។

---

## 🖥 IDE / Agent GUI

### Cline · Roo Code · Kilo Code · Cursor

ជ្រើសរើស **OpenAI Compatible** (ឬ **Custom OpenAI**) ជា provider រួចបិទភ្ជាប់៖

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ ត្រូវប្រើ **ចន្លោះ OpenAI Compatible** ជានិច្ច — ចន្លោះ OpenRouter ដែលមានស្រាប់ ត្រូវបានកំណត់ hardcode ទៅ openrouter.ai ហើយនឹងបរាជ័យ។ **Cursor** តម្រូវឱ្យមាន `/v1` នៅក្នុង base URL និងប្រអប់ key ដែលមិនទទេ។ **Kilo Code** មានបញ្ហាដែលដឹងស្រាប់ (#681) ដែល base URL ផ្ទាល់ខ្លួន មិនត្រូវបានបញ្ជូនទៅការទាញយកបញ្ជីគំរូ — សូមបញ្ចូល model ID ដោយដៃ។

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

ជាមួយ `model: AUTODETECT`, Continue នឹងទាញយកបញ្ជីគំរូដោយស្វ័យប្រវត្តិ។

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

ឈ្មោះ field អាចខុសគ្នាទៅតាមកំណែ Zed — សូមពិនិត្យឯកសារណែនាំរបស់ Zed។

---

## 📦 SDK

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

## 🎨 Multimodal — រូបភាព · សំឡេង · វីដេអូ

ម៉ូដទាំងអស់សុទ្ធតែជា HTTP endpoint ដែលត្រូវគ្នាជាមួយ OpenAI លើ key តែមួយដដែល។ ជ្រើសរើសគំរូដែលគាំទ្រម៉ូដនោះពី [`GET /v1/models`](https://pleum.ai/models)។

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

### ផ្ទៃប្រព័ន្ធ API

| Endpoint | ពិធីការ |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (streaming, tools, vision) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | ការបង្កើតរូបភាព |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | វីដេអូបែប Async |
| `GET /v1/models` | កាតាឡុកគំរូ (សាធារណៈ) |
| `GET /v1/credits` | សមតុល្យក្រេឌីត |

---

## 🔌 Agent ផ្សេងទៀត

Agent ភាគច្រើនដែលមិនបានរាយក្នុងនេះ ដំណើរការតាមវិធីដូចគ្នា — គ្រាន់តែកំណត់ base URL ដែលត្រូវគ្នាជាមួយ OpenAI៖

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** និងផ្សេងទៀត។

តាមរយៈ `/v1/messages` ដែលត្រូវគ្នាជាមួយ Anthropic៖ **claude-code-router** ក៏ភ្ជាប់ដោយប្រើ `ANTHROPIC_BASE_URL` ដែរ។

**Model ID**៖ រកបានតាមរយៈ `GET /v1/models` ឬនៅលើ [ទំព័រគំរូ](https://pleum.ai/models)។ Cline, Continue, OpenCode និងផ្សេងទៀត ទាញយកបញ្ជីនេះដោយស្វ័យប្រវត្តិ។ ID ទម្រង់ OpenRouter (`openai/gpt-5.5`) ត្រូវបានបំប្លែងដោយស្វ័យប្រវត្តិ។

**LiteLLM proxy** (Aider, OpenHands, Open Interpreter, SWE-agent និង gptme ជា LiteLLM-based ហើយភ្ជាប់ដោយផ្ទាល់ — ប៉ុន្តែប្រសិនបើអ្នកកំពុងប្រើ LiteLLM proxy)៖

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

## ការចូលរួមចំណែក

បានប្រើ PleumRouter ជាមួយឧបករណ៍ណាមួយដែលមិនទាន់មានក្នុងបញ្ជីនេះមែនទេ? PR ត្រូវបានស្វាគមន៍ — សូមបន្ថែមផ្នែកមួយដែលមាន snippet config ដែល **បានសាកល្បងផ្ទៀងផ្ទាត់រួច** (base URL, key env, ទម្រង់ model ID និងចំណុចលំបាកណាមួយ)។

## អាជ្ញាប័ណ្ណ

[MIT](LICENSE)
