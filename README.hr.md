<div align="center">

# Kako koristiti PleumRouter

**Jedan API ključ za 200+ AI modela — kompatibilno s OpenAI-jem, naplata u KRW.**

[Website](https://pleum.ai) · [Docs](https://pleum.ai/docs) · [Models](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · Hrvatski · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter je AI pristupnik (gateway): jedan ključ (`plm_…`), jedan bazni URL, 210+ modela od 18 pružatelja usluga — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE i drugi. Podržava **OpenAI Chat Completions**, **Anthropic Messages** i **OpenAI Responses**, tako da se gotovo svaki agent za kodiranje, IDE dodatak i SDK povezuje uz izmjenu konfiguracije od samo jedne linije. Tekst, ugradbeni vektori (embeddings), slika, govor i video — sve prolazi kroz isti ključ.

Ovaj repozitorij okuplja **provjerene recepte za integraciju**. Svaki isječak koda ispod testiran je uz aktivni (live) pristupnik.

## Početak rada

1. [Registrirajte se](https://pleum.ai/signup) → Dashboard → **API Keys** → izdajte ključ (počinje s `plm_`).
2. Usmjerite svoj alat na bazni URL:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Neki agenti (OpenCode, Crush) čitaju PLEUM_API_KEY — isti ključ, postavite oba.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Test ispravnosti (smoke test):

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Prilikom registracije dobivate ₩1.000 besplatnog kredita, a uz prvu uplatu bonus od ₩5.000.

## Integracije

| Kategorija | Alati |
|---|---|
| [⚡ Pokretač jednom naredbom](#-pleum-cli--brzi-put) | `pleum` CLI |
| [🤖 Terminalski agenti za kodiranje](#-terminalski--cli-agenti) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE / GUI agenti](#-ide--gui-agenti) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK-ovi](#-sdk-ovi) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 Multimodalni API](#-multimodalno--slika--audio--video) | Slike, TTS, STT, video, ugradbeni vektori |
| [🔌 Sve ostalo](#-ostali-agenti) | ID-ovi u stilu OpenRoutera, LiteLLM proxy, 15+ dodatnih agenata |

---

## ⚡ pleum CLI — brzi put

Službeni CLI pokreće vašeg omiljenog agenta već povezanog s PleumRouterom. Bez diranja konfiguracijskih datoteka.

```bash
npm install -g pleumrouter        # ili: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # prijava putem preglednika, ključ se automatski izdaje i sprema
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # terminalski chat REPL
pleum models                      # popis svih modela s cijenama
```

Podržano za automatsko pokretanje: `claude` · `aider` · `codex` · `goose` · `openhands` (uz konfiguracijske isječke za `opencode` · `crush`). Vaše postojeće konfiguracije alata nikad se ne mijenjaju.

---

## 🤖 Terminalski / CLI agenti

### Claude Code (kompatibilno s Anthropicom)

Claude Code i alati Claude Agent SDK povezuju se putem krajnje točke `/v1/messages`, kompatibilne s Anthropicom.

```bash
# ANTHROPIC_BASE_URL je KORIJEN (bez /v1) — CLI sam dodaje /v1/messages.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# Službeni CLI preferira ANTHROPIC_API_KEY; radi sigurnosti postavite oba.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ **Nemojte** stavljati `/v1` u `ANTHROPIC_BASE_URL` — postaje `/v1/v1/messages` i ne radi. Pozivi alata (tool calls) i streaming rade od početka do kraja, čak i kad se usmjeravaju na modele kompatibilne s OpenAI-jem.

### Codex CLI (Responses API)

Codex se povezuje putem OpenAI Responses API-ja (`/v1/responses`); put preko Chat Completions uklonjen je iz Codexa u veljači 2026.

```toml
# ~/.codex/config.toml
# model / model_provider su ključevi na korijenu dokumenta (moraju biti iznad [tablice]).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex dodaje /responses → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex podržava samo Responses API
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
// opencode.json   (ili: /connect → Other)
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

# Goose / OpenHands: ID modela treba imati prefiks openai/
#   model = openai/gpt-4.1
```

### Gemini CLI

Izvorni (upstream) Gemini CLI ima slabu podršku za vanjske krajnje točke kompatibilne s OpenAI-jem; možda će vam trebati omotač (wrapper) ili fork kompatibilan s OpenAI-jem.

---

## 🖥 IDE / GUI agenti

### Cline · Roo Code · Kilo Code · Cursor

Odaberite **OpenAI Compatible** (ili **Custom OpenAI**) kao pružatelja usluge i zalijepite:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Uvijek koristite **utor OpenAI Compatible** — namjenski unos za OpenRouter tvrdo je kodiran na openrouter.ai i neće raditi. **Cursor** zahtijeva `/v1` u baznom URL-u i neprazno polje za ključ. **Kilo Code** ima poznatu grešku (#681) gdje se prilagođeni bazni URL ne prosljeđuje pri dohvatu popisa modela — unesite ID modela ručno.

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

Uz `model: AUTODETECT` Continue automatski povlači popis modela.

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

Nazivi polja mogu varirati ovisno o verziji Zeda — provjerite dokumentaciju Zeda.

---

## 📦 SDK-ovi

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
    base_url="https://router.pleum.ai",   # korijen, bez /v1 — SDK dodaje /v1/messages
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # radi bilo koji model PleumRoutera
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Multimodalno — slika · audio · video

Sve modalitete predstavljaju HTTP krajnje točke kompatibilne s OpenAI-jem na istom ključu. Odaberite model koji podržava dani modalitet putem [`GET /v1/models`](https://pleum.ai/models).

```bash
# Generiranje slika
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Pretvorba teksta u govor (vraća audio bajtove; trošak u zaglavlju X-Cost-Krw)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Pretvorba govora u tekst (multipart prijenos)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# Generiranje videa je asinkrono: POST vraća job_id, zatim se poziva GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### API površina

| Krajnja točka | Protokol |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (streaming, alati, vid) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Generiranje slika |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Asinkroni video |
| `GET /v1/models` | Katalog modela (javan) |
| `GET /v1/credits` | Stanje kredita |

---

## 🔌 Ostali agenti

Većina agenata koji ovdje nisu navedeni radi na isti način — postavite bazni URL kompatibilan s OpenAI-jem:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** i drugi.

Putem `/v1/messages` kompatibilnog s Anthropicom: **claude-code-router** također se povezuje uz `ANTHROPIC_BASE_URL`.

**ID-ovi modela**: pronađite ih putem `GET /v1/models` ili na [stranici modela](https://pleum.ai/models). Cline, Continue, OpenCode i drugi automatski dohvaćaju popis. ID-ovi u OpenRouter formatu (`openai/gpt-5.5`) automatski se pretvaraju.

**LiteLLM proxy** (Aider, OpenHands, Open Interpreter, SWE-agent i gptme temelje se na LiteLLM-u i povezuju se izravno — ali ako održavate LiteLLM proxy):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # prefiks openai/ → ruta kompatibilna s OpenAI-jem
      api_base: https://router.pleum.ai/v1           # NEMOJTE dodavati /chat/completions
      api_key: os.environ/PLEUM_API_KEY
```

---

## Doprinosi

Uspjeli ste pokrenuti PleumRouter s alatom koji ovdje nije naveden? PR-ovi su dobrodošli — dodajte odjeljak s **testiranim** konfiguracijskim isječkom (bazni URL, varijabla okruženja za ključ, format ID-a modela i eventualne zamke).

## Licenca

[MIT](LICENSE)
