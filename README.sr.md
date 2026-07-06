<div align="center">

# Kako koristiti PleumRouter

**Jedan API ključ za 200+ AI modela — kompatibilno sa OpenAI, naplata u KRW.**

[Sajt](https://pleum.ai) · [Dokumentacija](https://pleum.ai/docs) · [Modeli](https://pleum.ai/models) · [Plejgraund](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · Српски · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter je AI gejtvej: jedan ključ (`plm_…`), jedan bazni URL, 210+ modela od 18 provajdera — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE i drugi. Podržava **OpenAI Chat Completions**, **Anthropic Messages** i **OpenAI Responses**, tako da se skoro svaki kodirajući agent, IDE dodatak i SDK povezuje uz izmenu konfiguracije od samo jedne linije. Tekst, embedinzi, slika, govor i video — sve to radi preko istog ključa.

Ovaj repozitorijum sadrži **verifikovane recepte za integraciju**. Svaki isečak koda ispod je testiran nad živim gejtvejom.

## Prvi koraci

1. [Registrujte se](https://pleum.ai/signup) → Kontrolna tabla → **API Keys** → izdajte ključ (počinje sa `plm_`).
2. Usmerite svoj alat na bazni URL:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Neki agenti (OpenCode, Crush) čitaju PLEUM_API_KEY — isti ključ, postavite oba.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Provera ispravnosti:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Dobijate ₩1.000 besplatnog kredita prilikom registracije i bonus od ₩5.000 pri prvoj dopuni.

## Integracije

| Kategorija | Alati |
|---|---|
| [⚡ Pokretač jednom komandom](#-pleum-cli--najbrži-put) | `pleum` CLI |
| [🤖 Terminalski kodirajući agenti](#-terminal--cli-agenti) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE / GUI agenti](#-ide--gui-agenti) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK-ovi](#-sdk-ovi) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 Multimodalni API](#-multimodalno--slika--audio--video) | Slike, TTS, STT, Video, Embedinzi |
| [🔌 Sve ostalo](#-više-agenata) | ID-jevi u stilu OpenRouter-a, LiteLLM proksi, 15+ dodatnih agenata |

---

## ⚡ pleum CLI — najbrži put

Zvanični CLI pokreće vaš omiljeni agent koji je već povezan sa PleumRouter-om. Nijedan konfiguracioni fajl se ne dira.

```bash
npm install -g pleumrouter        # ili: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # prijava kroz pregledač, ključ se automatski izdaje i čuva
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # terminalski REPL za ćaskanje
pleum models                      # prikaz svih modela sa cenama
```

Podržano za automatsko pokretanje: `claude` · `aider` · `codex` · `goose` · `openhands` (plus konfiguracioni isečci za `opencode` · `crush`). Vaše postojeće konfiguracije alata se nikada ne menjaju.

---

## 🤖 Terminal / CLI agenti

### Claude Code (kompatibilno sa Anthropic-om)

Claude Code i alati Claude Agent SDK-a povezuju se preko krajnje tačke `/v1/messages`, kompatibilne sa Anthropic-om.

```bash
# ANTHROPIC_BASE_URL je KOREN (bez /v1) — CLI sam dodaje /v1/messages.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# Zvanični CLI daje prednost ANTHROPIC_API_KEY; postavite oba radi sigurnosti.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ **Nemojte** stavljati `/v1` u `ANTHROPIC_BASE_URL` — to postaje `/v1/v1/messages` i ne radi. Pozivi alata i strimovanje rade od početka do kraja, čak i kada su usmereni ka modelima kompatibilnim sa OpenAI-om.

### Codex CLI (Responses API)

Codex se povezuje preko OpenAI Responses API-ja (`/v1/responses`); putanja Chat Completions je uklonjena iz Codex-a u februaru 2026.

```toml
# ~/.codex/config.toml
# model / model_provider su ključevi na korenu dokumenta (moraju biti iznad [table]).
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

# Goose / OpenHands: dodajte prefiks openai/ ispred ID-ja modela
#   model = openai/gpt-4.1
```

### Gemini CLI

Zvanični (upstream) Gemini CLI ima slabu podršku za spoljne krajnje tačke kompatibilne sa OpenAI-om; možda će vam biti potreban omotač (wrapper) ili fork kompatibilan sa OpenAI-om.

---

## 🖥 IDE / GUI agenti

### Cline · Roo Code · Kilo Code · Cursor

Izaberite **OpenAI Compatible** (ili **Custom OpenAI**) kao provajdera i nalepite:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Uvek koristite **slot OpenAI Compatible** — namenski unos za OpenRouter je fiksno vezan za openrouter.ai i neće raditi. **Cursor** zahteva `/v1` u baznom URL-u i neprazno polje za ključ. **Kilo Code** ima poznat problem (#681) gde se prilagođeni bazni URL ne prosleđuje pri listanju modela — unesite ID modela ručno.

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

Uz `model: AUTODETECT`, Continue automatski povlači listu modela.

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

Nazivi polja mogu varirati u zavisnosti od verzije Zed-a — proverite dokumentaciju Zed-a.

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
    base_url="https://router.pleum.ai",   # koren, bez /v1 — SDK sam dodaje /v1/messages
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # radi bilo koji model PleumRouter-a
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Multimodalno — slika · audio · video

Sve modalitete su HTTP krajnje tačke kompatibilne sa OpenAI-om, na istom ključu. Izaberite model koji podržava dati modalitet sa [`GET /v1/models`](https://pleum.ai/models).

```bash
# Generisanje slike
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Pretvaranje teksta u govor (vraća audio bajtove; trošak je u zaglavlju X-Cost-Krw)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Pretvaranje govora u tekst (multipart otpremanje)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# Generisanje videa je asinhrono: POST vraća job_id, zatim se poziva GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### API površina

| Krajnja tačka | Protokol |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (strimovanje, alati, vizuelni unos) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Generisanje slike |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Asinhroni video |
| `GET /v1/models` | Katalog modela (javan) |
| `GET /v1/credits` | Stanje |

---

## 🔌 Više agenata

Većina agenata koji ovde nisu navedeni radi na isti način — postavite bazni URL kompatibilan sa OpenAI-om:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** i drugi.

Preko krajnje tačke `/v1/messages`, kompatibilne sa Anthropic-om: **claude-code-router** se takođe povezuje pomoću `ANTHROPIC_BASE_URL`.

**ID-jevi modela**: pronađite ih na `GET /v1/models` ili na [stranici modela](https://pleum.ai/models). Cline, Continue, OpenCode i drugi automatski preuzimaju listu. ID-jevi u formatu OpenRouter-a (`openai/gpt-5.5`) se automatski konvertuju.

**LiteLLM proksi** (Aider, OpenHands, Open Interpreter, SWE-agent i gptme su bazirani na LiteLLM-u i povezuju se direktno — ali ukoliko koristite LiteLLM proksi):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # prefiks openai/ → ruta kompatibilna sa OpenAI-om
      api_base: https://router.pleum.ai/v1           # NE dodavati /chat/completions
      api_key: os.environ/PLEUM_API_KEY
```

---

## Doprinos

Uspeli ste da pokrenete PleumRouter sa alatom koji ovde nije naveden? Pull request-ovi su dobrodošli — dodajte sekciju sa **testiranim** konfiguracionim isečkom (bazni URL, promenljiva okruženja za ključ, format ID-ja modela i eventualne zamke).

## Licenca

[MIT](LICENSE)
