<div align="center">

# PleumRouter ကို အသုံးပြုနည်း

**AI မော်ဒယ် 200+ အတွက် API key တစ်ခုတည်း — OpenAI-compatible, KRW ဖြင့် ငွေတောင်းခံသည်။**

[ဝဘ်ဆိုက်](https://pleum.ai) · [စာရွက်စာတမ်း](https://pleum.ai/docs) · [မော်ဒယ်များ](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · မြန်မာ · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter သည် AI gateway တစ်ခုဖြစ်သည်— key တစ်ခု (`plm_…`)၊ base URL တစ်ခု၊ provider 18 ခုမှ မော်ဒယ် 210+ — GPT၊ Claude၊ Gemini၊ DeepSeek၊ Qwen၊ EXAONE နှင့် နောက်ထပ်များစွာ။ ၎င်းသည် **OpenAI Chat Completions**၊ **Anthropic Messages** နှင့် **OpenAI Responses** တို့ကို ကိုင်တွယ်နိုင်သဖြင့် coding agent၊ IDE plugin၊ SDK အားလုံးနီးပါးကို config တစ်ကြောင်းသာ ပြောင်းလိုက်ရုံဖြင့် ချိတ်ဆက်နိုင်သည်။ Text၊ embeddings၊ image၊ speech နှင့် video အားလုံးကို key တစ်ခုတည်းဖြင့် အသုံးပြုနိုင်သည်။

ဤ repo တွင် **အတည်ပြုပြီးသား integration recipes** များကို စုစည်းထားသည်။ အောက်ပါ snippet တိုင်းကို live gateway ပေါ်တွင် စမ်းသပ်ထားပြီးဖြစ်သည်။

## စတင်အသုံးပြုနည်း

1. [Sign up](https://pleum.ai/signup) → Dashboard → **API Keys** → key တစ်ခု ထုတ်ပါ (`plm_` ဖြင့် စတင်သည်)။
2. သင့် tool ကို base URL သို့ ညွှန်းပါ။

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Some agents (OpenCode, Crush) read PLEUM_API_KEY — same key, set both.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. စမ်းသပ်စစ်ဆေးခြင်း။

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Sign up လုပ်လျှင် အခမဲ့ credit ₩1,000 ရရှိမည်ဖြစ်ပြီး ပထမဆုံးအကြိမ် top-up လုပ်လျှင် ₩5,000 bonus ရရှိမည်ဖြစ်သည်။

## Integration များ

| အမျိုးအစား | Tool များ |
|---|---|
| [⚡ One-command launcher](#-pleum-cli--အမြန်ဆုံးလမ်းကြောင်း) | `pleum` CLI |
| [🤖 Terminal coding agent များ](#-terminal--cli-agent-များ) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE / GUI agent များ](#-ide--gui-agent-များ) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK များ](#-sdk-များ) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 Multimodal API](#-multimodal--image--audio--video) | Images, TTS, STT, Video, Embeddings |
| [🔌 အခြားအားလုံး](#-နောက်ထပ်-agent-များ) | OpenRouter-style ID များ, LiteLLM proxy, agent 15+ ထပ်ပေါင်း |

---

## ⚡ pleum CLI — အမြန်ဆုံးလမ်းကြောင်း

Official CLI သည် သင်အနှစ်သက်ဆုံး agent ကို PleumRouter နှင့် ချိတ်ဆက်ပြီးသား အနေအထားဖြင့် စတင်ပေးသည်။ Config ဖိုင်များကို လက်မထိရပါ။

```bash
npm install -g pleumrouter        # or: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # browser login, key auto-issued & saved
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # terminal chat REPL
pleum models                      # list all models with pricing
```

Auto-launch အတွက် ပံ့ပိုးထားသည်— `claude` · `aider` · `codex` · `goose` · `openhands` (ထို့အပြင် `opencode` · `crush` အတွက် config snippet များ)။ သင့်ရှိပြီးသား tool config များကို ဘယ်တော့မှ ပြောင်းလဲမည် မဟုတ်ပါ။

---

## 🤖 Terminal / CLI agent များ

### Claude Code (Anthropic-compatible)

Claude Code နှင့် Claude Agent SDK tool များသည် Anthropic-compatible `/v1/messages` endpoint မှတစ်ဆင့် ချိတ်ဆက်ပါသည်။

```bash
# ANTHROPIC_BASE_URL is the ROOT (no /v1) — the CLI appends /v1/messages itself.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# The official CLI prefers ANTHROPIC_API_KEY; set both to be safe.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ `ANTHROPIC_BASE_URL` တွင် `/v1` ကို **မထည့်ပါနှင့်** — ၎င်းသည် `/v1/v1/messages` ဖြစ်သွားပြီး error တက်ပါလိမ့်မည်။ Tool call များနှင့် streaming သည် OpenAI-compatible မော်ဒယ်များသို့ route လုပ်ထားသည့်တိုင် အစအဆုံး အလုပ်လုပ်ပါသည်။

### Codex CLI (Responses API)

Codex သည် OpenAI Responses API (`/v1/responses`) မှတစ်ဆင့် ချိတ်ဆက်ပါသည်— Chat Completions path ကို Codex မှ 2026 ခုနှစ် ဖေဖော်ဝါရီလတွင် ဖယ်ရှားလိုက်ပါပြီ။

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

Upstream Gemini CLI သည် ပြင်ပ OpenAI-compatible endpoint များအတွက် အထောက်အပံ့ အားနည်းသည်— OpenAI-compatible wrapper သို့မဟုတ် fork တစ်ခု လိုအပ်နိုင်ပါသည်။

---

## 🖥 IDE / GUI agent များ

### Cline · Roo Code · Kilo Code · Cursor

Provider အနေဖြင့် **OpenAI Compatible** (သို့မဟုတ် **Custom OpenAI**) ကို ရွေးချယ်ပြီး အောက်ပါအတိုင်း ကူးထည့်ပါ။

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ **OpenAI Compatible slot** ကိုသာ အမြဲအသုံးပြုပါ — OpenRouter အတွက် သီးသန့်ထားသော entry သည် openrouter.ai အတွက် hardcode လုပ်ထားပြီး error တက်ပါလိမ့်မည်။ **Cursor** သည် base URL တွင် `/v1` ကို ထည့်ဖို့နှင့် key field ကို ဗလာမထားဖို့ လိုအပ်ပါသည်။ **Kilo Code** တွင် သိထားပြီးသား ပြဿနာ (#681) ရှိသည်— custom base URL ကို model listing သို့ ဖြတ်ပေးမထားသဖြင့် model ID ကို ကိုယ်တိုင် ရိုက်ထည့်ပါ။

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

`model: AUTODETECT` ဖြင့် Continue သည် model list ကို အလိုအလျောက် ဆွဲထုတ်ပါသည်။

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

Field နာမည်များသည် Zed version အလိုက် ကွဲပြားနိုင်သည် — Zed documentation ကို စစ်ဆေးပါ။

---

## 📦 SDK များ

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

## 🎨 Multimodal — image · audio · video

Modality အားလုံးသည် key တစ်ခုတည်းပေါ်ရှိ OpenAI-compatible HTTP endpoint များဖြစ်ပါသည်။ [`GET /v1/models`](https://pleum.ai/models) မှ modality ကို ပံ့ပိုးထားသော မော်ဒယ်တစ်ခုကို ရွေးချယ်ပါ။

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

### API surface

| Endpoint | Protocol |
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

## 🔌 နောက်ထပ် agent များ

ဤနေရာတွင် မဖော်ပြထားသော agent အများစုသည် နည်းလမ်းတူတူ အလုပ်လုပ်ပါသည်— OpenAI-compatible base URL ကို သတ်မှတ်ပေးရုံသာဖြစ်သည်။

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** နှင့် နောက်ထပ်များစွာ။

Anthropic-compatible `/v1/messages` မှတစ်ဆင့်— **claude-code-router** သည်လည်း `ANTHROPIC_BASE_URL` ဖြင့် ချိတ်ဆက်ပါသည်။

**Model ID များ**: ၎င်းတို့ကို `GET /v1/models` တွင် သို့မဟုတ် [models page](https://pleum.ai/models) တွင် ရှာဖွေနိုင်ပါသည်။ Cline၊ Continue၊ OpenCode နှင့် အခြား tool များက list ကို အလိုအလျောက် ဆွဲထုတ်ကြပါသည်။ OpenRouter-format ID များ (`openai/gpt-5.5`) ကို အလိုအလျောက် ပြောင်းလဲပေးပါသည်။

**LiteLLM proxy** (Aider၊ OpenHands၊ Open Interpreter၊ SWE-agent နှင့် gptme တို့သည် LiteLLM-based ဖြစ်ပြီး တိုက်ရိုက် ချိတ်ဆက်ပါသည် — သို့သော် LiteLLM proxy တစ်ခု ဆက်လက်ထိန်းထားလျှင်)။

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

## Contributing

ဤနေရာတွင် မပါဝင်သေးသော tool တစ်ခုနှင့် PleumRouter ကို အောင်မြင်စွာ အလုပ်လုပ်စေနိုင်ပါသလား။ PR များကို ကြိုဆိုပါသည် — **စမ်းသပ်ပြီးသား** config snippet (base URL၊ key env၊ model ID format နှင့် သတိပေးစရာများ) ပါဝင်သော section တစ်ခု ထည့်ပေးပါ။

## License

[MIT](LICENSE)
