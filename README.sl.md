<div align="center">

# Kako uporabljati PleumRouter

**En API ključ za 200+ modelov UI — združljiv z OpenAI, obračunano v KRW.**

[Spletna stran](https://pleum.ai) · [Dokumentacija](https://pleum.ai/docs) · [Modeli](https://pleum.ai/models) · [Igrišče](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · Slovenščina · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter je prehod UI (AI gateway): en ključ (`plm_…`), en osnovni URL, 210+ modelov 18 ponudnikov — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE in drugi. Govori **OpenAI Chat Completions**, **Anthropic Messages** in **OpenAI Responses**, zato se skoraj vsak kodirni agent, vtičnik za IDE in SDK poveže z eno vrstico spremembe konfiguracije. Besedilo, vdelave (embeddings), slika, govor in video vsi tečejo prek istega ključa.

Ta repozitorij zbira **preverjene recepte za integracijo**. Vsak spodnji izsek je testiran na živem prehodu.

## Kako začeti

1. [Registrirajte se](https://pleum.ai/signup) → Nadzorna plošča → **API-ključi** → izdajte ključ (se začne s `plm_`).
2. Usmerite svoje orodje na osnovni URL:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Some agents (OpenCode, Crush) read PLEUM_API_KEY — same key, set both.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Preizkus delovanja:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Ob registraciji dobite ₩1.000 brezplačnega dobroimetja in bonus ₩5.000 ob prvem dopolnilu.

## Integracije

| Kategorija | Orodja |
|---|---|
| [⚡ Zaganjalnik z enim ukazom](#-pleum-cli--hitra-pot) | ukaz `pleum` |
| [🤖 Terminalski kodirni agenti](#-terminalski--cli-agenti) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 Agenti za IDE / GUI](#-agenti-za-ide--gui) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK-ji](#-sdk-ji) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 Multimodalni API](#-multimodalno--slika--zvok--video) | Slike, TTS, STT, video, vdelave (embeddings) |
| [🔌 Vse ostalo](#-več-agentov) | ID-ji v slogu OpenRouter, proxy LiteLLM, 15+ drugih agentov |

---

## ⚡ pleum CLI — hitra pot

Uradni CLI zažene vaš najljubši agent, ki je že povezan s PleumRouter. Nobene konfiguracijske datoteke se ne dotakne.

```bash
npm install -g pleumrouter        # or: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # browser login, key auto-issued & saved
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # terminal chat REPL
pleum models                      # list all models with pricing
```

Podprto za samodejni zagon: `claude` · `aider` · `codex` · `goose` · `openhands` (poleg tega izseki konfiguracije za `opencode` · `crush`). Vaše obstoječe konfiguracije orodij niso nikoli spremenjene.

---

## 🤖 Terminalski / CLI agenti

### Claude Code (združljiv z Anthropic)

Claude Code in orodja Claude Agent SDK se povežejo prek z Anthropic združljive končne točke `/v1/messages`.

```bash
# ANTHROPIC_BASE_URL is the ROOT (no /v1) — the CLI appends /v1/messages itself.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# The official CLI prefers ANTHROPIC_API_KEY; set both to be safe.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ Nikoli ne dodajte `/v1` v `ANTHROPIC_BASE_URL` — postane `/v1/v1/messages` in ne deluje. Klici orodij (tool calls) in pretakanje (streaming) delujejo od konca do konca, tudi kadar so usmerjeni na modele, združljive z OpenAI.

### Codex CLI (Responses API)

Codex se poveže prek API-ja OpenAI Responses (`/v1/responses`); pot Chat Completions je bila iz Codexa odstranjena februarja 2026.

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

Uradni Gemini CLI ima šibko podporo za zunanje z OpenAI združljive končne točke; morda boste potrebovali ovojnico (wrapper) ali razvejitev (fork), združljivo z OpenAI.

---

## 🖥 Agenti za IDE / GUI

### Cline · Roo Code · Kilo Code · Cursor

Izberite **OpenAI Compatible** (ali **Custom OpenAI**) kot ponudnika in prilepite:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Vedno uporabite **režo OpenAI Compatible** — namenski vnos za OpenRouter je trdo kodiran na openrouter.ai in ne bo deloval. **Cursor** zahteva `/v1` v osnovnem URL-ju in neprazno polje za ključ. **Kilo Code** ima znano težavo (#681), kjer se poljubni osnovni URL ne posreduje pri izpisu seznama modelov — vnesite ID modela ročno.

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

Z nastavitvijo `model: AUTODETECT` Continue samodejno pridobi seznam modelov.

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

Imena polj se lahko razlikujejo glede na različico Zed — preverite dokumentacijo Zed.

---

## 📦 SDK-ji

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

## 🎨 Multimodalno — slika · zvok · video

Vse modalnosti so HTTP končne točke, združljive z OpenAI, na istem ključu. Izberite model, ki podpira določeno modalnost, na [`GET /v1/models`](https://pleum.ai/models).

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

### Površina API

| Končna točka | Protokol |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (pretakanje, orodja, vid) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Generiranje slik |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Asinhroni video |
| `GET /v1/models` | Katalog modelov (javni) |
| `GET /v1/credits` | Dobroimetje |

---

## 🔌 Več agentov

Večina agentov, ki tukaj niso navedeni, deluje enako — nastavite osnovni URL, združljiv z OpenAI:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** in drugi.

Prek z Anthropic združljive poti `/v1/messages`: tudi **claude-code-router** se poveže z `ANTHROPIC_BASE_URL`.

**ID-ji modelov**: najdete jih na `GET /v1/models` ali na [strani z modeli](https://pleum.ai/models). Cline, Continue, OpenCode in drugi seznam pridobijo samodejno. ID-ji v formatu OpenRouter (`openai/gpt-5.5`) se pretvorijo samodejno.

**Proxy LiteLLM** (Aider, OpenHands, Open Interpreter, SWE-agent in gptme temeljijo na LiteLLM in se povežejo neposredno — če pa vzdržujete proxy LiteLLM):

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

## Prispevanje

Ste PleumRouter spravili v delovanje z orodjem, ki tukaj ni navedeno? Zahteve za združitev (PR) so dobrodošle — dodajte razdelek s **preizkušenim** izsekom konfiguracije (osnovni URL, spremenljivka okolja za ključ, format ID-ja modela in morebitne pasti).

## Licenca

[MIT](LICENSE)
