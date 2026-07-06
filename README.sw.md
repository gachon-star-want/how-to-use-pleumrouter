<div align="center">

# Jinsi ya kutumia PleumRouter

**Ufunguo mmoja wa API kwa mifano 200+ ya AI — inayoendana na OpenAI, inatozwa kwa KRW.**

[Tovuti](https://pleum.ai) · [Nyaraka](https://pleum.ai/docs) · [Mifano](https://pleum.ai/models) · [Uwanja wa Michezo](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · Kiswahili · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter ni lango la AI: ufunguo mmoja (`plm_…`), URL ya msingi moja, mifano 210+ kutoka kwa watoa huduma 18 — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE na zaidi. Inazungumza **OpenAI Chat Completions**, **Anthropic Messages**, na **OpenAI Responses**, hivyo karibu kila wakala wa uandishi wa msimbo, programu-jalizi ya IDE, na SDK huunganishwa kwa mabadiliko ya mstari mmoja tu wa usanidi. Maandishi, embeddings, picha, sauti na video vyote hutumia ufunguo huohuo.

Hazina hii inakusanya **mapishi ya uunganishaji yaliyothibitishwa**. Kila kipande cha msimbo hapa chini kimejaribiwa dhidi ya lango halisi linaloendesha.

## Kuanza

1. [Jisajili](https://pleum.ai/signup) → Dashibodi → **API Keys** → toa ufunguo (huanza na `plm_`).
2. Elekeza zana yako kwenye URL ya msingi:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Baadhi ya mawakala (OpenCode, Crush) husoma PLEUM_API_KEY — ufunguo uleule, weka zote mbili.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Jaribio la haraka:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Unapata mkopo wa bure wa ₩1,000 unapojisajili na zawadi ya ₩5,000 kwenye malipo yako ya kwanza ya kuongeza salio.

## Miunganisho

| Kategoria | Zana |
|---|---|
| [⚡ Kizindua cha amri moja](#-pleum-cli--njia-ya-haraka) | CLI ya `pleum` |
| [🤖 Mawakala wa uandishi wa msimbo wa terminal](#-mawakala-wa-terminal--cli) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 Mawakala wa IDE / GUI](#-mawakala-wa-ide--gui) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK](#-sdk) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 API ya Multimodal](#-multimodal--picha--sauti--video) | Picha, TTS, STT, Video, Embeddings |
| [🔌 Kila kitu kingine](#-mawakala-wengine) | Vitambulisho vya mtindo wa OpenRouter, proksi ya LiteLLM, mawakala 15+ zaidi |

---

## ⚡ pleum CLI — njia ya haraka

CLI rasmi huzindua wakala unaompenda ukiwa tayari umeunganishwa na PleumRouter. Hakuna faili za usanidi zinazoguswa.

```bash
npm install -g pleumrouter        # au: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # kuingia kwa kivinjari, ufunguo hutolewa na kuhifadhiwa kiotomatiki
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # REPL ya mazungumzo ya terminal
pleum models                      # orodhesha mifano yote pamoja na bei
```

Inasaidiwa kwa uzinduzi kiotomatiki: `claude` · `aider` · `codex` · `goose` · `openhands` (pamoja na vipande vya usanidi kwa `opencode` · `crush`). Usanidi wako uliopo wa zana kamwe hauguswi.

---

## 🤖 Mawakala wa Terminal / CLI

### Claude Code (inayoendana na Anthropic)

Zana za Claude Code na Claude Agent SDK huunganishwa kupitia mwisho wa njia unaoendana na Anthropic `/v1/messages`.

```bash
# ANTHROPIC_BASE_URL ni MZIZI (bila /v1) — CLI yenyewe huongeza /v1/messages.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# CLI rasmi hupendelea ANTHROPIC_API_KEY; weka zote mbili ili kuwa salama.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ **Usiweke** `/v1` katika `ANTHROPIC_BASE_URL` — inakuwa `/v1/v1/messages` na kushindwa. Miito ya zana na utiririshaji hufanya kazi mwanzo hadi mwisho, hata inapoelekezwa kwenye mifano inayoendana na OpenAI.

### Codex CLI (Responses API)

Codex huunganishwa kupitia OpenAI Responses API (`/v1/responses`); njia ya Chat Completions iliondolewa kutoka Codex mnamo Februari 2026.

```toml
# ~/.codex/config.toml
# model / model_provider ni funguo za mzizi wa hati (lazima ziwe juu ya [table]).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex huongeza /responses → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex inasaidia tu Responses API
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
// opencode.json   (au: /connect → Other)
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

# Goose / OpenHands: weka kiambishi awali openai/ mbele ya kitambulisho cha mfano
#   model = openai/gpt-4.1
```

### Gemini CLI

Gemini CLI ya asili ina msaada dhaifu kwa miisho ya njia ya nje inayoendana na OpenAI; huenda ukahitaji kifuniko (wrapper) au tawi (fork) linaloendana na OpenAI.

---

## 🖥 Mawakala wa IDE / GUI

### Cline · Roo Code · Kilo Code · Cursor

Chagua **OpenAI Compatible** (au **Custom OpenAI**) kama mtoa huduma kisha bandika:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Tumia kila mara **nafasi ya OpenAI Compatible** — kiingilio maalum cha OpenRouter kimewekwa kigumu (hardcoded) kwenda openrouter.ai na kitashindwa. **Cursor** inahitaji `/v1` katika URL ya msingi na sehemu ya ufunguo isiyo tupu. **Kilo Code** ina hitilafu inayojulikana (#681) ambapo URL ya msingi maalum haipitishwi kwenye orodha ya mifano — ingiza kitambulisho cha mfano kwa mkono.

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

Kwa `model: AUTODETECT`, Continue huvuta orodha ya mifano kiotomatiki.

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

Majina ya sehemu (fields) yanaweza kutofautiana kulingana na toleo la Zed — angalia nyaraka za Zed.

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
    base_url="https://router.pleum.ai",   # mzizi, bila /v1 — SDK huongeza /v1/messages
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # mfano wowote wa PleumRouter unafanya kazi
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Multimodal — picha · sauti · video

Njia zote za modali ni miisho ya njia ya HTTP inayoendana na OpenAI kwa ufunguo huohuo. Chagua mfano unaosaidia modali hiyo kutoka [`GET /v1/models`](https://pleum.ai/models).

```bash
# Uzalishaji wa picha
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Maandishi-kwenda-sauti (hurudisha baiti za sauti; gharama iko katika kichwa X-Cost-Krw)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Sauti-kwenda-maandishi (upakiaji wa multipart)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# Uzalishaji wa video ni asynchronous: POST hurudisha job_id, kisha piga kura GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### Muundo wa API

| Mwisho wa njia | Itifaki |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (utiririshaji, zana, uoni) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Uzalishaji wa picha |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Video ya asynchronous |
| `GET /v1/models` | Katalogi ya mifano (ya umma) |
| `GET /v1/credits` | Salio |

---

## 🔌 Mawakala wengine

Mawakala wengi wasioorodheshwa hapa hufanya kazi kwa njia ileile — weka URL ya msingi inayoendana na OpenAI:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** na zaidi.

Kupitia `/v1/messages` inayoendana na Anthropic: **claude-code-router** pia huunganishwa kwa `ANTHROPIC_BASE_URL`.

**Vitambulisho vya mfano**: vitafute kwenye `GET /v1/models` au kwenye [ukurasa wa mifano](https://pleum.ai/models). Cline, Continue, OpenCode na wengine huvuta orodha kiotomatiki. Vitambulisho vya muundo wa OpenRouter (`openai/gpt-5.5`) hubadilishwa kiotomatiki.

**Proksi ya LiteLLM** (Aider, OpenHands, Open Interpreter, SWE-agent na gptme zinatumia msingi wa LiteLLM na huunganishwa moja kwa moja — lakini kama unatunza proksi ya LiteLLM):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # kiambishi awali openai/ → njia inayoendana na OpenAI
      api_base: https://router.pleum.ai/v1           # USIONGEZE /chat/completions
      api_key: os.environ/PLEUM_API_KEY
```

---

## Kuchangia

Umefanikiwa kutumia PleumRouter na zana isiyoorodheshwa hapa? PR zinakaribishwa — ongeza sehemu yenye kipande cha usanidi kilicho**jaribiwa** (URL ya msingi, mazingira ya ufunguo, muundo wa kitambulisho cha mfano, na mitego yoyote).

## Leseni

[MIT](LICENSE)
