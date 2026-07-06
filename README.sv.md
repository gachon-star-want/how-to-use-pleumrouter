<div align="center">

# Så använder du PleumRouter

**En API-nyckel för 200+ AI-modeller — OpenAI-kompatibel, fakturerad i KRW.**

[Webbplats](https://pleum.ai) · [Dokumentation](https://pleum.ai/docs) · [Modeller](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · Svenska · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter är en AI-gateway: en nyckel (`plm_…`), en bas-URL, 210+ modeller från 18 leverantörer — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE med flera. Den talar **OpenAI Chat Completions**, **Anthropic Messages** och **OpenAI Responses**, så nästan varje kodningsagent, IDE-plugin och SDK ansluter med en enda konfigurationsändring. Text, embeddingar, bild, tal och video körs alla genom samma nyckel.

Det här repot samlar **verifierade integrationsrecept**. Varje kodsnutt nedan är testad mot den skarpa gatewayen.

## Kom igång

1. [Skapa konto](https://pleum.ai/signup) → Dashboard → **API Keys** → utfärda en nyckel (börjar med `plm_`).
2. Peka ditt verktyg mot bas-URL:en:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Vissa agenter (OpenCode, Crush) läser PLEUM_API_KEY — samma nyckel, sätt båda.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Röktest:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Du får ₩1 000 i gratis kredit vid registrering och en bonus på ₩5 000 vid din första påfyllning.

## Integrationer

| Kategori | Verktyg |
|---|---|
| [⚡ Enkommandolansering](#-pleum-cli--den-snabba-vägen) | `pleum`-CLI |
| [🤖 Terminalbaserade kodningsagenter](#-terminal--cli-agenter) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE-/GUI-agenter](#-ide--gui-agenter) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK:er](#-sdker) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 Multimodalt API](#-multimodalt--bild--ljud--video) | Bilder, TTS, STT, video, embeddingar |
| [🔌 Allt annat](#-fler-agenter) | OpenRouter-liknande ID:n, LiteLLM-proxy, 15+ fler agenter |

---

## ⚡ pleum CLI — den snabba vägen

Det officiella CLI:t startar din favoritagent redan uppkopplad mot PleumRouter. Inga konfigurationsfiler rörs.

```bash
npm install -g pleumrouter        # eller: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # webbläsarinloggning, nyckel utfärdas & sparas automatiskt
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # chatt-REPL i terminalen
pleum models                      # lista alla modeller med prissättning
```

Stöds för autostart: `claude` · `aider` · `codex` · `goose` · `openhands` (plus konfigurationssnuttar för `opencode` · `crush`). Dina befintliga verktygskonfigurationer ändras aldrig.

---

## 🤖 Terminal- / CLI-agenter

### Claude Code (Anthropic-kompatibel)

Claude Code och Claude Agent SDK-verktyg ansluter via den Anthropic-kompatibla `/v1/messages`-slutpunkten.

```bash
# ANTHROPIC_BASE_URL är ROTEN (utan /v1) — CLI:t lägger själv till /v1/messages.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# Det officiella CLI:t föredrar ANTHROPIC_API_KEY; sätt båda för säkerhets skull.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ Lägg **inte** till `/v1` i `ANTHROPIC_BASE_URL` — det blir `/v1/v1/messages` och misslyckas. Verktygsanrop och streaming fungerar helt och hållet, även när trafiken routas till OpenAI-kompatibla modeller.

### Codex CLI (Responses API)

Codex ansluter via OpenAI Responses API (`/v1/responses`); Chat Completions-vägen togs bort från Codex i februari 2026.

```toml
# ~/.codex/config.toml
# model / model_provider är nycklar på dokumentrotens nivå (måste stå ovanför [table]).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex lägger till /responses → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex stöder endast Responses API
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

# Goose / OpenHands: sätt prefixet openai/ framför modell-id:t
#   model = openai/gpt-4.1
```

### Gemini CLI

Gemini CLI från uppströms har svagt stöd för externa OpenAI-kompatibla slutpunkter; du kan behöva en OpenAI-kompatibel wrapper eller en fork.

---

## 🖥 IDE-/GUI-agenter

### Cline · Roo Code · Kilo Code · Cursor

Välj **OpenAI Compatible** (eller **Custom OpenAI**) som leverantör och klistra in:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Använd alltid **OpenAI Compatible-platsen** — den dedikerade OpenRouter-posten är hårdkodad till openrouter.ai och kommer att misslyckas. **Cursor** kräver `/v1` i bas-URL:en och ett icke-tomt nyckelfält. **Kilo Code** har ett känt problem (#681) där den anpassade bas-URL:en inte skickas vidare till modellistningen — ange modell-id:t manuellt.

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

Med `model: AUTODETECT` hämtar Continue modellistan automatiskt.

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

Fältnamnen kan variera beroende på Zed-version — kontrollera Zeds dokumentation.

---

## 📦 SDK:er

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
    base_url="https://router.pleum.ai",   # rot, utan /v1 — SDK:t lägger till /v1/messages
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # vilken PleumRouter-modell som helst fungerar
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Multimodalt — bild · ljud · video

Alla modaliteter är OpenAI-kompatibla HTTP-slutpunkter på samma nyckel. Välj en modell som stöder modaliteten från [`GET /v1/models`](https://pleum.ai/models).

```bash
# Bildgenerering
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Text-till-tal (returnerar ljuddata; kostnad i X-Cost-Krw-headern)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Tal-till-text (multipart-uppladdning)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# Videogenerering är asynkron: POST returnerar ett job_id, polla sedan GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### API-yta

| Slutpunkt | Protokoll |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (streaming, verktyg, vision) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Bildgenerering |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Asynkron video |
| `GET /v1/models` | Modellkatalog (offentlig) |
| `GET /v1/credits` | Saldo |

---

## 🔌 Fler agenter

De flesta agenter som inte listas här fungerar på samma sätt — sätt den OpenAI-kompatibla bas-URL:en:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** och fler.

Via den Anthropic-kompatibla `/v1/messages`: **claude-code-router** ansluter också med `ANTHROPIC_BASE_URL`.

**Modell-ID:n**: hitta dem via `GET /v1/models` eller på [modellsidan](https://pleum.ai/models). Cline, Continue, OpenCode och andra hämtar listan automatiskt. ID:n i OpenRouter-format (`openai/gpt-5.5`) konverteras automatiskt.

**LiteLLM-proxy** (Aider, OpenHands, Open Interpreter, SWE-agent och gptme är LiteLLM-baserade och ansluter direkt — men om du kör en LiteLLM-proxy):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # openai/-prefix → OpenAI-kompatibel rutt
      api_base: https://router.pleum.ai/v1           # lägg INTE till /chat/completions
      api_key: os.environ/PLEUM_API_KEY
```

---

## Bidra

Har du fått PleumRouter att fungera med ett verktyg som inte listas här? PR:ar välkomnas — lägg till ett avsnitt med en **testad** konfigurationssnutt (bas-URL, nyckel-env, modell-ID-format och eventuella fallgropar).

## Licens

[MIT](LICENSE)
