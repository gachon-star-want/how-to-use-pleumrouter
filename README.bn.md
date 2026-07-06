<div align="center">

# PleumRouter কীভাবে ব্যবহার করবেন

**২০০+ AI মডেলের জন্য একটি API কী — OpenAI-সামঞ্জস্যপূর্ণ, KRW-তে বিল করা হয়।**

[ওয়েবসাইট](https://pleum.ai) · [ডকুমেন্টেশন](https://pleum.ai/docs) · [মডেলসমূহ](https://pleum.ai/models) · [প্লেগ্রাউন্ড](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · বাংলা · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter হলো একটি AI গেটওয়ে: একটি কী (`plm_…`), একটি বেস URL, ১৮টি প্রোভাইডার থেকে ২১০+ মডেল — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE এবং আরও অনেক কিছু। এটি **OpenAI Chat Completions**, **Anthropic Messages**, এবং **OpenAI Responses** ভাষায় কথা বলে, তাই প্রায় প্রতিটি কোডিং এজেন্ট, IDE প্লাগইন এবং SDK এক লাইনের কনফিগ পরিবর্তনেই সংযুক্ত হয়ে যায়। টেক্সট, এমবেডিং, ছবি, স্পিচ এবং ভিডিও সবকিছুই একই কী দিয়ে চলে।

এই রিপোতে **যাচাইকৃত ইন্টিগ্রেশন রেসিপি** সংগ্রহ করা আছে। নিচের প্রতিটি স্নিপেট লাইভ গেটওয়ের বিরুদ্ধে পরীক্ষিত।

## শুরু করা

1. [সাইন আপ করুন](https://pleum.ai/signup) → ড্যাশবোর্ড → **API Keys** → একটি কী ইস্যু করুন (`plm_` দিয়ে শুরু হয়)।
2. আপনার টুলকে বেস URL-এর দিকে নির্দেশ করুন:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# কিছু এজেন্ট (OpenCode, Crush) PLEUM_API_KEY পড়ে — একই কী, দুটোই সেট করুন।
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. স্মোক টেস্ট:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

সাইনআপে আপনি ₩১,০০০ ফ্রি ক্রেডিট এবং প্রথম টপ-আপে ₩৫,০০০ বোনাস পাবেন।

## ইন্টিগ্রেশন

| ক্যাটাগরি | টুলস |
|---|---|
| [⚡ ওয়ান-কমান্ড লঞ্চার](#-pleum-cli--দ্রুত-পথ) | `pleum` CLI |
| [🤖 টার্মিনাল কোডিং এজেন্ট](#-টার্মিনাল--cli-এজেন্ট) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE / GUI এজেন্ট](#-ide--gui-এজেন্ট) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK-সমূহ](#-sdk-সমূহ) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 মাল্টিমোডাল API](#-মাল্টিমোডাল--ছবি--অডিও--ভিডিও) | ছবি, TTS, STT, ভিডিও, এমবেডিং |
| [🔌 আরও যা কিছু](#-আরও-এজেন্ট) | OpenRouter-স্টাইল আইডি, LiteLLM প্রক্সি, ১৫+ আরও এজেন্ট |

---

## ⚡ pleum CLI — দ্রুত পথ

অফিসিয়াল CLI আপনার প্রিয় এজেন্টকে PleumRouter-এর সাথে আগে থেকেই সংযুক্ত করে লঞ্চ করে। কোনো কনফিগ ফাইল স্পর্শ করা হয় না।

```bash
npm install -g pleumrouter        # অথবা: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # ব্রাউজার লগইন, কী স্বয়ংক্রিয়ভাবে ইস্যু ও সংরক্ষিত হয়
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # টার্মিনাল চ্যাট REPL
pleum models                      # মূল্যসহ সব মডেলের তালিকা
```

অটো-লঞ্চের জন্য সমর্থিত: `claude` · `aider` · `codex` · `goose` · `openhands` (এছাড়া `opencode` · `crush`-এর জন্য কনফিগ স্নিপেট)। আপনার বিদ্যমান টুল কনফিগ কখনো পরিবর্তন করা হয় না।

---

## 🤖 টার্মিনাল / CLI এজেন্ট

### Claude Code (Anthropic-সামঞ্জস্যপূর্ণ)

Claude Code এবং Claude Agent SDK টুলস Anthropic-সামঞ্জস্যপূর্ণ `/v1/messages` এন্ডপয়েন্টের মাধ্যমে সংযুক্ত হয়।

```bash
# ANTHROPIC_BASE_URL হলো ROOT (কোনো /v1 নেই) — CLI নিজেই /v1/messages যোগ করে।
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# অফিসিয়াল CLI ANTHROPIC_API_KEY-কে অগ্রাধিকার দেয়; নিরাপত্তার জন্য দুটোই সেট করুন।
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ `ANTHROPIC_BASE_URL`-এ **`/v1` দেবেন না** — এটি `/v1/v1/messages` হয়ে ব্যর্থ হয়। OpenAI-সামঞ্জস্যপূর্ণ মডেলে রুট করা হলেও টুল কল এবং স্ট্রিমিং শুরু থেকে শেষ পর্যন্ত কাজ করে।

### Codex CLI (Responses API)

Codex OpenAI Responses API (`/v1/responses`)-এর মাধ্যমে সংযুক্ত হয়; Chat Completions পাথ ফেব্রুয়ারি ২০২৬-এ Codex থেকে সরিয়ে দেওয়া হয়েছে।

```toml
# ~/.codex/config.toml
# model / model_provider হলো ডকুমেন্ট-রুট কী (অবশ্যই [table]-এর উপরে থাকতে হবে)।
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex /responses যোগ করে → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex শুধুমাত্র Responses API সমর্থন করে
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
// opencode.json   (অথবা: /connect → Other)
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

# Goose / OpenHands: মডেল আইডির আগে openai/ প্রিফিক্স লাগান
#   model = openai/gpt-4.1
```

### Gemini CLI

আপস্ট্রিম Gemini CLI-তে বাহ্যিক OpenAI-সামঞ্জস্যপূর্ণ এন্ডপয়েন্টের জন্য দুর্বল সমর্থন রয়েছে; আপনার একটি OpenAI-সামঞ্জস্যপূর্ণ র‍্যাপার বা ফর্ক প্রয়োজন হতে পারে।

---

## 🖥 IDE / GUI এজেন্ট

### Cline · Roo Code · Kilo Code · Cursor

প্রোভাইডার হিসেবে **OpenAI Compatible** (বা **Custom OpenAI**) বাছাই করুন এবং পেস্ট করুন:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ সবসময় **OpenAI Compatible স্লট** ব্যবহার করুন — নির্ধারিত OpenRouter এন্ট্রি openrouter.ai-এ হার্ডকোড করা এবং তা ব্যর্থ হবে। **Cursor**-এর জন্য বেস URL-এ `/v1` এবং একটি নন-এম্পটি কী ফিল্ড প্রয়োজন। **Kilo Code**-এ একটি জানা সমস্যা রয়েছে (#681) যেখানে কাস্টম বেস URL মডেল লিস্টিংয়ে পাঠানো হয় না — মডেল আইডি ম্যানুয়ালি এন্টার করুন।

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

`model: AUTODETECT` দিয়ে Continue স্বয়ংক্রিয়ভাবে মডেল তালিকা টেনে আনে।

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

Zed-এর ভার্সন অনুযায়ী ফিল্ড নাম ভিন্ন হতে পারে — Zed ডকুমেন্টেশন চেক করুন।

---

## 📦 SDK-সমূহ

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
    base_url="https://router.pleum.ai",   # root, /v1 নেই — SDK নিজেই /v1/messages যোগ করে
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # যেকোনো PleumRouter মডেল কাজ করে
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 মাল্টিমোডাল — ছবি · অডিও · ভিডিও

সব মোডালিটি একই কীতে OpenAI-সামঞ্জস্যপূর্ণ HTTP এন্ডপয়েন্ট হিসেবে কাজ করে। [`GET /v1/models`](https://pleum.ai/models) থেকে সেই মোডালিটি সমর্থন করে এমন একটি মডেল বাছাই করুন।

```bash
# ছবি জেনারেশন
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# টেক্সট-টু-স্পিচ (অডিও বাইট রিটার্ন করে; খরচ X-Cost-Krw হেডারে)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# স্পিচ-টু-টেক্সট (মাল্টিপার্ট আপলোড)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# ভিডিও জেনারেশন অ্যাসিঙ্ক্রোনাস: POST একটি job_id রিটার্ন করে, তারপর GET /v1/jobs/{job_id} পোল করুন
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### API সারফেস

| এন্ডপয়েন্ট | প্রোটোকল |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (স্ট্রিমিং, টুলস, ভিশন) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | ছবি জেনারেশন |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | অ্যাসিঙ্ক্রোনাস ভিডিও |
| `GET /v1/models` | মডেল ক্যাটালগ (পাবলিক) |
| `GET /v1/credits` | ব্যালেন্স |

---

## 🔌 আরও এজেন্ট

এখানে তালিকাভুক্ত নয় এমন বেশিরভাগ এজেন্ট একইভাবে কাজ করে — OpenAI-সামঞ্জস্যপূর্ণ বেস URL সেট করুন:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** এবং আরও।

Anthropic-সামঞ্জস্যপূর্ণ `/v1/messages`-এর মাধ্যমে: **claude-code-router**-ও `ANTHROPIC_BASE_URL` দিয়ে সংযুক্ত হয়।

**মডেল আইডি**: `GET /v1/models`-এ অথবা [মডেল পেজে](https://pleum.ai/models) খুঁজে পাবেন। Cline, Continue, OpenCode এবং অন্যরা স্বয়ংক্রিয়ভাবে তালিকা টেনে আনে। OpenRouter-ফরম্যাট আইডি (`openai/gpt-5.5`) স্বয়ংক্রিয়ভাবে রূপান্তরিত হয়।

**LiteLLM প্রক্সি** (Aider, OpenHands, Open Interpreter, SWE-agent এবং gptme LiteLLM-ভিত্তিক এবং সরাসরি সংযুক্ত হয় — কিন্তু আপনি যদি একটি LiteLLM প্রক্সি বজায় রাখেন):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # openai/ প্রিফিক্স → OpenAI-compat রুট
      api_base: https://router.pleum.ai/v1           # /chat/completions যোগ করবেন না
      api_key: os.environ/PLEUM_API_KEY
```

---

## অবদান রাখা

এখানে তালিকাভুক্ত নয় এমন কোনো টুলের সাথে PleumRouter কাজ করাতে পেরেছেন? PR স্বাগত — একটি **পরীক্ষিত** কনফিগ স্নিপেট (বেস URL, কী env, মডেল আইডি ফরম্যাট, এবং যেকোনো সমস্যা) সহ একটি সেকশন যোগ করুন।

## লাইসেন্স

[MIT](LICENSE)
