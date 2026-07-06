<div align="center">

# Cum se utilizează PleumRouter

**O singură cheie API pentru peste 200 de modele AI — compatibil OpenAI, facturat în KRW.**

[Website](https://pleum.ai) · [Documentație](https://pleum.ai/docs) · [Modele](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · Română · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter este un gateway AI: o singură cheie (`plm_…`), un singur URL de bază, peste 210 modele de la 18 furnizori — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE și altele. Comunică prin **OpenAI Chat Completions**, **Anthropic Messages** și **OpenAI Responses**, astfel încât aproape orice agent de codare, plugin IDE și SDK se conectează cu o singură modificare de configurare. Text, embeddings, imagine, voce și video — toate rulează prin aceeași cheie.

Acest depozit adună **rețete de integrare verificate**. Fiecare fragment de mai jos este testat pe gateway-ul live.

## Primii pași

1. [Înregistrează-te](https://pleum.ai/signup) → Dashboard → **API Keys** → emite o cheie (începe cu `plm_`).
2. Îndreaptă-ți instrumentul către URL-ul de bază:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Unii agenți (OpenCode, Crush) citesc PLEUM_API_KEY — aceeași cheie, setează-le pe amândouă.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Test rapid de funcționare:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Primești ₩1.000 credit gratuit la înregistrare și un bonus de ₩5.000 la prima reîncărcare.

## Integrări

| Categorie | Instrumente |
|---|---|
| [⚡ Lansator dintr-o comandă](#-cli-ul-pleum--calea-rapidă) | CLI `pleum` |
| [🤖 Agenți de codare din terminal](#-agenți-terminal--cli) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 Agenți IDE / GUI](#-agenți-ide--gui) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK-uri](#-sdk-uri) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 API multimodal](#-multimodal--imagine--audio--video) | Imagini, TTS, STT, Video, Embeddings |
| [🔌 Toate celelalte](#-alți-agenți) | ID-uri în stil OpenRouter, proxy LiteLLM, 15+ agenți suplimentari |

---

## ⚡ CLI-ul pleum — calea rapidă

CLI-ul oficial lansează agentul tău preferat deja conectat la PleumRouter. Niciun fișier de configurare nu este atins.

```bash
npm install -g pleumrouter        # sau: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # login din browser, cheia se emite și se salvează automat
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # REPL de chat în terminal
pleum models                      # listează toate modelele cu prețurile
```

Suportate pentru auto-lansare: `claude` · `aider` · `codex` · `goose` · `openhands` (plus fragmente de configurare pentru `opencode` · `crush`). Configurațiile existente ale instrumentelor tale nu sunt niciodată modificate.

---

## 🤖 Agenți terminal / CLI

### Claude Code (compatibil Anthropic)

Claude Code și instrumentele Claude Agent SDK se conectează prin endpoint-ul compatibil Anthropic `/v1/messages`.

```bash
# ANTHROPIC_BASE_URL este RĂDĂCINA (fără /v1) — CLI-ul adaugă singur /v1/messages.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# CLI-ul oficial preferă ANTHROPIC_API_KEY; setează-le pe amândouă pentru siguranță.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ **Nu** pune `/v1` în `ANTHROPIC_BASE_URL` — devine `/v1/v1/messages` și eșuează. Apelurile de instrumente (tool calls) și streaming-ul funcționează integral, chiar și atunci când sunt rutate către modele compatibile OpenAI.

### Codex CLI (Responses API)

Codex se conectează prin OpenAI Responses API (`/v1/responses`); calea Chat Completions a fost eliminată din Codex în februarie 2026.

```toml
# ~/.codex/config.toml
# model / model_provider sunt chei rădăcină ale documentului (trebuie să fie deasupra [table]).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex adaugă /responses → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex suportă doar Responses API
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
// opencode.json   (sau: /connect → Other)
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

# Goose / OpenHands: prefixează id-ul modelului cu openai/
#   model = openai/gpt-4.1
```

### Gemini CLI

Gemini CLI original are un suport slab pentru endpoint-uri externe compatibile OpenAI; s-ar putea să ai nevoie de un wrapper sau fork compatibil OpenAI.

---

## 🖥 Agenți IDE / GUI

### Cline · Roo Code · Kilo Code · Cursor

Selectează **OpenAI Compatible** (sau **Custom OpenAI**) ca furnizor și inserează:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Folosește întotdeauna **slotul OpenAI Compatible** — intrarea dedicată OpenRouter este codificată fix pe openrouter.ai și va eșua. **Cursor** necesită `/v1` în URL-ul de bază și un câmp de cheie ne-gol. **Kilo Code** are o problemă cunoscută (#681) în care URL-ul de bază personalizat nu este transmis către listarea modelelor — introdu id-ul modelului manual.

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

Cu `model: AUTODETECT`, Continue preia automat lista de modele.

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

Numele câmpurilor pot varia în funcție de versiunea Zed — verifică documentația Zed.

---

## 📦 SDK-uri

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
    base_url="https://router.pleum.ai",   # rădăcină, fără /v1 — SDK-ul adaugă /v1/messages
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # funcționează orice model PleumRouter
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Multimodal — imagine · audio · video

Toate modalitățile sunt endpoint-uri HTTP compatibile OpenAI pe aceeași cheie. Alege un model care suportă modalitatea respectivă din [`GET /v1/models`](https://pleum.ai/models).

```bash
# Generare de imagini
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Text-to-speech (returnează bytes audio; costul apare în header-ul X-Cost-Krw)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Speech-to-text (upload multipart)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# Generarea de video este asincronă: POST returnează un job_id, apoi interoghezi GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### Suprafața API

| Endpoint | Protocol |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (streaming, instrumente, viziune) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Generare de imagini |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Video asincron |
| `GET /v1/models` | Catalog de modele (public) |
| `GET /v1/credits` | Sold |

---

## 🔌 Alți agenți

Majoritatea agenților care nu sunt listați aici funcționează la fel — setează URL-ul de bază compatibil OpenAI:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** și altele.

Prin Anthropic-compatibil `/v1/messages`: **claude-code-router** se conectează de asemenea cu `ANTHROPIC_BASE_URL`.

**ID-urile modelelor**: le găsești la `GET /v1/models` sau pe [pagina de modele](https://pleum.ai/models). Cline, Continue, OpenCode și altele preiau lista automat. ID-urile în format OpenRouter (`openai/gpt-5.5`) sunt convertite automat.

**Proxy LiteLLM** (Aider, OpenHands, Open Interpreter, SWE-agent și gptme se bazează pe LiteLLM și se conectează direct — dar dacă păstrezi un proxy LiteLLM):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # prefixul openai/ → rută compatibilă OpenAI
      api_base: https://router.pleum.ai/v1           # NU adăuga /chat/completions
      api_key: os.environ/PLEUM_API_KEY
```

---

## Contribuții

Ai reușit să faci PleumRouter să funcționeze cu un instrument care nu este listat aici? PR-urile sunt binevenite — adaugă o secțiune cu un fragment de configurare **testat** (URL de bază, variabilă de mediu pentru cheie, formatul id-ului modelului și orice capcane întâlnite).

## Licență

[MIT](LICENSE)
