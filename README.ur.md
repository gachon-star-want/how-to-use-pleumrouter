<div align="center">

# PleumRouter کا استعمال کیسے کریں

**200+ AI ماڈلز کے لیے ایک API کلید — OpenAI-compatible، KRW میں بلنگ۔**

[ویب سائٹ](https://pleum.ai) · [دستاویزات](https://pleum.ai/docs) · [ماڈلز](https://pleum.ai/models) · [پلے گراؤنڈ](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · اردو · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter ایک AI گیٹ وے ہے: ایک کلید (`plm_…`)، ایک بیس URL، 18 پرووائیڈرز کے 210+ ماڈلز — GPT، Claude، Gemini، DeepSeek، Qwen، EXAONE اور مزید۔ یہ **OpenAI Chat Completions**، **Anthropic Messages**، اور **OpenAI Responses** بولتا ہے، اس لیے تقریباً ہر کوڈنگ ایجنٹ، IDE پلگ اِن، اور SDK صرف ایک لائن کی کنفیگ تبدیلی سے جڑ جاتا ہے۔ متن، ایمبیڈنگز، تصویر، تقریر اور ویڈیو — سب ایک ہی کلید کے ذریعے چلتے ہیں۔

یہ ریپو **تصدیق شدہ انٹیگریشن ریسیپیز** جمع کرتا ہے۔ نیچے دیا گیا ہر اسنپٹ لائیو گیٹ وے کے خلاف ٹیسٹ کیا گیا ہے۔

## شروعات

1. [سائن اپ کریں](https://pleum.ai/signup) → ڈیش بورڈ → **API Keys** → ایک کلید جاری کریں (`plm_` سے شروع ہوتی ہے)۔
2. اپنے ٹول کو بیس URL کی طرف اشارہ کریں:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Some agents (OpenCode, Crush) read PLEUM_API_KEY — same key, set both.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. سموک ٹیسٹ:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

سائن اپ پر آپ کو ₩1,000 مفت کریڈٹ اور پہلی ٹاپ اپ پر ₩5,000 کا بونس ملتا ہے۔

## انٹیگریشنز

| زمرہ | ٹولز |
|---|---|
| [⚡ ایک کمانڈ لانچر](#-pleum-cli--تیز-ترین-راستہ) | `pleum` CLI |
| [🤖 ٹرمینل کوڈنگ ایجنٹس](#-ٹرمینل--cli-ایجنٹس) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE / GUI ایجنٹس](#-ide--gui-ایجنٹس) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDKs](#-sdks) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 ملٹی موڈل API](#-ملٹی-موڈل--تصویر--آڈیو--ویڈیو) | Images, TTS, STT, Video, Embeddings |
| [🔌 باقی سب کچھ](#-مزید-ایجنٹس) | OpenRouter-style IDs, LiteLLM proxy, 15+ more agents |

---

## ⚡ pleum CLI — تیز ترین راستہ

سرکاری CLI آپ کے پسندیدہ ایجنٹ کو پہلے سے PleumRouter سے منسلک کرکے لانچ کرتا ہے۔ کوئی کنفیگ فائل چھیڑی نہیں جاتی۔

```bash
npm install -g pleumrouter        # or: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # browser login, key auto-issued & saved
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # terminal chat REPL
pleum models                      # list all models with pricing
```

آٹو لانچ کے لیے تعاون یافتہ: `claude` · `aider` · `codex` · `goose` · `openhands` (اس کے علاوہ `opencode` · `crush` کے لیے کنفیگ اسنپٹس بھی موجود ہیں)۔ آپ کی موجودہ ٹول کنفیگز کبھی تبدیل نہیں کی جاتیں۔

---

## 🤖 ٹرمینل / CLI ایجنٹس

### Claude Code (Anthropic-compatible)

Claude Code اور Claude Agent SDK ٹولز Anthropic-compatible `/v1/messages` اینڈ پوائنٹ کے ذریعے جڑتے ہیں۔

```bash
# ANTHROPIC_BASE_URL is the ROOT (no /v1) — the CLI appends /v1/messages itself.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# The official CLI prefers ANTHROPIC_API_KEY; set both to be safe.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ `ANTHROPIC_BASE_URL` میں `/v1` **مت** ڈالیں — یہ `/v1/v1/messages` بن جاتا ہے اور ناکام ہو جاتا ہے۔ ٹول کالز اور اسٹریمنگ سرے سے سرے تک کام کرتے ہیں، چاہے OpenAI-compatible ماڈلز کی طرف روٹ کیا جائے۔

### Codex CLI (Responses API)

Codex OpenAI Responses API (`/v1/responses`) کے ذریعے جڑتا ہے؛ فروری 2026 میں Codex سے Chat Completions پاتھ ہٹا دیا گیا تھا۔

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

اپ اسٹریم Gemini CLI بیرونی OpenAI-compatible اینڈ پوائنٹس کی کمزور حمایت رکھتا ہے؛ آپ کو ایک OpenAI-compatible ریپر یا فورک کی ضرورت پڑ سکتی ہے۔

---

## 🖥 IDE / GUI ایجنٹس

### Cline · Roo Code · Kilo Code · Cursor

پرووائیڈر کے طور پر **OpenAI Compatible** (یا **Custom OpenAI**) منتخب کریں اور یہ پیسٹ کریں:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ ہمیشہ **OpenAI Compatible سلاٹ** استعمال کریں — مخصوص OpenRouter اندراج openrouter.ai پر ہارڈ کوڈ شدہ ہے اور ناکام ہو جائے گا۔ **Cursor** کو بیس URL میں `/v1` اور ایک غیر خالی کلید فیلڈ درکار ہوتی ہے۔ **Kilo Code** میں ایک معلوم مسئلہ ہے (#681) جہاں کسٹم بیس URL ماڈل لسٹنگ کو منتقل نہیں ہوتا — ماڈل ID دستی طور پر درج کریں۔

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

`model: AUTODETECT` کے ساتھ Continue خودکار طور پر ماڈل لسٹ حاصل کرتا ہے۔

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

فیلڈ کے نام Zed کے ورژن کے مطابق مختلف ہو سکتے ہیں — Zed کی دستاویزات دیکھیں۔

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

## 🎨 ملٹی موڈل — تصویر · آڈیو · ویڈیو

تمام موڈیلیٹیز ایک ہی کلید پر OpenAI-compatible HTTP اینڈ پوائنٹس ہیں۔ [`GET /v1/models`](https://pleum.ai/models) سے وہ ماڈل منتخب کریں جو مطلوبہ موڈیلیٹی کی حمایت کرتا ہو۔

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

### API سطح

| اینڈ پوائنٹ | پروٹوکول |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (streaming, tools, vision) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Image generation |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Async video |
| `GET /v1/models` | Model catalog (public) |
| `GET /v1/credits` | Balance |

---

## 🔌 مزید ایجنٹس

یہاں درج نہ ہونے والے زیادہ تر ایجنٹس اسی طرح کام کرتے ہیں — OpenAI-compatible بیس URL سیٹ کریں:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** اور مزید۔

Anthropic-compatible `/v1/messages` کے ذریعے: **claude-code-router** بھی `ANTHROPIC_BASE_URL` کے ساتھ جڑتا ہے۔

**ماڈل IDs**: انہیں `GET /v1/models` پر یا [ماڈلز کے صفحے](https://pleum.ai/models) پر تلاش کریں۔ Cline، Continue، OpenCode اور دیگر خودکار طور پر لسٹ حاصل کر لیتے ہیں۔ OpenRouter-format IDs (`openai/gpt-5.5`) خودکار طور پر تبدیل ہو جاتی ہیں۔

**LiteLLM پراکسی** (Aider، OpenHands، Open Interpreter، SWE-agent اور gptme LiteLLM پر مبنی ہیں اور براہ راست جڑتے ہیں — لیکن اگر آپ LiteLLM پراکسی برقرار رکھتے ہیں):

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

## تعاون

کیا آپ نے PleumRouter کو کسی ایسے ٹول کے ساتھ چلایا جو یہاں درج نہیں ہے؟ PRs کا خیرمقدم ہے — ایک **ٹیسٹ شدہ** کنفیگ اسنپٹ (بیس URL، کلید env، ماڈل ID فارمیٹ، اور کوئی بھی خامیاں) کے ساتھ ایک سیکشن شامل کریں۔

## لائسنس

[MIT](LICENSE)
