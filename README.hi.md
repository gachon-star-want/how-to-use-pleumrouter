<div align="center">

# PleumRouter का उपयोग कैसे करें

**200+ AI मॉडल के लिए एक API कुंजी — OpenAI-संगत, KRW में बिल किया जाता है।**

[वेबसाइट](https://pleum.ai) · [दस्तावेज़](https://pleum.ai/docs) · [मॉडल](https://pleum.ai/models) · [प्लेग्राउंड](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · हिन्दी · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter एक AI गेटवे है: एक कुंजी (`plm_…`), एक बेस URL, 18 प्रोवाइडर के 210+ मॉडल — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE और अन्य। यह **OpenAI Chat Completions**, **Anthropic Messages**, और **OpenAI Responses** को सपोर्ट करता है, इसलिए लगभग हर कोडिंग एजेंट, IDE प्लगइन, और SDK सिर्फ़ एक-लाइन कॉन्फ़िग बदलाव से कनेक्ट हो जाता है। टेक्स्ट, एम्बेडिंग, इमेज, स्पीच और वीडियो — सब कुछ उसी एक कुंजी से चलता है।

यह रिपॉज़िटरी **सत्यापित इंटीग्रेशन रेसिपी** का संग्रह है। नीचे दिया गया हर स्निपेट लाइव गेटवे पर टेस्ट किया गया है।

## शुरुआत करें

1. [साइन अप करें](https://pleum.ai/signup) → डैशबोर्ड → **API Keys** → एक कुंजी जारी करें (जो `plm_` से शुरू होती है)।
2. अपने टूल को बेस URL पर पॉइंट करें:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Some agents (OpenCode, Crush) read PLEUM_API_KEY — same key, set both.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. स्मोक टेस्ट करें:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

साइन अप करने पर आपको ₩1,000 का मुफ़्त क्रेडिट मिलता है, और आपके पहले टॉप-अप पर ₩5,000 का बोनस भी मिलता है।

## इंटीग्रेशन

| श्रेणी | टूल्स |
|---|---|
| [⚡ एक-कमांड लॉन्चर](#-pleum-cli--तेज़-रास्ता) | `pleum` CLI |
| [🤖 टर्मिनल कोडिंग एजेंट्स](#-टर्मिनल--cli-एजेंट्स) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE / GUI एजेंट्स](#-ide--gui-एजेंट्स) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDKs](#-sdks) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 मल्टीमॉडल API](#-मल्टीमॉडल--इमेज--ऑडियो--वीडियो) | इमेज, TTS, STT, वीडियो, एम्बेडिंग |
| [🔌 बाक़ी सब कुछ](#-अधिक-एजेंट्स) | OpenRouter-स्टाइल IDs, LiteLLM प्रॉक्सी, 15+ अन्य एजेंट्स |

---

## ⚡ pleum CLI — तेज़ रास्ता

ऑफ़िशियल CLI आपके पसंदीदा एजेंट को पहले से PleumRouter से वायर्ड करके लॉन्च करता है। कोई भी कॉन्फ़िग फ़ाइल नहीं छेड़ी जाती।

```bash
npm install -g pleumrouter        # or: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # browser login, key auto-issued & saved
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # terminal chat REPL
pleum models                      # list all models with pricing
```

ऑटो-लॉन्च के लिए सपोर्टेड: `claude` · `aider` · `codex` · `goose` · `openhands` (साथ ही `opencode` · `crush` के लिए कॉन्फ़िग स्निपेट्स)। आपके मौजूदा टूल कॉन्फ़िग कभी मॉडिफ़ाई नहीं किए जाते।

---

## 🤖 टर्मिनल / CLI एजेंट्स

### Claude Code (Anthropic-संगत)

Claude Code और Claude Agent SDK टूल्स Anthropic-संगत `/v1/messages` एंडपॉइंट के ज़रिए कनेक्ट होते हैं।

```bash
# ANTHROPIC_BASE_URL is the ROOT (no /v1) — the CLI appends /v1/messages itself.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# The official CLI prefers ANTHROPIC_API_KEY; set both to be safe.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ `ANTHROPIC_BASE_URL` में `/v1` **मत** डालें — यह `/v1/v1/messages` बन जाता है और फ़ेल हो जाता है। टूल कॉल्स और स्ट्रीमिंग एंड-टू-एंड काम करते हैं, भले ही यह OpenAI-संगत मॉडल्स पर रूट किया गया हो।

### Codex CLI (Responses API)

Codex, OpenAI Responses API (`/v1/responses`) के ज़रिए कनेक्ट होता है; Chat Completions पाथ को Codex से फ़रवरी 2026 में हटा दिया गया था।

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

अपस्ट्रीम Gemini CLI में बाहरी OpenAI-संगत एंडपॉइंट्स के लिए सपोर्ट कमज़ोर है; आपको एक OpenAI-संगत रैपर या फ़ोर्क की ज़रूरत पड़ सकती है।

---

## 🖥 IDE / GUI एजेंट्स

### Cline · Roo Code · Kilo Code · Cursor

प्रोवाइडर के रूप में **OpenAI Compatible** (या **Custom OpenAI**) चुनें और यह पेस्ट करें:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ हमेशा **OpenAI Compatible slot** का इस्तेमाल करें — डेडिकेटेड OpenRouter एंट्री openrouter.ai पर हार्डकोडेड है और फ़ेल हो जाएगी। **Cursor** को बेस URL में `/v1` और एक नॉन-एम्प्टी की फ़ील्ड चाहिए होती है। **Kilo Code** में एक जाना-पहचाना इशू (#681) है जहाँ कस्टम बेस URL मॉडल लिस्टिंग को पास नहीं होता — मॉडल ID मैन्युअली एंटर करें।

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

`model: AUTODETECT` के साथ Continue अपने आप मॉडल लिस्ट खींच लेता है।

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

फ़ील्ड नेम Zed वर्शन के हिसाब से अलग हो सकते हैं — Zed डॉक्स चेक करें।

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

## 🎨 मल्टीमॉडल — इमेज · ऑडियो · वीडियो

सभी मोडैलिटी एक ही कुंजी पर OpenAI-संगत HTTP एंडपॉइंट के रूप में उपलब्ध हैं। [`GET /v1/models`](https://pleum.ai/models) से ऐसा मॉडल चुनें जो उस मोडैलिटी को सपोर्ट करता हो।

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

### API सतह

| एंडपॉइंट | प्रोटोकॉल |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (स्ट्रीमिंग, टूल्स, विज़न) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | इमेज जनरेशन |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | एसिंक वीडियो |
| `GET /v1/models` | मॉडल कैटलॉग (पब्लिक) |
| `GET /v1/credits` | बैलेंस |

---

## 🔌 अधिक एजेंट्स

यहाँ लिस्ट न किए गए ज़्यादातर एजेंट्स भी उसी तरह काम करते हैं — OpenAI-संगत बेस URL सेट करें:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** और भी बहुत कुछ।

Anthropic-संगत `/v1/messages` के ज़रिए: **claude-code-router** भी `ANTHROPIC_BASE_URL` से कनेक्ट होता है।

**मॉडल IDs**: इन्हें `GET /v1/models` पर या [मॉडल पेज](https://pleum.ai/models) पर खोजें। Cline, Continue, OpenCode और अन्य टूल्स लिस्ट को अपने आप फ़ेच कर लेते हैं। OpenRouter-फ़ॉर्मेट वाली IDs (`openai/gpt-5.5`) अपने आप कन्वर्ट हो जाती हैं।

**LiteLLM प्रॉक्सी** (Aider, OpenHands, Open Interpreter, SWE-agent और gptme LiteLLM-बेस्ड हैं और सीधे कनेक्ट होते हैं — लेकिन अगर आप एक LiteLLM प्रॉक्सी इस्तेमाल करते हैं):

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

## योगदान करें

PleumRouter को यहाँ लिस्ट न किए गए किसी टूल के साथ चला पाए? PRs का स्वागत है — एक **टेस्टेड** कॉन्फ़िग स्निपेट (बेस URL, कुंजी वाला एनवायरनमेंट वेरिएबल, मॉडल ID फ़ॉर्मेट, और कोई भी अड़चनें) के साथ एक सेक्शन जोड़ें।

## लाइसेंस

[MIT](LICENSE)
