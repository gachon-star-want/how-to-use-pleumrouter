<div align="center">

# PleumRouter አጠቃቀም

**ከ200+ በላይ የAI ሞዴሎች ለአንድ API ቁልፍ — ከOpenAI ጋር ተኳሃኝ፣ በKRW ተመንዘሮ ይከፈላል።**

[ድረ-ገጽ](https://pleum.ai) · [ሰነዶች](https://pleum.ai/docs) · [ሞዴሎች](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · አማርኛ · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter የAI መግቢያ በር (gateway) ነው፦ አንድ ቁልፍ (`plm_…`)፣ አንድ base URL፣ ከ18 አቅራቢዎች የተገኙ 210+ ሞዴሎች — GPT፣ Claude፣ Gemini፣ DeepSeek፣ Qwen፣ EXAONE እና ሌሎችም። **OpenAI Chat Completions**፣ **Anthropic Messages**፣ እና **OpenAI Responses**ን ይናገራል፣ ስለዚህ ማለት ይቻላል እያንዳንዱ የኮዲንግ ወኪል (coding agent)፣ የIDE ተጨማሪ (plugin)፣ እና SDK በአንድ መስመር ውቅር (config) ለውጥ ብቻ ይገናኛል። ጽሑፍ፣ embeddings፣ ምስል፣ ድምፅ እና ቪዲዮ ሁሉም በተመሳሳይ ቁልፍ ውስጥ ያልፋሉ።

ይህ repo **የተረጋገጡ የውህደት (integration) የምግብ አዘገጃጀቶችን** ይሰበስባል። ከታች ያለው እያንዳንዱ ኮድ ቁራጭ በቀጥታ (live) gateway ላይ ተፈትኗል።

## መጀመሪያ ደረጃዎች

1. [ይመዝገቡ](https://pleum.ai/signup) → Dashboard → **API Keys** → ቁልፍ ያውጡ (በ`plm_` ይጀምራል)።
2. መሣሪያዎ base URLን እንዲያመለክት ያድርጉ፦

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Some agents (OpenCode, Crush) read PLEUM_API_KEY — same key, set both.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. የሙከራ ምርመራ (smoke test)፦

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

በምዝገባ ጊዜ ₩1,000 ነጻ ክሬዲት እና በመጀመሪያ ኃርጅ (top-up) ላይ ₩5,000 ጉርሻ ያገኛሉ።

## ውህደቶች (Integrations)

| ምድብ | መሣሪያዎች |
|---|---|
| [⚡ በአንድ-ትዕዛዝ ማስጀመሪያ](#-pleum-cli--ፈጣኑ-መንገድ) | `pleum` CLI |
| [🤖 የተርሚናል ኮዲንግ ወኪሎች](#-ተርሚናል--cli-ወኪሎች) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE / GUI ወኪሎች](#-ide--gui-ወኪሎች) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDKs](#-sdks) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 Multimodal API](#-multimodal--ምስል--ድምፅ--ቪዲዮ) | Images, TTS, STT, Video, Embeddings |
| [🔌 ሌላ ማንኛውም ነገር](#-ተጨማሪ-ወኪሎች) | OpenRouter-style IDs, LiteLLM proxy, 15+ more agents |

---

## ⚡ pleum CLI — ፈጣኑ መንገድ

ኦፊሴላዊው CLI የሚወዱትን ወኪል ወዲያውኑ ከPleumRouter ጋር ተያይዞ ያስጀምረዋል። ምንም የውቅር (config) ፋይል አይነካም።

```bash
npm install -g pleumrouter        # or: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # browser login, key auto-issued & saved
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # terminal chat REPL
pleum models                      # list all models with pricing
```

በራስ-ማስጀመሪያ (auto-launch) የሚደገፉት፦ `claude` · `aider` · `codex` · `goose` · `openhands` (ከዚህ በተጨማሪ ለ`opencode` · `crush` የውቅር (config) ቁርጥራጮች ይገኛሉ)። ነባር የመሣሪያ ውቅሮችዎ (configs) በፍጹም አይለወጡም።

---

## 🤖 ተርሚናል / CLI ወኪሎች

### Claude Code (ከAnthropic ጋር ተኳሃኝ)

Claude Code እና Claude Agent SDK መሣሪያዎች ከAnthropic ጋር ተኳሃኝ በሆነው `/v1/messages` መጨረሻ ነጥብ (endpoint) በኩል ይገናኛሉ።

```bash
# ANTHROPIC_BASE_URL is the ROOT (no /v1) — the CLI appends /v1/messages itself.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# The official CLI prefers ANTHROPIC_API_KEY; set both to be safe.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ `ANTHROPIC_BASE_URL` ውስጥ `/v1` **አያስገቡ** — ወደ `/v1/v1/messages` ይቀየርና ይከሽፋል። የመሣሪያ ጥሪዎች (tool calls) እና streaming ወደ OpenAI-ተኳሃኝ ሞዴሎች ቢመሩ እንኳ ከጫፍ እስከ ጫፍ ይሠራሉ።

### Codex CLI (Responses API)

Codex በOpenAI Responses API (`/v1/responses`) በኩል ይገናኛል፤ የChat Completions መንገድ ከየካቲት 2026 ጀምሮ ከCodex ተወግዷል።

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

የላይኛው ጅረት (upstream) Gemini CLI ለውጫዊ OpenAI-ተኳሃኝ መጨረሻ ነጥቦች (endpoints) ደካማ ድጋፍ አለው፤ OpenAI-ተኳሃኝ ማጣቀሻ (wrapper) ወይም fork ሊያስፈልግዎ ይችላል።

---

## 🖥 IDE / GUI ወኪሎች

### Cline · Roo Code · Kilo Code · Cursor

**OpenAI Compatible** (ወይም **Custom OpenAI**)ን እንደ አቅራቢ (provider) ይምረጡ እና ይህን ይለጥፉ፦

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ ሁልጊዜ **የOpenAI Compatible ማስገቢያውን (slot)** ይጠቀሙ — ልዩ የOpenRouter ማስገቢያ ወደ openrouter.ai በጥብቅ ተያይዞ (hardcoded) ተቀምጦ ስለሆነ ይከሽፋል። **Cursor** በbase URL ውስጥ `/v1`ን እና ባዶ ያልሆነ የቁልፍ ሜዳ (field) ይጠይቃል። **Kilo Code** የታወቀ ችግር (#681) አለው፦ ብጁ (custom) base URL ወደ ሞዴል ዝርዝር (listing) አይተላለፍም — የሞዴል ID በእጅ ያስገቡ።

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

በ`model: AUTODETECT` Continue የሞዴል ዝርዝሩን በራስ-ሰር ይጎትታል።

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

የሜዳ ስሞች (field names) እንደ Zed ስሪት (version) ሊለያዩ ይችላሉ — የZed ሰነዶችን ይመልከቱ።

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

## 🎨 Multimodal — ምስል · ድምፅ · ቪዲዮ

ሁሉም ግብዓት-አይነቶች (modalities) በተመሳሳይ ቁልፍ ላይ የOpenAI-ተኳሃኝ HTTP መጨረሻ ነጥቦች (endpoints) ናቸው። ግብዓት-አይነቱን ከ[`GET /v1/models`](https://pleum.ai/models) ከሚደግፍ ሞዴል ይምረጡ።

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

### API ገጽታ (surface)

| መጨረሻ ነጥብ (Endpoint) | ፕሮቶኮል |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (streaming, tools, vision) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | የምስል መፍጠር |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Async ቪዲዮ |
| `GET /v1/models` | የሞዴል ካታሎግ (ይፋዊ) |
| `GET /v1/credits` | ቀሪ ሂሳብ (Balance) |

---

## 🔌 ተጨማሪ ወኪሎች

እዚህ ያልተዘረዘሩ አብዛኞቹ ወኪሎች በተመሳሳይ መንገድ ይሠራሉ — የOpenAI-ተኳሃኝ base URLን ያዘጋጁ፦

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** እና ሌሎችም።

በAnthropic-ተኳሃኝ `/v1/messages` በኩል፦ **claude-code-router**ም ከ`ANTHROPIC_BASE_URL` ጋር ይገናኛል።

**የሞዴል IDዎች**፦ በ`GET /v1/models` ወይም በ[ሞዴሎች ገጽ](https://pleum.ai/models) ላይ ያገኙዋቸዋል። Cline፣ Continue፣ OpenCode እና ሌሎችም ዝርዝሩን በራስ-ሰር ይጎትታሉ። የOpenRouter-ቅርጸት IDዎች (`openai/gpt-5.5`) በራስ-ሰር ይቀየራሉ።

**LiteLLM proxy** (Aider፣ OpenHands፣ Open Interpreter፣ SWE-agent እና gptme በLiteLLM ላይ የተመሠረቱ ናቸውና በቀጥታ ይገናኛሉ — ነገር ግን LiteLLM proxy የሚያቆዩ ከሆነ)፦

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

## አስተዋፅዖ ማድረግ (Contributing)

PleumRouterን እዚህ ካልተዘረዘረ መሣሪያ ጋር አሠርተውታል? PR እንኳን ደህና መጡ — **የተፈተነ** የውቅር (config) ቁራጭ (base URL፣ key env፣ የሞዴል ID ቅርጸት፣ እና ማንኛውም ወጥመዶች) ያለው ክፍል ይጨምሩ።

## ፈቃድ (License)

[MIT](LICENSE)
