<div align="center">

# Sådan bruger du PleumRouter

**Én API-nøgle til 200+ AI-modeller — OpenAI-kompatibel, faktureret i KRW.**

[Websted](https://pleum.ai) · [Dokumentation](https://pleum.ai/docs) · [Modeller](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · Dansk · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter er en AI-gateway: én nøgle (`plm_…`), én base-URL, 210+ modeller fra 18 udbydere — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE og flere. Den taler **OpenAI Chat Completions**, **Anthropic Messages** og **OpenAI Responses**, så næsten enhver kodningsagent, IDE-plugin og SDK kan forbindes med en enkelt linjes konfigurationsændring. Tekst, embeddings, billeder, tale og video kører alle igennem den samme nøgle.

Dette repository samler **verificerede integrationsopskrifter**. Hvert kodestykke nedenfor er testet mod den live gateway.

## Kom i gang

1. [Tilmeld dig](https://pleum.ai/signup) → Dashboard → **API Keys** → udsted en nøgle (starter med `plm_`).
2. Peg dit værktøj mod base-URL'en:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Nogle agenter (OpenCode, Crush) læser PLEUM_API_KEY — samme nøgle, sæt begge.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Røgtest:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Du får ₩1.000 gratis kredit ved tilmelding og en ₩5.000 bonus ved din første optankning.

## Integrationer

| Kategori | Værktøjer |
|---|---|
| [⚡ Ét-kommando-launcher](#-pleum-cli--den-hurtige-vej) | `pleum` CLI |
| [🤖 Terminal-kodningsagenter](#-terminal--cli-agenter) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE-/GUI-agenter](#-ide--gui-agenter) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK'er](#-sdker) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 Multimodal API](#-multimodal--billede--lyd--video) | Billeder, TTS, STT, Video, Embeddings |
| [🔌 Alt andet](#-flere-agenter) | OpenRouter-stil-ID'er, LiteLLM-proxy, 15+ flere agenter |

---

## ⚡ pleum CLI — den hurtige vej

Den officielle CLI starter din foretrukne agent allerede forbundet til PleumRouter. Ingen konfigurationsfiler bliver rørt.

```bash
npm install -g pleumrouter        # eller: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # browser-login, nøgle udstedes & gemmes automatisk
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # terminal-chat REPL
pleum models                      # vis alle modeller med priser
```

Understøttet til auto-start: `claude` · `aider` · `codex` · `goose` · `openhands` (plus konfigurationsuddrag til `opencode` · `crush`). Dine eksisterende værktøjskonfigurationer bliver aldrig ændret.

---

## 🤖 Terminal- / CLI-agenter

### Claude Code (Anthropic-kompatibel)

Claude Code og Claude Agent SDK-værktøjer forbinder via det Anthropic-kompatible `/v1/messages`-endpoint.

```bash
# ANTHROPIC_BASE_URL er ROD-URL'en (uden /v1) — CLI'en tilføjer selv /v1/messages.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# Den officielle CLI foretrækker ANTHROPIC_API_KEY; sæt begge for en sikkerheds skyld.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ Sæt **ikke** `/v1` i `ANTHROPIC_BASE_URL` — det bliver til `/v1/v1/messages` og fejler. Værktøjskald og streaming virker fra ende til anden, selv når der routes til OpenAI-kompatible modeller.

### Codex CLI (Responses API)

Codex forbinder via OpenAI Responses API (`/v1/responses`); Chat Completions-vejen blev fjernet fra Codex i februar 2026.

```toml
# ~/.codex/config.toml
# model / model_provider er nøgler i dokumentets rod (skal stå over [table]).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex tilføjer /responses → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex understøtter kun Responses API
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
// opencode.json   (eller: /connect → Other)
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

# Goose / OpenHands: sæt præfikset openai/ foran model-id'et
#   model = openai/gpt-4.1
```

### Gemini CLI

Den officielle Gemini CLI har svag understøttelse af eksterne OpenAI-kompatible endpoints; du kan få brug for en OpenAI-kompatibel wrapper eller fork.

---

## 🖥 IDE-/GUI-agenter

### Cline · Roo Code · Kilo Code · Cursor

Vælg **OpenAI Compatible** (eller **Custom OpenAI**) som udbyder og indsæt:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Brug altid **OpenAI Compatible-feltet** — den dedikerede OpenRouter-indgang er hardkodet til openrouter.ai og vil fejle. **Cursor** kræver `/v1` i base-URL'en og et ikke-tomt nøglefelt. **Kilo Code** har et kendt problem (#681), hvor den brugerdefinerede base-URL ikke sendes videre til modellisten — indtast model-ID'et manuelt.

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

Med `model: AUTODETECT` henter Continue automatisk modellisten.

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

Feltnavne kan variere afhængigt af Zed-version — tjek Zed-dokumentationen.

---

## 📦 SDK'er

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
    base_url="https://router.pleum.ai",   # rod-URL, uden /v1 — SDK'en tilføjer /v1/messages
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # enhver PleumRouter-model virker
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Multimodal — billede · lyd · video

Alle modaliteter er OpenAI-kompatible HTTP-endpoints på den samme nøgle. Vælg en model, der understøtter modaliteten, fra [`GET /v1/models`](https://pleum.ai/models).

```bash
# Billedgenerering
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Tekst-til-tale (returnerer lydbytes; pris i X-Cost-Krw-header)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Tale-til-tekst (multipart-upload)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# Videogenerering er asynkron: POST returnerer et job_id, poll derefter GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### API-flade

| Endpoint | Protokol |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (streaming, værktøjer, vision) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Billedgenerering |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Asynkron video |
| `GET /v1/models` | Modelkatalog (offentligt) |
| `GET /v1/credits` | Saldo |

---

## 🔌 Flere agenter

De fleste agenter, der ikke er nævnt her, fungerer på samme måde — sæt den OpenAI-kompatible base-URL:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** og flere.

Via det Anthropic-kompatible `/v1/messages`: **claude-code-router** forbinder også med `ANTHROPIC_BASE_URL`.

**Model-ID'er**: find dem på `GET /v1/models` eller på [modelsiden](https://pleum.ai/models). Cline, Continue, OpenCode og andre henter listen automatisk. ID'er i OpenRouter-format (`openai/gpt-5.5`) konverteres automatisk.

**LiteLLM-proxy** (Aider, OpenHands, Open Interpreter, SWE-agent og gptme er LiteLLM-baserede og forbinder direkte — men hvis du opretholder en LiteLLM-proxy):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # openai/-præfiks → OpenAI-kompatibel rute
      api_base: https://router.pleum.ai/v1           # tilføj IKKE /chat/completions
      api_key: os.environ/PLEUM_API_KEY
```

---

## Bidrag

Har du fået PleumRouter til at virke med et værktøj, der ikke er nævnt her? PR'er er velkomne — tilføj en sektion med et **testet** konfigurationsuddrag (base-URL, nøgle-miljøvariabel, model-ID-format og eventuelle faldgruber).

## Licens

[MIT](LICENSE)
