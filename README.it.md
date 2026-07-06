<div align="center">

# Come usare PleumRouter

**Una chiave API per oltre 200 modelli AI — compatibile con OpenAI, fatturata in KRW.**

[Sito web](https://pleum.ai) · [Documentazione](https://pleum.ai/docs) · [Modelli](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · Italiano · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter è un gateway AI: una chiave (`plm_…`), un solo URL di base, oltre 210 modelli da 18 provider — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE e altri. Supporta **OpenAI Chat Completions**, **Anthropic Messages** e **OpenAI Responses**, quindi quasi tutti gli agenti di coding, i plugin per IDE e gli SDK si collegano con una modifica di configurazione di una sola riga. Testo, embedding, immagini, audio e video passano tutti attraverso la stessa chiave.

Questo repository raccoglie **ricette di integrazione verificate**. Ogni snippet qui sotto è testato sul gateway live.

## Per iniziare

1. [Registrati](https://pleum.ai/signup) → Dashboard → **API Keys** → genera una chiave (inizia con `plm_`).
2. Punta il tuo strumento all'URL di base:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Alcuni agenti (OpenCode, Crush) leggono PLEUM_API_KEY — stessa chiave, impostale entrambe.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Test rapido:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Ricevi ₩1.000 di credito gratuito alla registrazione e un bonus di ₩5.000 alla prima ricarica.

## Integrazioni

| Categoria | Strumenti |
|---|---|
| [⚡ Launcher a un comando](#-pleum-cli--il-percorso-rapido) | CLI `pleum` |
| [🤖 Agenti di coding da terminale](#-agenti-terminale--cli) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 Agenti IDE / GUI](#-agenti-ide--gui) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK](#-sdk) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 API multimodale](#-multimodale--immagini--audio--video) | Immagini, TTS, STT, Video, Embedding |
| [🔌 Tutto il resto](#-altri-agenti) | ID in stile OpenRouter, proxy LiteLLM, oltre 15 altri agenti |

---

## ⚡ pleum CLI — il percorso rapido

La CLI ufficiale avvia il tuo agente preferito già collegato a PleumRouter. Nessun file di configurazione viene toccato.

```bash
npm install -g pleumrouter        # oppure: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # login da browser, chiave generata e salvata automaticamente
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # REPL di chat da terminale
pleum models                      # elenca tutti i modelli con i relativi prezzi
```

Supportati per l'avvio automatico: `claude` · `aider` · `codex` · `goose` · `openhands` (più snippet di configurazione per `opencode` · `crush`). Le configurazioni dei tuoi strumenti esistenti non vengono mai modificate.

---

## 🤖 Agenti terminale / CLI

### Claude Code (compatibile Anthropic)

Claude Code e gli strumenti Claude Agent SDK si collegano tramite l'endpoint compatibile Anthropic `/v1/messages`.

```bash
# ANTHROPIC_BASE_URL è la RADICE (senza /v1) — la CLI aggiunge da sé /v1/messages.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# La CLI ufficiale preferisce ANTHROPIC_API_KEY; impostale entrambe per sicurezza.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ **Non** inserire `/v1` in `ANTHROPIC_BASE_URL` — diventerebbe `/v1/v1/messages` e fallirebbe. Le chiamate a strumenti (tool call) e lo streaming funzionano end-to-end, anche quando instradati verso modelli compatibili OpenAI.

### Codex CLI (Responses API)

Codex si collega tramite la OpenAI Responses API (`/v1/responses`); il percorso Chat Completions è stato rimosso da Codex a febbraio 2026.

```toml
# ~/.codex/config.toml
# model / model_provider sono chiavi alla radice del documento (devono stare sopra la [tabella]).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex aggiunge /responses → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex supporta solo la Responses API
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
// opencode.json   (oppure: /connect → Other)
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

# Goose / OpenHands: fai precedere l'id del modello dal prefisso openai/
#   model = openai/gpt-4.1
```

### Gemini CLI

Il Gemini CLI upstream ha un supporto limitato per endpoint esterni compatibili OpenAI; potrebbe servirti un wrapper o un fork compatibile OpenAI.

---

## 🖥 Agenti IDE / GUI

### Cline · Roo Code · Kilo Code · Cursor

Seleziona **OpenAI Compatible** (o **Custom OpenAI**) come provider e incolla:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Usa sempre lo **slot OpenAI Compatible** — la voce dedicata a OpenRouter è cablata su openrouter.ai e fallirà. **Cursor** richiede `/v1` nell'URL di base e un campo chiave non vuoto. **Kilo Code** ha un problema noto (#681) per cui l'URL di base personalizzato non viene passato all'elenco dei modelli — inserisci l'ID del modello manualmente.

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

Con `model: AUTODETECT` Continue recupera automaticamente l'elenco dei modelli.

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

I nomi dei campi possono variare a seconda della versione di Zed — controlla la documentazione di Zed.

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
    base_url="https://router.pleum.ai",   # radice, senza /v1 — l'SDK aggiunge /v1/messages
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # funziona con qualsiasi modello PleumRouter
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Multimodale — immagini · audio · video

Tutte le modalità sono endpoint HTTP compatibili OpenAI sulla stessa chiave. Scegli un modello che supporti la modalità desiderata da [`GET /v1/models`](https://pleum.ai/models).

```bash
# Generazione di immagini
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Sintesi vocale (text-to-speech; restituisce byte audio; costo nell'header X-Cost-Krw)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Riconoscimento vocale (speech-to-text; upload multipart)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# La generazione video è asincrona: la POST restituisce un job_id, poi interroga GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### Superficie API

| Endpoint | Protocollo |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (streaming, strumenti, visione) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Generazione di immagini |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Video asincrono |
| `GET /v1/models` | Catalogo modelli (pubblico) |
| `GET /v1/credits` | Saldo |

---

## 🔌 Altri agenti

La maggior parte degli agenti non elencati qui funziona allo stesso modo — imposta l'URL di base compatibile OpenAI:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** e altri.

Tramite l'endpoint compatibile Anthropic `/v1/messages`: anche **claude-code-router** si collega con `ANTHROPIC_BASE_URL`.

**ID dei modelli**: trovali su `GET /v1/models` o sulla [pagina dei modelli](https://pleum.ai/models). Cline, Continue, OpenCode e altri recuperano l'elenco automaticamente. Gli ID in formato OpenRouter (`openai/gpt-5.5`) vengono convertiti automaticamente.

**Proxy LiteLLM** (Aider, OpenHands, Open Interpreter, SWE-agent e gptme si basano su LiteLLM e si collegano direttamente — ma se mantieni un proxy LiteLLM):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # prefisso openai/ → rotta compatibile OpenAI
      api_base: https://router.pleum.ai/v1           # NON aggiungere /chat/completions
      api_key: os.environ/PLEUM_API_KEY
```

---

## Contribuire

Hai fatto funzionare PleumRouter con uno strumento non elencato qui? Le PR sono benvenute — aggiungi una sezione con uno snippet di configurazione **testato** (URL di base, variabile d'ambiente della chiave, formato dell'ID modello ed eventuali insidie).

## Licenza

[MIT](LICENSE)
