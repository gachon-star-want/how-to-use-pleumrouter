<div align="center">

# איך להשתמש ב-PleumRouter

**מפתח API אחד ל-200+ מודלי בינה מלאכותית — תואם OpenAI, מחויב בוונים קוריאניים (KRW).**

[אתר](https://pleum.ai) · [תיעוד](https://pleum.ai/docs) · [מודלים](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · עברית · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter הוא שער בינה מלאכותית (AI gateway): מפתח אחד (`plm_…`), כתובת בסיס אחת, 210+ מודלים מ-18 ספקים — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE ועוד. הוא תומך ב-**OpenAI Chat Completions**, ב-**Anthropic Messages** וב-**OpenAI Responses**, כך שכמעט כל סוכן קידוד, תוסף IDE וערכת פיתוח (SDK) מתחברים באמצעות שינוי תצורה של שורה אחת. טקסט, embeddings, תמונה, דיבור ווידאו — כולם פועלים דרך אותו מפתח.

מאגר זה אוסף **מתכוני שילוב מאומתים**. כל קטע קוד להלן נבדק מול השער החי (live gateway).

## תחילת העבודה

1. [הרשמה](https://pleum.ai/signup) ← לוח בקרה ← **מפתחות API** ← הנפקת מפתח (מתחיל ב-`plm_`).
2. הפנו את הכלי שלכם לכתובת הבסיס:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# חלק מהסוכנים (OpenCode, Crush) קוראים PLEUM_API_KEY — אותו מפתח, הגדירו את שניהם.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. בדיקת תקינות:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

תקבלו ₩1,000 קרדיט חינם עם ההרשמה ובונוס של ₩5,000 בטעינה הראשונה.

## שילובים (Integrations)

| קטגוריה | כלים |
|---|---|
| [⚡ מפעיל בפקודה אחת](#-pleum-cli--הנתיב-המהיר) | `pleum` CLI |
| [🤖 סוכני קידוד בטרמינל](#-סוכני-טרמינל--cli) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 סוכני IDE / GUI](#-סוכני-ide--gui) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 ערכות פיתוח (SDKs)](#-ערכות-פיתוח-sdks) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 API מולטימודלי](#-מולטימודלי--תמונה--שמע--וידאו) | תמונות, TTS, STT, וידאו, Embeddings |
| [🔌 כל השאר](#-עוד-סוכנים) | מזהים בסגנון OpenRouter, פרוקסי LiteLLM, 15+ סוכנים נוספים |

---

## ⚡ pleum CLI — הנתיב המהיר

ה-CLI הרשמי מפעיל את הסוכן המועדף עליכם כשהוא כבר מחובר ל-PleumRouter. שום קובץ תצורה לא נגע.

```bash
npm install -g pleumrouter        # או: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # התחברות דרך הדפדפן, מפתח מונפק ונשמר אוטומטית
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # REPL צ'אט בטרמינל
pleum models                      # הצגת כל המודלים כולל תמחור
```

נתמך להפעלה אוטומטית: `claude` · `aider` · `codex` · `goose` · `openhands` (בנוסף לקטעי תצורה עבור `opencode` · `crush`). תצורות הכלים הקיימות שלכם לעולם לא משתנות.

---

## 🤖 סוכני טרמינל / CLI

### Claude Code (תואם Anthropic)

Claude Code וכלי Claude Agent SDK מתחברים דרך נקודת הקצה התואמת ל-Anthropic, `/v1/messages`.

```bash
# ANTHROPIC_BASE_URL הוא ה-ROOT (ללא /v1) — ה-CLI מוסיף בעצמו /v1/messages.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# ה-CLI הרשמי מעדיף ANTHROPIC_API_KEY; הגדירו את שניהם ליתר ביטחון.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ **אל** תכניסו `/v1` לתוך `ANTHROPIC_BASE_URL` — זה הופך ל-`/v1/v1/messages` ונכשל. קריאות לכלים (tool calls) והזרמה (streaming) פועלות מקצה לקצה, גם כשהניתוב מבוצע למודלים תואמי-OpenAI.

### Codex CLI (Responses API)

Codex מתחבר דרך OpenAI Responses API (‏`/v1/responses`); נתיב Chat Completions הוסר מ-Codex בפברואר 2026.

```toml
# ~/.codex/config.toml
# model / model_provider הם מפתחות ברמת שורש המסמך (document-root) — חייבים להופיע מעל ה-[table].
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex מוסיף /responses ← /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex תומך רק ב-Responses API
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
// opencode.json   (או: /connect ← Other)
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

# Goose / OpenHands: הוסיפו את הקידומת openai/ למזהה המודל
#   model = openai/gpt-4.1
```

### Gemini CLI

לגרסת המקור (upstream) של Gemini CLI יש תמיכה חלשה בנקודות קצה חיצוניות תואמות-OpenAI; ייתכן שתזדקקו לעטיפה (wrapper) תואמת-OpenAI או ל-fork.

---

## 🖥 סוכני IDE / GUI

### Cline · Roo Code · Kilo Code · Cursor

בחרו **OpenAI Compatible** (או **Custom OpenAI**) כספק, והדביקו:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ השתמשו תמיד ב-**חריץ OpenAI Compatible** — הערך הייעודי של OpenRouter מקודד-קשיח (hardcoded) ל-openrouter.ai ויכשל. **Cursor** דורש `/v1` בכתובת הבסיס ושדה מפתח שאינו ריק. ל-**Kilo Code** יש תקלה ידועה (#681) שבה כתובת הבסיס המותאמת אישית אינה מועברת לרשימת המודלים — הזינו את מזהה המודל ידנית.

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

עם `model: AUTODETECT‎`, Continue שולף את רשימת המודלים אוטומטית.

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

שמות השדות עשויים להשתנות בין גרסאות Zed — בדקו את תיעוד Zed.

---

## 📦 ערכות פיתוח (SDKs)

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
    base_url="https://router.pleum.ai",   # root, ללא /v1 — ה-SDK מוסיף /v1/messages
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # כל מודל של PleumRouter עובד
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 מולטימודלי — תמונה · שמע · וידאו

כל המודליות הן נקודות קצה HTTP תואמות-OpenAI תחת אותו מפתח. בחרו מודל שתומך במודליות הרצויה מתוך [`GET /v1/models`](https://pleum.ai/models).

```bash
# יצירת תמונה
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# המרת טקסט לדיבור (Text-to-speech; מחזיר בייטים של שמע; העלות בכותרת X-Cost-Krw)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# המרת דיבור לטקסט (Speech-to-text; העלאה מסוג multipart)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# יצירת וידאו היא אסינכרונית: בקשת POST מחזירה job_id, ולאחר מכן בצעו polling ל-GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### שטח ה-API (API surface)

| נקודת קצה | פרוטוקול |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (הזרמה, כלים, ראייה) |
| `POST /v1/messages` | Anthropic Messages (‏Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (‏Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | יצירת תמונות |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | וידאו אסינכרוני |
| `GET /v1/models` | קטלוג מודלים (ציבורי) |
| `GET /v1/credits` | יתרה |

---

## 🔌 עוד סוכנים

רוב הסוכנים שלא מופיעים כאן פועלים באותו אופן — הגדירו את כתובת הבסיס התואמת-OpenAI:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** ועוד.

דרך `/v1/messages` התואם ל-Anthropic: גם **claude-code-router** מתחבר באמצעות `ANTHROPIC_BASE_URL`.

**מזהי מודלים**: מצאו אותם דרך `GET /v1/models` או ב[עמוד המודלים](https://pleum.ai/models). ‏Cline, Continue, OpenCode ואחרים שולפים את הרשימה אוטומטית. מזהים בפורמט OpenRouter (‏`openai/gpt-5.5`) מומרים אוטומטית.

**פרוקסי LiteLLM** (‏Aider, OpenHands, Open Interpreter, SWE-agent ו-gptme מבוססים על LiteLLM ומתחברים ישירות — אך אם אתם שומרים על פרוקסי LiteLLM):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # קידומת openai/ ← נתיב תואם-OpenAI
      api_base: https://router.pleum.ai/v1           # אל תוסיפו /chat/completions
      api_key: os.environ/PLEUM_API_KEY
```

---

## תרומה לפרויקט

הצלחתם להריץ את PleumRouter עם כלי שלא מופיע כאן? מוזמנים לפתוח Pull Request — הוסיפו סעיף עם קטע תצורה **שנבדק בפועל** (כתובת בסיס, משתנה סביבה של המפתח, פורמט מזהה המודל, וכל תקלה ידועה).

## רישיון

[MIT](LICENSE)
