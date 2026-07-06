<div align="center">

# Hoe gebruik je PleumRouter

**Eén API-sleutel voor 200+ AI-modellen — OpenAI-compatibel, gefactureerd in KRW.**

[Website](https://pleum.ai) · [Documentatie](https://pleum.ai/docs) · [Modellen](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · Nederlands · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter is een AI-gateway: één sleutel (`plm_…`), één basis-URL, 210+ modellen van 18 providers — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE en meer. Het spreekt **OpenAI Chat Completions**, **Anthropic Messages** en **OpenAI Responses**, zodat vrijwel elke coding agent, IDE-plugin en SDK verbinding maakt met slechts één regel configuratiewijziging. Tekst, embeddings, afbeeldingen, spraak en video draaien allemaal via dezelfde sleutel.

Deze repo verzamelt **geverifieerde integratierecepten**. Elk fragment hieronder is getest tegen de live gateway.

## Aan de slag

1. [Meld je aan](https://pleum.ai/signup) → Dashboard → **API Keys** → geef een sleutel uit (begint met `plm_`).
2. Wijs je tool naar de basis-URL:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Sommige agents (OpenCode, Crush) lezen PLEUM_API_KEY — dezelfde sleutel, stel beide in.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Smoke test:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Je krijgt ₩1.000 gratis tegoed bij aanmelding en een bonus van ₩5.000 bij je eerste opwaardering.

## Integraties

| Categorie | Tools |
|---|---|
| [⚡ Startcommando in één stap](#-pleum-cli--het-snelle-pad) | `pleum` CLI |
| [🤖 Terminal coding agents](#-terminal--cli-agents) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE- / GUI-agents](#-ide--gui-agents) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK's](#-sdks) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 Multimodale API](#-multimodaal--afbeelding--audio--video) | Afbeeldingen, TTS, STT, Video, Embeddings |
| [🔌 Al de rest](#-meer-agents) | OpenRouter-stijl ID's, LiteLLM-proxy, 15+ andere agents |

---

## ⚡ pleum CLI — het snelle pad

De officiële CLI start je favoriete agent al aangesloten op PleumRouter. Geen configuratiebestanden worden aangeraakt.

```bash
npm install -g pleumrouter        # of: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # inloggen via browser, sleutel automatisch uitgegeven & opgeslagen
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # terminal chat REPL
pleum models                      # lijst alle modellen met prijzen
```

Ondersteund voor automatisch starten: `claude` · `aider` · `codex` · `goose` · `openhands` (plus configuratiefragmenten voor `opencode` · `crush`). Je bestaande toolconfiguraties worden nooit gewijzigd.

---

## 🤖 Terminal / CLI-agents

### Claude Code (Anthropic-compatibel)

Claude Code en Claude Agent SDK-tools maken verbinding via het Anthropic-compatibele `/v1/messages`-eindpunt.

```bash
# ANTHROPIC_BASE_URL is de ROOT (geen /v1) — de CLI voegt zelf /v1/messages toe.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# De officiële CLI geeft de voorkeur aan ANTHROPIC_API_KEY; stel beide in om zeker te zijn.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ Zet **geen** `/v1` in `ANTHROPIC_BASE_URL` — het wordt dan `/v1/v1/messages` en mislukt. Tool calls en streaming werken end-to-end, zelfs wanneer gerouteerd naar OpenAI-compatibele modellen.

### Codex CLI (Responses API)

Codex maakt verbinding via de OpenAI Responses API (`/v1/responses`); het Chat Completions-pad is in februari 2026 uit Codex verwijderd.

```toml
# ~/.codex/config.toml
# model / model_provider zijn document-root sleutels (moeten boven de [table] staan).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex voegt /responses toe → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex ondersteunt alleen de Responses API
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
// opencode.json   (of: /connect → Other)
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

# Goose / OpenHands: zet het voorvoegsel openai/ vóór het model-id
#   model = openai/gpt-4.1
```

### Gemini CLI

De upstream Gemini CLI heeft zwakke ondersteuning voor externe OpenAI-compatibele eindpunten; mogelijk heb je een OpenAI-compatibele wrapper of fork nodig.

---

## 🖥 IDE- / GUI-agents

### Cline · Roo Code · Kilo Code · Cursor

Kies **OpenAI Compatible** (of **Custom OpenAI**) als provider en plak:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Gebruik altijd de **OpenAI Compatible-sleuf** — de speciale OpenRouter-invoer is hardgecodeerd naar openrouter.ai en zal mislukken. **Cursor** vereist `/v1` in de basis-URL en een niet-leeg sleutelveld. **Kilo Code** heeft een bekend probleem (#681) waarbij de aangepaste basis-URL niet wordt doorgegeven aan de modellenlijst — voer het model-id handmatig in.

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

Met `model: AUTODETECT` haalt Continue de modellenlijst automatisch op.

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

Veldnamen kunnen per Zed-versie verschillen — raadpleeg de Zed-documentatie.

---

## 📦 SDK's

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
    base_url="https://router.pleum.ai",   # root, geen /v1 — SDK voegt /v1/messages toe
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # elk PleumRouter-model werkt
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Multimodaal — afbeelding · audio · video

Alle modaliteiten zijn OpenAI-compatibele HTTP-eindpunten op dezelfde sleutel. Kies een model dat de modaliteit ondersteunt via [`GET /v1/models`](https://pleum.ai/models).

```bash
# Afbeelding genereren
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Tekst-naar-spraak (retourneert audiobytes; kosten in de header X-Cost-Krw)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Spraak-naar-tekst (multipart-upload)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# Videogeneratie is asynchroon: POST geeft een job_id terug, poll daarna GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### API-oppervlak

| Eindpunt | Protocol |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (streaming, tools, vision) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Afbeelding genereren |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Asynchrone video |
| `GET /v1/models` | Modelcatalogus (openbaar) |
| `GET /v1/credits` | Saldo |

---

## 🔌 Meer agents

De meeste agents die hier niet vermeld staan, werken op dezelfde manier — stel de OpenAI-compatibele basis-URL in:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** en meer.

Via het Anthropic-compatibele `/v1/messages`: **claude-code-router** maakt ook verbinding met `ANTHROPIC_BASE_URL`.

**Model-ID's**: vind ze via `GET /v1/models` of op de [modellenpagina](https://pleum.ai/models). Cline, Continue, OpenCode en anderen halen de lijst automatisch op. ID's in OpenRouter-formaat (`openai/gpt-5.5`) worden automatisch geconverteerd.

**LiteLLM-proxy** (Aider, OpenHands, Open Interpreter, SWE-agent en gptme zijn LiteLLM-gebaseerd en maken direct verbinding — maar als je een LiteLLM-proxy aanhoudt):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # openai/-voorvoegsel → OpenAI-compat route
      api_base: https://router.pleum.ai/v1           # voeg GEEN /chat/completions toe
      api_key: os.environ/PLEUM_API_KEY
```

---

## Bijdragen

PleumRouter werkend gekregen met een tool die hier niet vermeld staat? PR's zijn welkom — voeg een sectie toe met een **geteste** configuratiesnippet (basis-URL, sleutel-omgevingsvariabele, model-ID-formaat en eventuele valkuilen).

## Licentie

[MIT](LICENSE)
