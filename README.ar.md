<div align="center">

# كيفية استخدام PleumRouter

**مفتاح API واحد لأكثر من 200 نموذج ذكاء اصطناعي — متوافق مع OpenAI، ويُفوتر بالوون الكوري (KRW).**

[الموقع الإلكتروني](https://pleum.ai) · [الوثائق](https://pleum.ai/docs) · [النماذج](https://pleum.ai/models) · [ساحة التجربة](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · العربية · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter هي بوابة ذكاء اصطناعي: مفتاح واحد (‏`plm_…`‏)، وعنوان أساس واحد (base URL)، وأكثر من 210 نموذج من 18 مزوّدًا — GPT وClaude وGemini وDeepSeek وQwen وEXAONE والمزيد. تدعم البوابة واجهات **OpenAI Chat Completions** و**Anthropic Messages** و**OpenAI Responses**، لذا يتصل بها تقريبًا أي عميل برمجة أو إضافة IDE أو SDK بمجرد تغيير سطر واحد من الإعداد. النصوص والتضمينات (embeddings) والصور والصوت والفيديو، كلها تعمل عبر المفتاح نفسه.

يجمع هذا المستودع **وصفات تكامل موثّقة**. كل مقتطف أدناه تم اختباره على البوابة الفعلية (live gateway).

## البدء

1. [أنشئ حسابًا](https://pleum.ai/signup) ← لوحة التحكم ← **API Keys** ← أصدر مفتاحًا (يبدأ بـ `plm_`).
2. وجّه أداتك إلى العنوان الأساس (base URL):

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# بعض العملاء (OpenCode، Crush) يقرؤون PLEUM_API_KEY — نفس المفتاح، فاضبط الاثنين معًا.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. اختبار سريع (Smoke test):

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

تحصل على رصيد مجاني قدره ₩1,000 عند التسجيل، وعلى مكافأة ₩5,000 عند أول عملية شحن رصيد.

## التكاملات

| الفئة | الأدوات |
|---|---|
| [⚡ مُشغِّل بأمر واحد](#-pleum-cli-—-المسار-السريع) | أداة CLI باسم `pleum` |
| [🤖 عملاء برمجة الطرفية (Terminal)](#-عملاء-cli--الطرفية) | Claude Code وCodex CLI وAider وOpenCode وCrush وGoose وOpenHands |
| [🖥 عملاء IDE / واجهات رسومية](#-عملاء-ide--الواجهة-الرسومية) | Cline وRoo Code وKilo Code وCursor وContinue.dev وZed |
| [📦 حزم SDK](#-حزم-sdk) | OpenAI SDK (بايثون/جافاسكريبت)، وAnthropic SDK |
| [🎨 واجهة برمجة متعددة الوسائط](#-الوسائط-المتعددة--الصورة--الصوت--الفيديو) | الصور، وتحويل النص إلى كلام (TTS)، وتحويل الكلام إلى نص (STT)، والفيديو، والتضمينات (Embeddings) |
| [🔌 كل شيء آخر](#-عملاء-إضافيون) | معرّفات على طراز OpenRouter، ووكيل LiteLLM، وأكثر من 15 عميلًا إضافيًا |

---

## ⚡ pleum CLI — المسار السريع

تُشغّل الأداة الرسمية عميلك المفضل موصولًا بالفعل بـ PleumRouter. لا تُلمَس أي ملفات إعداد.

```bash
npm install -g pleumrouter        # أو: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # تسجيل دخول عبر المتصفح، ويُصدَر المفتاح ويُحفظ تلقائيًا
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # واجهة محادثة تفاعلية (REPL) في الطرفية
pleum models                      # عرض كل النماذج مع أسعارها
```

مدعوم للتشغيل التلقائي: `claude` · `aider` · `codex` · `goose` · `openhands` (بالإضافة إلى مقتطفات إعداد لـ `opencode` · `crush`). إعدادات أدواتك الحالية لا تُعدَّل أبدًا.

---

## 🤖 عملاء CLI / الطرفية

### Claude Code (متوافق مع Anthropic)

تتصل أداة Claude Code وأدوات Claude Agent SDK عبر نقطة النهاية المتوافقة مع Anthropic ‏`/v1/messages`.

```bash
# ANTHROPIC_BASE_URL هو الجذر (بدون /v1) — الأداة نفسها تُلحق /v1/messages.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# الأداة الرسمية تفضّل ANTHROPIC_API_KEY؛ اضبط الاثنين معًا لضمان الأمان.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ **لا** تضع `/v1` داخل `ANTHROPIC_BASE_URL` — فذلك يحوّلها إلى `/v1/v1/messages` فيفشل الطلب. استدعاءات الأدوات (tool calls) والبث (streaming) تعملان من طرف إلى طرف، حتى عند التوجيه إلى نماذج متوافقة مع OpenAI.

### Codex CLI (واجهة Responses API)

تتصل Codex عبر واجهة OpenAI Responses (‏`/v1/responses`)؛ إذ أُزيل مسار Chat Completions من Codex في فبراير 2026.

```toml
# ~/.codex/config.toml
# model / model_provider مفاتيح على مستوى جذر المستند (يجب أن تكون فوق الجدول [table]).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex تُلحق /responses ← /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex تدعم فقط واجهة Responses
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
// opencode.json   (أو: /connect ← Other)
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

# Goose / OpenHands: أضِف البادئة openai/ إلى معرّف النموذج
#   model = openai/gpt-4.1
```

### Gemini CLI

دعم أداة Gemini CLI الرسمية لنقاط النهاية الخارجية المتوافقة مع OpenAI ضعيف؛ قد تحتاج إلى غلاف (wrapper) متوافق مع OpenAI أو نسخة معدَّلة (fork).

---

## 🖥 عملاء IDE / الواجهة الرسومية

### Cline · Roo Code · Kilo Code · Cursor

اختر **OpenAI Compatible** (أو **Custom OpenAI**) كمزوّد، والصق ما يلي:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ استخدم دائمًا **خانة OpenAI Compatible** — فمُدخَل OpenRouter المخصص مُبرمَج ليشير حصرًا إلى openrouter.ai وسيفشل. **Cursor** يتطلب وجود `/v1` في العنوان الأساس وحقل مفتاح غير فارغ. لدى **Kilo Code** مشكلة معروفة (#681) لا يُمرَّر فيها العنوان الأساس المخصص إلى عملية سرد النماذج — أدخِل معرّف النموذج يدويًا.

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

مع `model: AUTODETECT` تسحب Continue قائمة النماذج تلقائيًا.

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

قد تختلف أسماء الحقول حسب إصدار Zed — راجع وثائق Zed.

---

## 📦 حزم SDK

### OpenAI SDK (بايثون)

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

### OpenAI SDK (جافاسكريبت / TypeScript)

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
    base_url="https://router.pleum.ai",   # الجذر، بدون /v1 — الـ SDK يُلحق /v1/messages
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # يعمل أي نموذج من PleumRouter
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 الوسائط المتعددة — الصورة · الصوت · الفيديو

جميع أنواع الوسائط هي نقاط نهاية HTTP متوافقة مع OpenAI تحت المفتاح نفسه. اختر نموذجًا يدعم نوع الوسيط من [`GET /v1/models`](https://pleum.ai/models).

```bash
# توليد الصور
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# تحويل النص إلى كلام (يُرجع بايتات صوتية؛ التكلفة في ترويسة X-Cost-Krw)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# تحويل الكلام إلى نص (رفع multipart)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# توليد الفيديو غير متزامن: يُرجع POST قيمة job_id، ثم استعلم عبر GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### واجهة الـ API

| نقطة النهاية | البروتوكول |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (بث، أدوات، رؤية) |
| `POST /v1/messages` | Anthropic Messages (Claude Code، Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | توليد الصور |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | تحويل النص إلى كلام · تحويل الكلام إلى نص |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | فيديو غير متزامن |
| `GET /v1/models` | كتالوج النماذج (عام) |
| `GET /v1/credits` | الرصيد |

---

## 🔌 عملاء إضافيون

معظم العملاء غير المدرجين هنا يعملون بالطريقة نفسها — اضبط العنوان الأساس المتوافق مع OpenAI:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** والمزيد.

عبر الواجهة المتوافقة مع Anthropic ‏`/v1/messages`: يتصل **claude-code-router** أيضًا عبر `ANTHROPIC_BASE_URL`.

**معرّفات النماذج**: تجدها عبر `GET /v1/models` أو على [صفحة النماذج](https://pleum.ai/models). تجلب Cline وContinue وOpenCode وغيرها القائمة تلقائيًا. تُحوَّل معرّفات بصيغة OpenRouter (‏`openai/gpt-5.5`) تلقائيًا.

**وكيل LiteLLM** (‏Aider وOpenHands وOpen Interpreter وSWE-agent وgptme مبنية على LiteLLM وتتصل مباشرة — لكن إن كنت تستخدم وكيل LiteLLM):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # البادئة openai/ ← مسار متوافق مع OpenAI
      api_base: https://router.pleum.ai/v1           # لا تُلحق /chat/completions
      api_key: os.environ/PLEUM_API_KEY
```

---

## المساهمة

هل جعلت PleumRouter يعمل مع أداة غير مدرجة هنا؟ طلبات السحب (PRs) مرحّب بها — أضِف قسمًا يتضمن مقتطف إعداد **مُختبَر** (العنوان الأساس، ومتغيّر بيئة المفتاح، وصيغة معرّف النموذج، وأي مطبّات معروفة).

## الترخيص

[MIT](LICENSE)
