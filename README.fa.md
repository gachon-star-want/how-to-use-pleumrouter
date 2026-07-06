<div align="center">

# نحوه استفاده از PleumRouter

**یک کلید API برای بیش از ۲۰۰ مدل هوش مصنوعی — سازگار با OpenAI، صورت‌حساب به وون کره (KRW).**

[وب‌سایت](https://pleum.ai) · [مستندات](https://pleum.ai/docs) · [مدل‌ها](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · فارسی · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter یک دروازه (gateway) هوش مصنوعی است: یک کلید (`plm_…`)، یک آدرس پایه (base URL)، بیش از ۲۱۰ مدل از ۱۸ ارائه‌دهنده — GPT، Claude، Gemini، DeepSeek، Qwen، EXAONE و موارد دیگر. این سرویس با **OpenAI Chat Completions**، **Anthropic Messages** و **OpenAI Responses** سازگار است، بنابراین تقریباً هر ایجنت کدنویسی، افزونهٔ IDE و SDK با یک تغییر تنظیمات تک‌خطی به آن متصل می‌شود. متن، امبدینگ (embeddings)، تصویر، گفتار و ویدیو همگی از طریق همان یک کلید اجرا می‌شوند.

این مخزن، **دستورالعمل‌های یکپارچه‌سازی تأییدشده** را گردآوری می‌کند. هر قطعه کد در ادامه در برابر دروازهٔ زنده (live gateway) آزمایش شده است.

## شروع کار

۱. [ثبت‌نام کنید](https://pleum.ai/signup) ← داشبورد ← **API Keys** ← یک کلید صادر کنید (با `plm_` شروع می‌شود).
۲. ابزار خود را به آدرس پایه (base URL) هدایت کنید:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# برخی ایجنت‌ها (OpenCode، Crush) از PLEUM_API_KEY می‌خوانند — کلید یکسان است، هر دو را تنظیم کنید.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

۳. تست عملکرد (smoke test):

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

با ثبت‌نام ۱٬۰۰۰ وون اعتبار رایگان و با اولین شارژ حساب ۵٬۰۰۰ وون پاداش دریافت می‌کنید.

## یکپارچه‌سازی‌ها

| دسته‌بندی | ابزارها |
|---|---|
| [⚡ راه‌انداز تک‌دستوره](#-پلیت-ام-cli--مسیر-سریع) | CLI به نام `pleum` |
| [🤖 ایجنت‌های کدنویسی ترمینال](#-ایجنت‌های-ترمینال--cli) | Claude Code، Codex CLI، Aider، OpenCode، Crush، Goose، OpenHands |
| [🖥 ایجنت‌های IDE / رابط گرافیکی](#-ایجنت‌های-ide--رابط-گرافیکی) | Cline، Roo Code، Kilo Code، Cursor، Continue.dev، Zed |
| [📦 SDKها](#-sdkها) | OpenAI SDK (Python/JS)، Anthropic SDK |
| [🎨 API چندرسانه‌ای](#-چندرسانه‌ای--تصویر--صدا--ویدیو) | تصاویر، TTS، STT، ویدیو، امبدینگ‌ها |
| [🔌 همه چیز دیگر](#-سایر-ایجنت‌ها) | شناسه‌های سبک OpenRouter، پراکسی LiteLLM، بیش از ۱۵ ایجنت دیگر |

---

## ⚡ پلیت ام CLI — مسیر سریع

CLI رسمی، ایجنت مورد علاقهٔ شما را که از پیش به PleumRouter متصل شده، راه‌اندازی می‌کند. هیچ فایل تنظیماتی دست‌کاری نمی‌شود.

```bash
npm install -g pleumrouter        # یا: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # ورود از طریق مرورگر، کلید به‌طور خودکار صادر و ذخیره می‌شود
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # رابط چت تعاملی (REPL) در ترمینال
pleum models                      # فهرست همهٔ مدل‌ها به همراه قیمت‌گذاری
```

پشتیبانی‌شده برای راه‌اندازی خودکار: `claude` · `aider` · `codex` · `goose` · `openhands` (به علاوهٔ قطعه‌کدهای تنظیمات برای `opencode` · `crush`). تنظیمات ابزارهای موجود شما هرگز تغییر نمی‌کند.

---

## 🤖 ایجنت‌های ترمینال / CLI

### Claude Code (سازگار با Anthropic)

ابزارهای Claude Code و Claude Agent SDK از طریق نقطهٔ پایانی سازگار با Anthropic یعنی `/v1/messages` متصل می‌شوند.

```bash
# ANTHROPIC_BASE_URL همان آدرس ریشه است (بدون /v1) — خود CLI عبارت /v1/messages را اضافه می‌کند.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# CLI رسمی، ANTHROPIC_API_KEY را ترجیح می‌دهد؛ برای اطمینان هر دو را تنظیم کنید.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ عبارت `/v1` را در `ANTHROPIC_BASE_URL` قرار **ندهید** — در این صورت به `/v1/v1/messages` تبدیل شده و با شکست مواجه می‌شود. فراخوانی ابزارها (tool calls) و استریمینگ، حتی هنگام مسیریابی به مدل‌های سازگار با OpenAI، سرتاسر به‌درستی کار می‌کنند.

### Codex CLI (Responses API)

Codex از طریق OpenAI Responses API (یعنی `/v1/responses`) متصل می‌شود؛ مسیر Chat Completions در فوریهٔ ۲۰۲۶ از Codex حذف شد.

```toml
# ~/.codex/config.toml
# model / model_provider کلیدهای ریشهٔ سند هستند (باید بالای [table] قرار گیرند).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex عبارت /responses را اضافه می‌کند ← /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex فقط از Responses API پشتیبانی می‌کند
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
// opencode.json   (یا: /connect ← Other)
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

# Goose / OpenHands: پیشوند openai/ را به شناسهٔ مدل اضافه کنید
#   model = openai/gpt-4.1
```

### Gemini CLI

نسخهٔ اصلی (upstream) Gemini CLI پشتیبانی ضعیفی از نقاط پایانی خارجی سازگار با OpenAI دارد؛ ممکن است به یک رَپِر (wrapper) یا فورک سازگار با OpenAI نیاز داشته باشید.

---

## 🖥 ایجنت‌های IDE / رابط گرافیکی

### Cline · Roo Code · Kilo Code · Cursor

گزینهٔ **OpenAI Compatible** (یا **Custom OpenAI**) را به‌عنوان ارائه‌دهنده انتخاب کرده و موارد زیر را جای‌گذاری کنید:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ همیشه از **جایگاه OpenAI Compatible** استفاده کنید — ورودی اختصاصی OpenRouter به‌صورت ثابت (hardcoded) به openrouter.ai اشاره دارد و کار نخواهد کرد. **Cursor** به وجود `/v1` در آدرس پایه و یک فیلد کلید غیرخالی نیاز دارد. **Kilo Code** یک مشکل شناخته‌شده (#681) دارد که در آن آدرس پایهٔ سفارشی به فهرست‌سازی مدل‌ها ارسال نمی‌شود — شناسهٔ مدل را به‌صورت دستی وارد کنید.

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

با تنظیم `model: AUTODETECT`، Continue فهرست مدل‌ها را به‌طور خودکار دریافت می‌کند.

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

نام فیلدها ممکن است بسته به نسخهٔ Zed متفاوت باشد — مستندات Zed را بررسی کنید.

---

## 📦 SDKها

### OpenAI SDK (پایتون)

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

### OpenAI SDK (جاوااسکریپت / تایپ‌اسکریپت)

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
    base_url="https://router.pleum.ai",   # ریشه، بدون /v1 — SDK عبارت /v1/messages را اضافه می‌کند
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # هر مدل PleumRouter کار می‌کند
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 چندرسانه‌ای — تصویر · صدا · ویدیو

تمام حالت‌های رسانه‌ای، نقاط پایانی HTTP سازگار با OpenAI روی همان یک کلید هستند. مدلی را که از آن حالت رسانه‌ای پشتیبانی می‌کند از [`GET /v1/models`](https://pleum.ai/models) انتخاب کنید.

```bash
# تولید تصویر
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# تبدیل متن به گفتار (بایت‌های صوتی برمی‌گرداند؛ هزینه در هدر X-Cost-Krw)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# تبدیل گفتار به متن (آپلود چندبخشی)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# تولید ویدیو ناهم‌زمان (async) است: درخواست POST یک job_id برمی‌گرداند، سپس GET /v1/jobs/{job_id} را پول (poll) کنید
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### سطح API (API surface)

| نقطهٔ پایانی | پروتکل |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (استریمینگ، ابزارها، بینایی) |
| `POST /v1/messages` | Anthropic Messages (Claude Code، Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | تولید تصویر |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | ویدیوی ناهم‌زمان |
| `GET /v1/models` | کاتالوگ مدل‌ها (عمومی) |
| `GET /v1/credits` | موجودی |

---

## 🔌 سایر ایجنت‌ها

بیشتر ایجنت‌هایی که در اینجا فهرست نشده‌اند به همین شکل کار می‌کنند — آدرس پایهٔ سازگار با OpenAI را تنظیم کنید:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** و موارد دیگر.

از طریق `/v1/messages` سازگار با Anthropic: **claude-code-router** نیز با `ANTHROPIC_BASE_URL` متصل می‌شود.

**شناسه‌های مدل**: آن‌ها را در `GET /v1/models` یا در [صفحهٔ مدل‌ها](https://pleum.ai/models) بیابید. Cline، Continue، OpenCode و ابزارهای دیگر فهرست را به‌طور خودکار دریافت می‌کنند. شناسه‌های با قالب OpenRouter (`openai/gpt-5.5`) به‌طور خودکار تبدیل می‌شوند.

**پراکسی LiteLLM** (Aider، OpenHands، Open Interpreter، SWE-agent و gptme مبتنی بر LiteLLM هستند و مستقیماً متصل می‌شوند — اما اگر یک پراکسی LiteLLM را نگه می‌دارید):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # پیشوند openai/ ← مسیر سازگار با OpenAI
      api_base: https://router.pleum.ai/v1           # عبارت /chat/completions را اضافه نکنید
      api_key: os.environ/PLEUM_API_KEY
```

---

## مشارکت

آیا PleumRouter را با ابزاری که در اینجا فهرست نشده کار انداخته‌اید؟ از ارسال PR استقبال می‌کنیم — بخشی با یک قطعه‌کد تنظیمات **آزمایش‌شده** اضافه کنید (آدرس پایه، متغیر محیطی کلید، قالب شناسهٔ مدل و هر نکتهٔ ریز و دردسرساز).

## مجوز

[MIT](LICENSE)
