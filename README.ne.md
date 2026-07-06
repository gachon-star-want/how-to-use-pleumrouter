<div align="center">

# PleumRouter कसरी प्रयोग गर्ने

**२००+ AI मोडेलहरूको लागि एउटै API कुञ्जी — OpenAI-सुसंगत, KRW मा बिल गरिएको।**

[Website](https://pleum.ai) · [Docs](https://pleum.ai/docs) · [Models](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · नेपाली · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter एउटा AI गेटवे हो: एउटै कुञ्जी (`plm_…`), एउटै base URL, १८ प्रदायकबाट २१०+ मोडेलहरू — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE र थप धेरै। यसले **OpenAI Chat Completions**, **Anthropic Messages**, र **OpenAI Responses** बोल्छ, त्यसैले लगभग हरेक कोडिङ एजेन्ट, IDE प्लगइन, र SDK एक-लाइन कन्फिग परिवर्तनसँगै जोडिन्छ। टेक्स्ट, एम्बेडिङ, इमेज, स्पीच र भिडियो सबै एउटै कुञ्जीबाट चल्छन्।

यो रिपोमा **प्रमाणित इन्टिग्रेसन रेसिपीहरू** संकलन गरिएका छन्। तलको हरेक स्निपेट लाइभ गेटवेमा परीक्षण गरिएको छ।

## सुरु गर्दै

1. [Sign up](https://pleum.ai/signup) → ड्यासबोर्ड → **API Keys** → एउटा कुञ्जी जारी गर्नुहोस् (`plm_` बाट सुरु हुने)।
2. आफ्नो टूललाई base URL मा पोइन्ट गर्नुहोस्।

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Some agents (OpenCode, Crush) read PLEUM_API_KEY — same key, set both.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. स्मोक टेस्ट।

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

तपाईंले साइनअपमा ₩1,000 निःशुल्क क्रेडिट र आफ्नो पहिलो टप-अपमा ₩5,000 बोनस पाउनुहुन्छ।

## इन्टिग्रेसनहरू

| श्रेणी | टूलहरू |
|---|---|
| [⚡ एक-कमाण्ड लन्चर](#-pleum-cli--द-फास्ट-पाथ) | `pleum` CLI |
| [🤖 टर्मिनल कोडिङ एजेन्टहरू](#-टर्मिनल--cli-एजेन्टहरू) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE / GUI एजेन्टहरू](#-ide--gui-एजेन्टहरू) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDKs](#-sdks) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 मल्टिमोडल API](#-मल्टिमोडल--इमेज--अडियो--भिडियो) | Images, TTS, STT, Video, Embeddings |
| [🔌 अरू सबै](#-थप-एजेन्टहरू) | OpenRouter-शैलीका IDहरू, LiteLLM प्रोक्सी, थप १५+ एजेन्टहरू |

---

## ⚡ pleum CLI — द फास्ट पाथ

आधिकारिक CLI ले तपाईंको मनपर्ने एजेन्टलाई PleumRouter सँग पहिले नै तार जोडिएको अवस्थामा लन्च गर्छ। कुनै पनि कन्फिग फाइल छोइँदैन।

```bash
npm install -g pleumrouter        # or: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # browser login, key auto-issued & saved
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # terminal chat REPL
pleum models                      # list all models with pricing
```

अटो-लन्चको लागि समर्थित: `claude` · `aider` · `codex` · `goose` · `openhands` (साथै `opencode` · `crush` को लागि कन्फिग स्निपेटहरू)। तपाईंको अवस्थित टूल कन्फिगहरू कहिल्यै परिमार्जन गरिँदैनन्।

---

## 🤖 टर्मिनल / CLI एजेन्टहरू

### Claude Code (Anthropic-सुसंगत)

Claude Code र Claude Agent SDK टूलहरू Anthropic-सुसंगत `/v1/messages` एन्डपोइन्ट मार्फत जोडिन्छन्।

```bash
# ANTHROPIC_BASE_URL is the ROOT (no /v1) — the CLI appends /v1/messages itself.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# The official CLI prefers ANTHROPIC_API_KEY; set both to be safe.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ `ANTHROPIC_BASE_URL` मा `/v1` **नराख्नुहोस्** — यो `/v1/v1/messages` बन्छ र असफल हुन्छ। टूल कलहरू र स्ट्रिमिङ अन्त्यदेखि अन्त्यसम्म काम गर्छन्, OpenAI-सुसंगत मोडेलहरूमा राउट गरिँदा पनि।

### Codex CLI (Responses API)

Codex OpenAI Responses API (`/v1/responses`) मार्फत जोडिन्छ; Chat Completions पथलाई फेब्रुअरी 2026 मा Codex बाट हटाइएको थियो।

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

अपस्ट्रिम Gemini CLI मा बाह्य OpenAI-सुसंगत एन्डपोइन्टहरूको लागि कमजोर समर्थन छ; तपाईंलाई OpenAI-सुसंगत र्‍यापर वा फोर्क चाहिन सक्छ।

---

## 🖥 IDE / GUI एजेन्टहरू

### Cline · Roo Code · Kilo Code · Cursor

प्रदायकको रूपमा **OpenAI Compatible** (वा **Custom OpenAI**) छान्नुहोस् र पेस्ट गर्नुहोस्।

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ सधैं **OpenAI Compatible स्लट** प्रयोग गर्नुहोस् — समर्पित OpenRouter इन्ट्री openrouter.ai मा हार्डकोड गरिएको छ र असफल हुनेछ। **Cursor** लाई base URL मा `/v1` र खाली नभएको कुञ्जी फिल्ड आवश्यक पर्छ। **Kilo Code** मा एउटा ज्ञात समस्या (#681) छ जहाँ कस्टम base URL मोडेल लिस्टिङमा पास हुँदैन — मोडेल ID म्यानुअली प्रविष्ट गर्नुहोस्।

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

`model: AUTODETECT` सँग Continue ले मोडेल सूची स्वचालित रूपमा तान्छ।

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

फिल्ड नामहरू Zed संस्करण अनुसार फरक हुन सक्छन् — Zed डकुमेन्टेसन जाँच गर्नुहोस्।

---

## 📦 SDKs

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

## 🎨 मल्टिमोडल — इमेज · अडियो · भिडियो

सबै मोडालिटीहरू एउटै कुञ्जीमा OpenAI-सुसंगत HTTP एन्डपोइन्टहरू हुन्। [`GET /v1/models`](https://pleum.ai/models) बाट मोडालिटी समर्थन गर्ने मोडेल छान्नुहोस्।

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

### API सर्फेस

| एन्डपोइन्ट | प्रोटोकल |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (स्ट्रिमिङ, टूलहरू, भिजन) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | इमेज जेनेरेसन |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | एसिन्क्रोनस भिडियो |
| `GET /v1/models` | मोडेल क्याटलग (सार्वजनिक) |
| `GET /v1/credits` | ब्यालेन्स |

---

## 🔌 थप एजेन्टहरू

यहाँ सूचीबद्ध नगरिएका धेरैजसो एजेन्टहरूले उस्तै तरिकाले काम गर्छन् — OpenAI-सुसंगत base URL सेट गर्नुहोस्।

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** र थप।

Anthropic-सुसंगत `/v1/messages` मार्फत: **claude-code-router** पनि `ANTHROPIC_BASE_URL` सँग जोडिन्छ।

**मोडेल IDहरू**: तिनीहरूलाई `GET /v1/models` मा वा [models page](https://pleum.ai/models) मा फेला पार्नुहोस्। Cline, Continue, OpenCode र अरूले सूची स्वचालित रूपमा तान्छन्। OpenRouter-ढाँचाका IDहरू (`openai/gpt-5.5`) स्वचालित रूपमा रूपान्तरण गरिन्छन्।

**LiteLLM प्रोक्सी** (Aider, OpenHands, Open Interpreter, SWE-agent र gptme LiteLLM-आधारित हुन् र प्रत्यक्ष रूपमा जोडिन्छन् — तर यदि तपाईंले LiteLLM प्रोक्सी राख्नुभयो भने):

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

## योगदान

यहाँ सूचीबद्ध नभएको कुनै टूलसँग PleumRouter काम गराउनुभयो? PRहरूको स्वागत छ — **परीक्षण गरिएको** कन्फिग स्निपेट (base URL, कुञ्जी env, मोडेल ID ढाँचा, र कुनै पनि जटिलताहरू) सहित एउटा सेक्सन थप्नुहोस्।

## लाइसेन्स

[MIT](LICENSE)
