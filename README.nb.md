<div align="center">

# Slik bruker du PleumRouter

**Én API-nøkkel for 200+ AI-modeller — OpenAI-kompatibel, fakturert i KRW.**

[Nettside](https://pleum.ai) · [Dokumentasjon](https://pleum.ai/docs) · [Modeller](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · Norsk · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter er en AI-gateway: én nøkkel (`plm_…`), én base-URL, 210+ modeller fra 18 leverandører — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE og flere. Den snakker **OpenAI Chat Completions**, **Anthropic Messages** og **OpenAI Responses**, så nesten enhver kodeagent, IDE-plugin og SDK kobler til med én enkelt konfigurasjonsendring. Tekst, embeddings, bilde, tale og video kjører alle gjennom samme nøkkel.

Dette repoet samler **verifiserte integrasjonsoppskrifter**. Hvert kodeeksempel nedenfor er testet mot den live gatewayen.

## Kom i gang

1. [Registrer deg](https://pleum.ai/signup) → Dashboard → **API-nøkler** → utsted en nøkkel (starter med `plm_`).
2. Pek verktøyet ditt mot base-URL-en:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Enkelte agenter (OpenCode, Crush) leser PLEUM_API_KEY — samme nøkkel, sett begge.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Røyktest:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Du får ₩1.000 gratis kreditt ved registrering og en bonus på ₩5.000 ved din første påfylling.

## Integrasjoner

| Kategori | Verktøy |
|---|---|
| [⚡ Ett-kommando-launcher](#-pleum-cli--raskeste-vei) | `pleum` CLI |
| [🤖 Terminal-kodeagenter](#-terminal--cli-agenter) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE-/GUI-agenter](#-ide--gui-agenter) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK-er](#-sdk-er) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 Multimodal API](#-multimodal--bilde--lyd--video) | Bilder, TTS, STT, video, embeddings |
| [🔌 Alt annet](#-flere-agenter) | OpenRouter-stil IDer, LiteLLM-proxy, 15+ flere agenter |

---

## ⚡ pleum CLI — raskeste vei

Den offisielle CLI-en starter favorittagenten din allerede koblet til PleumRouter. Ingen konfigurasjonsfiler blir rørt.

```bash
npm install -g pleumrouter        # eller: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # nettleserinnlogging, nøkkel utstedes & lagres automatisk
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # terminal-chat-REPL
pleum models                      # list alle modeller med priser
```

Støttet for auto-launch: `claude` · `aider` · `codex` · `goose` · `openhands` (pluss konfigurasjonssnutter for `opencode` · `crush`). De eksisterende verktøykonfigurasjonene dine blir aldri endret.

---

## 🤖 Terminal / CLI-agenter

### Claude Code (Anthropic-kompatibel)

Claude Code og Claude Agent SDK-verktøy kobler til via det Anthropic-kompatible `/v1/messages`-endepunktet.

```bash
# ANTHROPIC_BASE_URL er ROTEN (uten /v1) — CLI-en legger selv til /v1/messages.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# Den offisielle CLI-en foretrekker ANTHROPIC_API_KEY; sett begge for sikkerhets skyld.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ Ikke sett `/v1` i `ANTHROPIC_BASE_URL` — det blir da `/v1/v1/messages` og feiler. Verktøykall og streaming fungerer fullt ut, selv når det rutes til OpenAI-kompatible modeller.

### Codex CLI (Responses API)

Codex kobler til via OpenAI Responses API (`/v1/responses`); Chat Completions-stien ble fjernet fra Codex i februar 2026.

```toml
# ~/.codex/config.toml
# model / model_provider er nøkler på dokumentroten (må stå over [table]).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex legger til /responses → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex støtter kun Responses API
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

# Goose / OpenHands: sett prefikset openai/ foran modell-IDen
#   model = openai/gpt-4.1
```

### Gemini CLI

Den originale Gemini CLI-en har svak støtte for eksterne OpenAI-kompatible endepunkter; du trenger kanskje en OpenAI-kompatibel wrapper eller fork.

---

## 🖥 IDE / GUI-agenter

### Cline · Roo Code · Kilo Code · Cursor

Velg **OpenAI Compatible** (eller **Custom OpenAI**) som leverandør og lim inn:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Bruk alltid **OpenAI Compatible-plassen** — den dedikerte OpenRouter-oppføringen er hardkodet til openrouter.ai og vil feile. **Cursor** krever `/v1` i base-URL-en og et ikke-tomt nøkkelfelt. **Kilo Code** har en kjent feil (#681) der den egendefinerte base-URL-en ikke sendes videre til modell-listingen — skriv inn modell-IDen manuelt.

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

Med `model: AUTODETECT` henter Continue modell-listen automatisk.

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

Feltnavn kan variere mellom Zed-versjoner — sjekk Zed-dokumentasjonen.

---

## 📦 SDK-er

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
    base_url="https://router.pleum.ai",   # rot, uten /v1 — SDK-en legger til /v1/messages
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # enhver PleumRouter-modell fungerer
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Multimodal — bilde · lyd · video

Alle modaliteter er OpenAI-kompatible HTTP-endepunkter på samme nøkkel. Velg en modell som støtter modaliteten fra [`GET /v1/models`](https://pleum.ai/models).

```bash
# Bildegenerering
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Tekst-til-tale (returnerer lydbytes; kostnad i X-Cost-Krw-header)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Tale-til-tekst (multipart-opplasting)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# Videogenerering er asynkron: POST returnerer en job_id, deretter poll GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### API-overflate

| Endepunkt | Protokoll |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (streaming, verktøy, syn) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Bildegenerering |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Asynkron video |
| `GET /v1/models` | Modellkatalog (offentlig) |
| `GET /v1/credits` | Saldo |

---

## 🔌 Flere agenter

De fleste agenter som ikke er listet her fungerer på samme måte — sett den OpenAI-kompatible base-URL-en:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** og flere.

Via Anthropic-kompatibel `/v1/messages`: **claude-code-router** kobler også til med `ANTHROPIC_BASE_URL`.

**Modell-IDer**: finn dem på `GET /v1/models` eller på [modellsiden](https://pleum.ai/models). Cline, Continue, OpenCode og andre henter listen automatisk. IDer i OpenRouter-format (`openai/gpt-5.5`) konverteres automatisk.

**LiteLLM-proxy** (Aider, OpenHands, Open Interpreter, SWE-agent og gptme er LiteLLM-baserte og kobler til direkte — men hvis du beholder en LiteLLM-proxy):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # openai/-prefiks → OpenAI-kompatibel rute
      api_base: https://router.pleum.ai/v1           # ikke legg til /chat/completions
      api_key: os.environ/PLEUM_API_KEY
```

---

## Bidra

Fikk du PleumRouter til å fungere med et verktøy som ikke er listet her? PR-er er velkomne — legg til en seksjon med en **testet** konfigurasjonssnutt (base-URL, nøkkel-env, modell-ID-format og eventuelle fallgruver).

## Lisens

[MIT](LICENSE)
