<div align="center">

# Ako používať PleumRouter

**Jeden API kľúč pre 200+ modelov AI — kompatibilný s OpenAI, fakturovaný v KRW.**

[Webová stránka](https://pleum.ai) · [Dokumentácia](https://pleum.ai/docs) · [Modely](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · Slovenčina · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter je brána AI: jeden kľúč (`plm_…`), jedna základná URL adresa, 210+ modelov od 18 poskytovateľov — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE a ďalšie. Podporuje **OpenAI Chat Completions**, **Anthropic Messages** a **OpenAI Responses**, takže takmer každý kódovací agent, doplnok IDE a SDK sa pripojí jednoduchou úpravou konfigurácie. Text, embeddingy, obrázky, reč a video — všetko beží cez ten istý kľúč.

Tento repozitár zhromažďuje **overené integračné recepty**. Každý úryvok nižšie je otestovaný oproti živej bráne.

## Ako začať

1. [Zaregistrujte sa](https://pleum.ai/signup) → Dashboard → **API Keys** → vygenerujte kľúč (začína na `plm_`).
2. Nasmerujte svoj nástroj na základnú URL adresu:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Niektorí agenti (OpenCode, Crush) čítajú PLEUM_API_KEY — rovnaký kľúč, nastavte oba.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Skúšobný test:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Pri registrácii získate ₩1,000 kreditu zdarma a bonus ₩5,000 pri prvom dobití.

## Integrácie

| Kategória | Nástroje |
|---|---|
| [⚡ Spúšťač jedným príkazom](#-pleum-cli--rýchla-cesta) | `pleum` CLI |
| [🤖 Terminálové kódovacie agenty](#-terminálové--cli-agenty) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE / GUI agenty](#-ide--gui-agenty) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK](#-sdk) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 Multimodálne API](#-multimodálne--obrázky--zvuk--video) | Obrázky, TTS, STT, Video, Embeddingy |
| [🔌 Všetko ostatné](#-ďalší-agenti) | ID v štýle OpenRouter, LiteLLM proxy, 15+ ďalších agentov |

---

## ⚡ pleum CLI — rýchla cesta

Oficiálne CLI spustí vášho obľúbeného agenta už prepojeného s PleumRouter. Žiadne konfiguračné súbory sa nemenia.

```bash
npm install -g pleumrouter        # alebo: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # prihlásenie cez prehliadač, kľúč sa vygeneruje a uloží automaticky
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # terminálový chatový REPL
pleum models                      # zoznam všetkých modelov s cenami
```

Podporované pre automatické spustenie: `claude` · `aider` · `codex` · `goose` · `openhands` (plus konfiguračné úryvky pre `opencode` · `crush`). Vaše existujúce konfigurácie nástrojov sa nikdy nemenia.

---

## 🤖 Terminálové / CLI agenty

### Claude Code (kompatibilný s Anthropic)

Nástroje Claude Code a Claude Agent SDK sa pripájajú cez koncový bod `/v1/messages` kompatibilný s Anthropic.

```bash
# ANTHROPIC_BASE_URL je KOREŇOVÁ adresa (bez /v1) — CLI si samo pridá /v1/messages.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# Oficiálne CLI uprednostňuje ANTHROPIC_API_KEY; pre istotu nastavte oba.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ **Nedávajte** `/v1` do `ANTHROPIC_BASE_URL` — vznikne z toho `/v1/v1/messages` a zlyhá to. Volania nástrojov a streamovanie fungujú od začiatku do konca, aj keď sú smerované na modely kompatibilné s OpenAI.

### Codex CLI (Responses API)

Codex sa pripája cez OpenAI Responses API (`/v1/responses`); cesta Chat Completions bola z Codexu odstránená vo februári 2026.

```toml
# ~/.codex/config.toml
# model / model_provider sú kľúče na koreňovej úrovni dokumentu (musia byť nad [table]).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex pridá /responses → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex podporuje iba Responses API
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
// opencode.json   (alebo: /connect → Other)
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

# Goose / OpenHands: pred ID modelu pridajte predponu openai/
#   model = openai/gpt-4.1
```

### Gemini CLI

Oficiálne Gemini CLI má slabú podporu pre externé koncové body kompatibilné s OpenAI; možno budete potrebovať obal (wrapper) alebo fork kompatibilný s OpenAI.

---

## 🖥 IDE / GUI agenty

### Cline · Roo Code · Kilo Code · Cursor

Vyberte **OpenAI Compatible** (alebo **Custom OpenAI**) ako poskytovateľa a vložte:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Vždy použite **slot OpenAI Compatible** — vyhradená položka OpenRouter je napevno nastavená na openrouter.ai a zlyhá. **Cursor** vyžaduje `/v1` v základnej URL adrese a neprázdne pole kľúča. **Kilo Code** má známy problém (#681), kde sa vlastná základná URL adresa neposiela do výpisu modelov — zadajte ID modelu ručne.

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

S `model: AUTODETECT` si Continue automaticky stiahne zoznam modelov.

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

Názvy polí sa môžu líšiť podľa verzie Zed — pozrite si dokumentáciu Zed.

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
    base_url="https://router.pleum.ai",   # koreňová adresa, bez /v1 — SDK pridá /v1/messages
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # funguje ľubovoľný model PleumRouter
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Multimodálne — obrázky · zvuk · video

Všetky modality sú HTTP koncové body kompatibilné s OpenAI na tom istom kľúči. Vyberte model, ktorý podporuje danú modalitu, z [`GET /v1/models`](https://pleum.ai/models).

```bash
# Generovanie obrázkov
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Text na reč (vráti zvukové bajty; náklady v hlavičke X-Cost-Krw)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Reč na text (nahrávanie typu multipart)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# Generovanie videa je asynchrónne: POST vráti job_id, potom sa pýtajte cez GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### Rozhranie API

| Koncový bod | Protokol |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (streamovanie, nástroje, vízia) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Generovanie obrázkov |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Asynchrónne video |
| `GET /v1/models` | Katalóg modelov (verejný) |
| `GET /v1/credits` | Zostatok |

---

## 🔌 Ďalší agenti

Väčšina agentov, ktoré tu nie sú uvedené, funguje rovnako — nastavte základnú URL adresu kompatibilnú s OpenAI:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** a ďalšie.

Cez `/v1/messages` kompatibilné s Anthropic: **claude-code-router** sa tiež pripája pomocou `ANTHROPIC_BASE_URL`.

**ID modelov**: nájdete ich na `GET /v1/models` alebo na [stránke s modelmi](https://pleum.ai/models). Cline, Continue, OpenCode a ďalší si zoznam stiahnu automaticky. ID vo formáte OpenRouter (`openai/gpt-5.5`) sa konvertujú automaticky.

**LiteLLM proxy** (Aider, OpenHands, Open Interpreter, SWE-agent a gptme sú založené na LiteLLM a pripájajú sa priamo — ale ak si udržiavate LiteLLM proxy):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # predpona openai/ → trasa kompatibilná s OpenAI
      api_base: https://router.pleum.ai/v1           # NEPRIDÁVAJTE /chat/completions
      api_key: os.environ/PLEUM_API_KEY
```

---

## Prispievanie

Podarilo sa vám rozbehať PleumRouter s nástrojom, ktorý tu nie je uvedený? Uvítame PR — pridajte sekciu s **otestovaným** konfiguračným úryvkom (základná URL adresa, premenná prostredia pre kľúč, formát ID modelu a prípadné úskalia).

## Licencia

[MIT](LICENSE)
