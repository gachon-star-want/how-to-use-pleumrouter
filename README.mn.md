<div align="center">

# PleumRouter-ийг хэрхэн ашиглах вэ

**200+ AI загварт зориулсан ганц API түлхүүр — OpenAI-тай нийцтэй, KRW-ээр тооцоо хийдэг.**

[Вэбсайт](https://pleum.ai) · [Баримт бичиг](https://pleum.ai/docs) · [Загварууд](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · Монгол · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter бол AI гарц (gateway) юм: нэг түлхүүр (`plm_…`), нэг үндсэн URL, 18 үйлчилгээ үзүүлэгчийн 210+ загвар — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE зэрэг олон загвар. Энэ нь **OpenAI Chat Completions**, **Anthropic Messages**, **OpenAI Responses** гурвыг дэмждэг тул бараг бүх coding agent, IDE залгаас (plugin), SDK нэг мөр тохиргоо өөрчлөхөд шууд холбогддог. Текст, эмбеддинг (embeddings), зураг, дуу хоолой болон видео — эдгээр бүгд нэг л түлхүүрээр ажилладаг.

Энэ репо нь **баталгаажсан интеграцийн жор**-уудыг цуглуулсан. Доорх бүх жишээ кодыг бодит гарц (live gateway) дээр туршиж шалгасан.

## Эхлэх нь

1. [Бүртгүүлэх](https://pleum.ai/signup) → Хяналтын самбар → **API Keys** → түлхүүр үүсгэх (`plm_`-ээр эхэлдэг).
2. Хэрэглэж буй хэрэгслээ үндсэн URL руу чиглүүлэх:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Зарим agent-ууд (OpenCode, Crush) PLEUM_API_KEY-г уншдаг — ижил түлхүүр, хоёуланг нь тохируулаарай.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Ажиллаж буйг шалгах:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Бүртгүүлэхэд ₩1,000 үнэгүй кредит, эхний цэнэглэлт дээр ₩5,000 урамшуулал олгоно.

## Интеграцууд

| Ангилал | Хэрэгслүүд |
|---|---|
| [⚡ Нэг-командт лончер](#-pleum-cli--хурдан-зам) | `pleum` CLI |
| [🤖 Терминалын coding agent-ууд](#-терминал--cli-agent-ууд) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE / GUI agent-ууд](#-ide--gui-agent-ууд) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK-ууд](#-sdk-ууд) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 Мультимодал API](#-мультимодал--зураг--аудио--видео) | Зураг, TTS, STT, Видео, Эмбеддинг |
| [🔌 Бусад бүгд](#-бусад-agent-ууд) | OpenRouter маягийн ID-ууд, LiteLLM прокси, 15+ бусад agent |

---

## ⚡ pleum CLI — хурдан зам

Албан ёсны CLI нь таны дуртай agent-ыг PleumRouter-т аль хэдийн холбосон байдлаар шууд лончилдог. Ямар ч тохиргооны файлд гар хүрэхгүй.

```bash
npm install -g pleumrouter        # эсвэл: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # хөтчөөр нэвтрэх, түлхүүр автоматаар үүсэж хадгалагдана
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # терминалын чат REPL
pleum models                      # бүх загварыг үнийн хамт жагсаах
```

Автомат-лончтой: `claude` · `aider` · `codex` · `goose` · `openhands` (мөн `opencode` · `crush`-д зориулсан тохиргооны жишээ кодтой). Таны одоо байгаа хэрэгслийн тохиргоог хэзээ ч өөрчлөхгүй.

---

## 🤖 Терминал / CLI agent-ууд

### Claude Code (Anthropic-тай нийцтэй)

Claude Code болон Claude Agent SDK хэрэгслүүд Anthropic-тай нийцтэй `/v1/messages` төгсгөл цэгээр холбогддог.

```bash
# ANTHROPIC_BASE_URL нь ROOT байх ёстой (/v1 байхгүй) — CLI өөрөө /v1/messages-ийг нэмдэг.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# Албан ёсны CLI нь ANTHROPIC_API_KEY-г илүүд үздэг; аюулгүй байдлын үүднээс хоёуланг нь тохируулна.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ `ANTHROPIC_BASE_URL`-д `/v1`-г **бүү оруул** — ингэвэл `/v1/v1/messages` болж алдаа гарна. OpenAI-тай нийцтэй загварт чиглүүлсэн үед ч гэсэн tool call болон стриминг бүрэн ажилладаг.

### Codex CLI (Responses API)

Codex нь OpenAI Responses API (`/v1/responses`)-аар холбогддог; Chat Completions замыг Codex-оос 2026 оны 2-р сард устгасан.

```toml
# ~/.codex/config.toml
# model / model_provider нь баримтын үндсэн (root) түлхүүрүүд ([table]-ийн дээр байх ёстой).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex /responses-ийг нэмнэ → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex зөвхөн Responses API-г дэмждэг
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
// opencode.json   (эсвэл: /connect → Other)
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

# Goose / OpenHands: загварын id-ын өмнө openai/ угтваргаа залгах
#   model = openai/gpt-4.1
```

### Gemini CLI

Албан ёсны (upstream) Gemini CLI нь гадаад OpenAI-тай нийцтэй төгсгөл цэгийг сул дэмждэг тул та OpenAI-тай нийцтэй wrapper эсвэл fork ашиглах шаардлагатай байж болно.

---

## 🖥 IDE / GUI agent-ууд

### Cline · Roo Code · Kilo Code · Cursor

**OpenAI Compatible** (эсвэл **Custom OpenAI**)-г үйлчилгээ үзүүлэгчээр сонгож дараахыг оруулна:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Ямагт **OpenAI Compatible слот**-ыг ашиглаарай — тусгайлсан OpenRouter оруулга нь openrouter.ai руу хатуу кодлогдсон тул амжилтгүй болно. **Cursor**-т үндсэн URL-д `/v1` заавал байх ёстой бөгөөд түлхүүрийн талбар хоосон байж болохгүй. **Kilo Code**-д мэдэгдэж буй асуудал (#681) байгаа бөгөөд custom base URL нь загварын жагсаалт татахад дамжигддаггүй — загварын ID-г гараар оруулна уу.

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

`model: AUTODETECT` тохиргоотой үед Continue загварын жагсаалтыг автоматаар татдаг.

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

Талбарын нэрс Zed-ийн хувилбараас хамаарч өөр байж болно — Zed-ийн баримт бичгээс шалгаарай.

---

## 📦 SDK-ууд

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
    base_url="https://router.pleum.ai",   # root, /v1 байхгүй — SDK өөрөө /v1/messages-ийг нэмнэ
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # PleumRouter-ийн ямар ч загвар ажиллана
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Мультимодал — зураг · аудио · видео

Бүх модалити (modality) нь ижил түлхүүр дээр ажилладаг OpenAI-тай нийцтэй HTTP төгсгөл цэгүүд юм. [`GET /v1/models`](https://pleum.ai/models)-ээс тухайн модалитийг дэмждэг загвар сонгоно уу.

```bash
# Зураг үүсгэх
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Текст-с-яриа (audio байт буцаана; өртөг нь X-Cost-Krw толгойд байна)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Яриа-с-текст (multipart байдлаар upload хийх)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# Видео үүсгэлт нь async: POST хийхэд job_id буцаана, дараа нь GET /v1/jobs/{job_id}-г polling хийнэ
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### API гадаргуу (surface)

| Төгсгөл цэг | Протокол |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (стриминг, tool, харааны боловсруулалт) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Зураг үүсгэлт |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Async видео |
| `GET /v1/models` | Загварын каталог (нийтэд нээлттэй) |
| `GET /v1/credits` | Үлдэгдэл |

---

## 🔌 Бусад agent-ууд

Энд жагсаагаагүй ихэнх agent-ууд ижил аргаар ажилладаг — OpenAI-тай нийцтэй үндсэн URL-г тохируулна:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** болон бусад.

Anthropic-тай нийцтэй `/v1/messages`-ээр дамжуулан: **claude-code-router** ч мөн `ANTHROPIC_BASE_URL`-ээр холбогддог.

**Загварын ID-ууд**: `GET /v1/models`-ээс эсвэл [загваруудын хуудас](https://pleum.ai/models)-наас олоорой. Cline, Continue, OpenCode болон бусад нь жагсаалтыг автоматаар татдаг. OpenRouter форматтай ID-ууд (`openai/gpt-5.5`) автоматаар хөрвүүлэгддэг.

**LiteLLM прокси** (Aider, OpenHands, Open Interpreter, SWE-agent, gptme нь LiteLLM дээр суурилсан бөгөөд шууд холбогддог — гэхдээ хэрэв та LiteLLM прокси ашиглах бол):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # openai/ угтвар → OpenAI-compat зам
      api_base: https://router.pleum.ai/v1           # /chat/completions-ийг НЭМЖ БОЛОХГҮЙ
      api_key: os.environ/PLEUM_API_KEY
```

---

## Хувь нэмэр оруулах (Contributing)

Энд жагсаагаагүй хэрэгслээр PleumRouter-ийг ажиллуулж чадсан уу? PR-ийг тавтай хүлээж авна — **туршиж баталгаажуулсан** тохиргооны жишээ кодтой хэсэг (үндсэн URL, түлхүүрийн орчны хувьсагч, загварын ID формат, мөн анхаарах нюансуудын хамт) нэмээрэй.

## Лиценз

[MIT](LICENSE)
