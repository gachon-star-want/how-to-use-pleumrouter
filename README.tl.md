<div align="center">

# Paano gamitin ang PleumRouter

**Iisang API key para sa 200+ AI models — OpenAI-compatible, sinisingil sa KRW.**

[Website](https://pleum.ai) · [Docs](https://pleum.ai/docs) · [Mga Modelo](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · Filipino · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

Ang PleumRouter ay isang AI gateway: iisang key (`plm_…`), iisang base URL, 210+ na modelo mula sa 18 providers — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE at marami pang iba. Sinusuportahan nito ang **OpenAI Chat Completions**, **Anthropic Messages**, at **OpenAI Responses**, kaya halos lahat ng coding agent, IDE plugin, at SDK ay kayang kumonekta sa pamamagitan lamang ng isang linyang pagbabago sa config. Ang text, embeddings, image, speech, at video ay lahat tumatakbo gamit ang parehong key.

Ang repong ito ay naglalaman ng **beripikadong mga recipe para sa integrasyon**. Bawat snippet sa ibaba ay nasubok laban sa live na gateway.

## Pagsisimula

1. [Mag-sign up](https://pleum.ai/signup) → Dashboard → **API Keys** → mag-isyu ng key (nagsisimula sa `plm_`).
2. Ituro ang iyong tool sa base URL:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Ang ilang agents (OpenCode, Crush) ay bumabasa ng PLEUM_API_KEY — parehong key, i-set ang dalawa.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Smoke test:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Makakakuha ka ng ₩1,000 libreng kredito sa pag-sign up at ₩5,000 bonus sa iyong unang top-up.

## Mga Integrasyon

| Kategorya | Mga Tool |
|---|---|
| [⚡ One-command launcher](#-pleum-cli--ang-mabilis-na-daan) | `pleum` CLI |
| [🤖 Mga terminal coding agent](#-terminal--cli-agents) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE / GUI agents](#-ide--gui-agents) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 Mga SDK](#-mga-sdk) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 Multimodal API](#-multimodal--image--audio--video) | Images, TTS, STT, Video, Embeddings |
| [🔌 Lahat pang iba](#-iba-pang-mga-agent) | OpenRouter-style IDs, LiteLLM proxy, 15+ pang agent |

---

## ⚡ pleum CLI — ang mabilis na daan

Ang opisyal na CLI ay naglulunsad ng iyong paboritong agent na naka-wire na sa PleumRouter. Walang config files na nagagalaw.

```bash
npm install -g pleumrouter        # o: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # browser login, awtomatikong nag-isyu at nag-save ng key
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # terminal chat REPL
pleum models                      # ilista ang lahat ng modelo kasama ang presyo
```

Suportado para sa auto-launch: `claude` · `aider` · `codex` · `goose` · `openhands` (kasama ang config snippets para sa `opencode` · `crush`). Ang iyong mga umiiral na config ng tool ay hindi kailanman binabago.

---

## 🤖 Terminal / CLI agents

### Claude Code (Anthropic-compatible)

Ang Claude Code at Claude Agent SDK tools ay kumokonekta sa pamamagitan ng Anthropic-compatible na `/v1/messages` endpoint.

```bash
# Ang ANTHROPIC_BASE_URL ay ang ROOT (walang /v1) — idinadagdag mismo ng CLI ang /v1/messages.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# Mas gusto ng opisyal na CLI ang ANTHROPIC_API_KEY; i-set ang dalawa para sigurado.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ **Huwag** ilagay ang `/v1` sa `ANTHROPIC_BASE_URL` — ito ay magiging `/v1/v1/messages` at mabibigo. Gumagana ang tool calls at streaming nang buong-buo, kahit na naka-route papunta sa mga OpenAI-compatible na modelo.

### Codex CLI (Responses API)

Kumokonekta ang Codex sa pamamagitan ng OpenAI Responses API (`/v1/responses`); ang Chat Completions path ay tinanggal na sa Codex noong Pebrero 2026.

```toml
# ~/.codex/config.toml
# model / model_provider ay document-root keys (dapat nasa itaas ng [table]).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Idinadagdag ng Codex ang /responses → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Sinusuportahan lang ng Codex ang Responses API
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
// opencode.json   (o: /connect → Other)
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

# Goose / OpenHands: ilagay ang openai/ bilang prefix sa model id
#   model = openai/gpt-4.1
```

### Gemini CLI

Ang upstream Gemini CLI ay may mahinang suporta para sa mga external na OpenAI-compatible na endpoint; maaaring kailanganin mo ng OpenAI-compatible wrapper o fork.

---

## 🖥 IDE / GUI agents

### Cline · Roo Code · Kilo Code · Cursor

Piliin ang **OpenAI Compatible** (o **Custom OpenAI**) bilang provider at i-paste:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Laging gamitin ang **OpenAI Compatible slot** — ang dedikadong OpenRouter entry ay hardcoded sa openrouter.ai at mabibigo. Kinakailangan ng **Cursor** ang `/v1` sa base URL at isang hindi-blangkong key field. May kilalang isyu ang **Kilo Code** (#681) kung saan ang custom base URL ay hindi ipinapasa sa model listing — i-type nang manwal ang model ID.

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

Gamit ang `model: AUTODETECT`, awtomatikong kinukuha ng Continue ang listahan ng modelo.

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

Maaaring magkaiba ang mga field name depende sa bersyon ng Zed — tingnan ang Zed docs.

---

## 📦 Mga SDK

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
    base_url="https://router.pleum.ai",   # root, walang /v1 — idinadagdag ng SDK ang /v1/messages
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # gumagana ang kahit anong modelo ng PleumRouter
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Multimodal — image · audio · video

Ang lahat ng modalidad ay mga OpenAI-compatible na HTTP endpoint gamit ang parehong key. Pumili ng modelo na sumusuporta sa modalidad mula sa [`GET /v1/models`](https://pleum.ai/models).

```bash
# Image generation
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Text-to-speech (nagbabalik ng audio bytes; nasa X-Cost-Krw header ang gastos)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Speech-to-text (multipart upload)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# Ang video generation ay asynchronous: ang POST ay nagbabalik ng job_id, pagkatapos ay i-poll ang GET /v1/jobs/{job_id}
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
| `GET /v1/models` | Model catalog (pampubliko) |
| `GET /v1/credits` | Balance |

---

## 🔌 Iba pang mga agent

Karamihan sa mga agent na hindi nakalista dito ay gumagana sa parehong paraan — i-set ang OpenAI-compatible na base URL:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** at marami pa.

Sa pamamagitan ng Anthropic-compatible na `/v1/messages`: kumokonekta rin ang **claude-code-router** gamit ang `ANTHROPIC_BASE_URL`.

**Mga Model ID**: hanapin ang mga ito sa `GET /v1/models` o sa [models page](https://pleum.ai/models). Awtomatikong kinukuha ng Cline, Continue, OpenCode, at iba pa ang listahan. Ang mga ID na OpenRouter-format (`openai/gpt-5.5`) ay awtomatikong kino-convert.

**LiteLLM proxy** (ang Aider, OpenHands, Open Interpreter, SWE-agent, at gptme ay LiteLLM-based at direktang kumokonekta — pero kung nagpapanatili ka ng LiteLLM proxy):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # openai/ prefix → OpenAI-compat route
      api_base: https://router.pleum.ai/v1           # HUWAG idagdag ang /chat/completions
      api_key: os.environ/PLEUM_API_KEY
```

---

## Pag-ambag

Napagana mo ba ang PleumRouter kasama ang isang tool na hindi nakalista dito? Malugod na tinatanggap ang mga PR — magdagdag ng seksyon na may **nasubok** na config snippet (base URL, key env, format ng model ID, at anumang gotcha).

## Lisensya

[MIT](LICENSE)
