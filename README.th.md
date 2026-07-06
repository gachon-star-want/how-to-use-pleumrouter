<div align="center">

# วิธีใช้ PleumRouter

**คีย์ API เดียวสำหรับโมเดล AI กว่า 200 ตัว — เข้ากันได้กับ OpenAI เรียกเก็บเงินเป็นวอนเกาหลี (KRW)**

[เว็บไซต์](https://pleum.ai) · [เอกสาร](https://pleum.ai/docs) · [โมเดล](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · ไทย · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter คือเกตเวย์ AI: คีย์เดียว (`plm_…`) URL ฐานเดียว โมเดลกว่า 210 ตัวจาก 18 ผู้ให้บริการ — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE และอื่น ๆ อีกมากมาย รองรับ **OpenAI Chat Completions**, **Anthropic Messages** และ **OpenAI Responses** ทำให้โค้ดดิ้งเอเจนต์ ปลั๊กอิน IDE และ SDK เกือบทุกตัวเชื่อมต่อได้ด้วยการเปลี่ยนค่าคอนฟิกเพียงบรรทัดเดียว ทั้งข้อความ embeddings รูปภาพ เสียง และวิดีโอต่างก็ทำงานผ่านคีย์เดียวกัน

รีโปนี้รวบรวม **สูตรการเชื่อมต่อที่ผ่านการยืนยันแล้ว** ทุกสนิปเป็ตด้านล่างได้รับการทดสอบกับเกตเวย์จริง

## เริ่มต้นใช้งาน

1. [สมัครสมาชิก](https://pleum.ai/signup) → แดชบอร์ด → **API Keys** → ออกคีย์ (ขึ้นต้นด้วย `plm_`)
2. ชี้เครื่องมือของคุณไปที่ URL ฐาน:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# เอเจนต์บางตัว (OpenCode, Crush) อ่านค่า PLEUM_API_KEY — เป็นคีย์เดียวกัน ให้ตั้งค่าทั้งสองตัว
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. ทดสอบระบบ:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

คุณจะได้เครดิตฟรี ₩1,000 เมื่อสมัครสมาชิก และโบนัส ₩5,000 เมื่อเติมเงินครั้งแรก

## การเชื่อมต่อ

| หมวดหมู่ | เครื่องมือ |
|---|---|
| [⚡ ตัวเรียกใช้งานคำสั่งเดียว](#-pleum-cli-—-เส้นทางที่รวดเร็ว) | `pleum` CLI |
| [🤖 เอเจนต์โค้ดดิ้งแบบเทอร์มินัล](#-เอเจนต์เทอร์มินัล--cli) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 เอเจนต์ IDE / GUI](#-เอเจนต์-ide--gui) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK](#-sdk) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 API มัลติโมดัล](#-มัลติโมดัล--รูปภาพ--เสียง--วิดีโอ) | รูปภาพ, TTS, STT, วิดีโอ, Embeddings |
| [🔌 อื่น ๆ ทั้งหมด](#-เอเจนต์อื่น-ๆ-เพิ่มเติม) | ID รูปแบบ OpenRouter, พร็อกซี LiteLLM, เอเจนต์อื่น ๆ อีก 15+ ตัว |

---

## ⚡ pleum CLI — เส้นทางที่รวดเร็ว

CLI อย่างเป็นทางการจะเปิดใช้งานเอเจนต์ที่คุณชื่นชอบโดยเชื่อมต่อกับ PleumRouter ไว้ล่วงหน้า ไม่ต้องแตะไฟล์คอนฟิกใด ๆ

```bash
npm install -g pleumrouter        # หรือ: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # ล็อกอินผ่านเบราว์เซอร์ ระบบออกคีย์และบันทึกให้อัตโนมัติ
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # REPL แชทในเทอร์มินัล
pleum models                      # แสดงรายการโมเดลทั้งหมดพร้อมราคา
```

รองรับการเปิดใช้งานอัตโนมัติสำหรับ: `claude` · `aider` · `codex` · `goose` · `openhands` (พร้อมสนิปเป็ตคอนฟิกสำหรับ `opencode` · `crush`) คอนฟิกเครื่องมือเดิมของคุณจะไม่ถูกแก้ไขเลย

---

## 🤖 เอเจนต์เทอร์มินัล / CLI

### Claude Code (เข้ากันได้กับ Anthropic)

Claude Code และเครื่องมือ Claude Agent SDK เชื่อมต่อผ่านเอนด์พอยต์ `/v1/messages` ที่เข้ากันได้กับ Anthropic

```bash
# ANTHROPIC_BASE_URL คือ ROOT (ไม่มี /v1) — CLI จะเติม /v1/messages ให้เอง
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# CLI อย่างเป็นทางการนิยมใช้ ANTHROPIC_API_KEY ให้ตั้งค่าทั้งสองตัวเพื่อความปลอดภัย
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ **ห้าม**ใส่ `/v1` ใน `ANTHROPIC_BASE_URL` — เพราะจะกลายเป็น `/v1/v1/messages` และล้มเหลว การเรียกใช้เครื่องมือ (tool calls) และการสตรีมทำงานได้ครบวงจร แม้จะถูกส่งไปยังโมเดลที่เข้ากันได้กับ OpenAI ก็ตาม

### Codex CLI (Responses API)

Codex เชื่อมต่อผ่าน OpenAI Responses API (`/v1/responses`) เส้นทาง Chat Completions ถูกลบออกจาก Codex ตั้งแต่เดือนกุมภาพันธ์ 2026

```toml
# ~/.codex/config.toml
# model / model_provider เป็นคีย์ระดับรากของเอกสาร (ต้องอยู่เหนือ [table])
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex จะเติม /responses → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex รองรับเฉพาะ Responses API เท่านั้น
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
// opencode.json   (หรือ: /connect → Other)
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

# Goose / OpenHands: เติมคำนำหน้า openai/ ที่ ID ของโมเดล
#   model = openai/gpt-4.1
```

### Gemini CLI

Gemini CLI ต้นทางยังรองรับเอนด์พอยต์ที่เข้ากันได้กับ OpenAI จากภายนอกได้ไม่ดีนัก คุณอาจต้องใช้ wrapper หรือ fork ที่เข้ากันได้กับ OpenAI

---

## 🖥 เอเจนต์ IDE / GUI

### Cline · Roo Code · Kilo Code · Cursor

เลือก **OpenAI Compatible** (หรือ **Custom OpenAI**) เป็นผู้ให้บริการ แล้ววาง:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ ใช้ **ช่อง OpenAI Compatible** เสมอ — ช่องเฉพาะสำหรับ OpenRouter ถูกฝังค่าตายตัวไว้ที่ openrouter.ai และจะล้มเหลว **Cursor** ต้องใส่ `/v1` ใน base URL และช่องคีย์ต้องไม่ว่างเปล่า **Kilo Code** มีปัญหาที่ทราบแล้ว (#681) ที่ base URL แบบกำหนดเองไม่ถูกส่งไปยังรายการโมเดล — ให้กรอก ID โมเดลด้วยตนเอง

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

เมื่อใช้ `model: AUTODETECT` Continue จะดึงรายการโมเดลมาโดยอัตโนมัติ

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

ชื่อฟิลด์อาจแตกต่างกันไปตามเวอร์ชันของ Zed — ตรวจสอบเอกสาร Zed

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
    base_url="https://router.pleum.ai",   # root ไม่มี /v1 — SDK จะเติม /v1/messages เอง
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # ใช้โมเดลใดของ PleumRouter ก็ได้
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 มัลติโมดัล — รูปภาพ · เสียง · วิดีโอ

ทุกโมดัลิตีเป็นเอนด์พอยต์ HTTP ที่เข้ากันได้กับ OpenAI บนคีย์เดียวกัน เลือกโมเดลที่รองรับโมดัลิตีนั้นจาก [`GET /v1/models`](https://pleum.ai/models)

```bash
# การสร้างรูปภาพ
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# แปลงข้อความเป็นเสียง (ส่งคืนไบต์เสียง ค่าใช้จ่ายอยู่ในเฮดเดอร์ X-Cost-Krw)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# แปลงเสียงเป็นข้อความ (อัปโหลดแบบ multipart)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# การสร้างวิดีโอเป็นแบบอะซิงโครนัส: POST จะส่งคืน job_id จากนั้น poll ที่ GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### API ที่เปิดให้ใช้งาน

| เอนด์พอยต์ | โปรโตคอล |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (สตรีมมิง, เครื่องมือ, การมองเห็น) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | การสร้างรูปภาพ |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | วิดีโอแบบอะซิงโครนัส |
| `GET /v1/models` | แคตตาล็อกโมเดล (สาธารณะ) |
| `GET /v1/credits` | ยอดคงเหลือ |

---

## 🔌 เอเจนต์อื่น ๆ เพิ่มเติม

เอเจนต์ส่วนใหญ่ที่ไม่ได้ระบุไว้ที่นี่ทำงานในลักษณะเดียวกัน — ตั้งค่า URL ฐานที่เข้ากันได้กับ OpenAI:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** และอื่น ๆ อีกมากมาย

ผ่าน `/v1/messages` ที่เข้ากันได้กับ Anthropic: **claude-code-router** ก็เชื่อมต่อได้ด้วย `ANTHROPIC_BASE_URL` เช่นกัน

**ID โมเดล**: ค้นหาได้ที่ `GET /v1/models` หรือที่[หน้าโมเดล](https://pleum.ai/models) Cline, Continue, OpenCode และเครื่องมืออื่น ๆ จะดึงรายการมาโดยอัตโนมัติ ID รูปแบบ OpenRouter (`openai/gpt-5.5`) จะถูกแปลงให้โดยอัตโนมัติ

**พร็อกซี LiteLLM** (Aider, OpenHands, Open Interpreter, SWE-agent และ gptme ใช้พื้นฐานจาก LiteLLM และเชื่อมต่อได้โดยตรง — แต่หากคุณยังคงใช้พร็อกซี LiteLLM):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # คำนำหน้า openai/ → เส้นทาง OpenAI-compat
      api_base: https://router.pleum.ai/v1           # ห้ามเติม /chat/completions ต่อท้าย
      api_key: os.environ/PLEUM_API_KEY
```

---

## การมีส่วนร่วม

ใช้งาน PleumRouter ได้สำเร็จกับเครื่องมือที่ไม่ได้ระบุไว้ที่นี่หรือไม่ ยินดีรับ PR — เพิ่มส่วนพร้อมสนิปเป็ตคอนฟิกที่**ผ่านการทดสอบแล้ว** (base URL, key env, รูปแบบ model ID และข้อควรระวังใด ๆ)

## สัญญาอนุญาต

[MIT](LICENSE)
