<div align="center">

# PleumRouter ఎలా ఉపయోగించాలి

**200+ AI మోడల్స్ కోసం ఒకే API కీ — OpenAI-compatible, KRWలో బిల్లింగ్.**

[వెబ్‌సైట్](https://pleum.ai) · [డాక్స్](https://pleum.ai/docs) · [మోడల్స్](https://pleum.ai/models) · [ప్లేగ్రౌండ్](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · తెలుగు · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter అనేది ఒక AI గేట్‌వే: ఒకే కీ (`plm_…`), ఒకే బేస్ URL, 18 ప్రొవైడర్ల నుండి 210+ మోడల్స్ — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE మరియు మరెన్నో. ఇది **OpenAI Chat Completions**, **Anthropic Messages**, మరియు **OpenAI Responses**ని మాట్లాడుతుంది, కాబట్టి దాదాపు ప్రతి కోడింగ్ ఏజెంట్, IDE ప్లగిన్, మరియు SDK ఒక్క లైన్ కాన్ఫిగ్ మార్పుతో కనెక్ట్ అవుతుంది. టెక్స్ట్, ఎంబెడింగ్‌లు, ఇమేజ్, స్పీచ్ మరియు వీడియో అన్నీ ఒకే కీ ద్వారా నడుస్తాయి.

ఈ రిపో **వెరిఫై చేసిన ఇంటిగ్రేషన్ రెసిపీలను** సేకరిస్తుంది. కింద ఉన్న ప్రతి స్నిప్పెట్ లైవ్ గేట్‌వేకి వ్యతిరేకంగా టెస్ట్ చేయబడింది.

## మొదలుపెట్టడం

1. [సైన్ అప్ చేయండి](https://pleum.ai/signup) → Dashboard → **API Keys** → ఒక కీని జారీ చేయండి (`plm_` తో మొదలవుతుంది).
2. మీ టూల్‌ని బేస్ URLకి పాయింట్ చేయండి:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Some agents (OpenCode, Crush) read PLEUM_API_KEY — same key, set both.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. స్మోక్ టెస్ట్:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

మీకు సైన్అప్‌పై ₩1,000 ఉచిత క్రెడిట్ మరియు మీ మొదటి టాప్-అప్‌పై ₩5,000 బోనస్ లభిస్తుంది.

## ఇంటిగ్రేషన్‌లు

| వర్గం | టూల్స్ |
|---|---|
| [⚡ వన్-కమాండ్ లాంచర్](#-pleum-cli-వేగవంతమైన-మార్గం) | `pleum` CLI |
| [🤖 టెర్మినల్ కోడింగ్ ఏజెంట్లు](#-టెర్మినల్--cli-ఏజెంట్లు) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE / GUI ఏజెంట్లు](#-ide--gui-ఏజెంట్లు) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDKలు](#-sdkలు) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 మల్టీమోడల్ API](#-మల్టీమోడల్--ఇమేజ్--ఆడియో--వీడియో) | Images, TTS, STT, Video, Embeddings |
| [🔌 మిగతావన్నీ](#-మరిన్ని-ఏజెంట్లు) | OpenRouter-style IDs, LiteLLM proxy, 15+ మరిన్ని ఏజెంట్లు |

---

## ⚡ pleum CLI — వేగవంతమైన మార్గం

అధికారిక CLI మీకు ఇష్టమైన ఏజెంట్‌ని PleumRouterకి ఇప్పటికే వైర్ చేసి లాంచ్ చేస్తుంది. కాన్ఫిగ్ ఫైల్స్ దేనినీ తాకదు.

```bash
npm install -g pleumrouter        # or: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # browser login, key auto-issued & saved
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # terminal chat REPL
pleum models                      # list all models with pricing
```

ఆటో-లాంచ్ కోసం సపోర్ట్ చేయబడేవి: `claude` · `aider` · `codex` · `goose` · `openhands` (అలాగే `opencode` · `crush` కోసం కాన్ఫిగ్ స్నిప్పెట్‌లు). మీ ఇప్పటికే ఉన్న టూల్ కాన్ఫిగ్‌లు ఎప్పుడూ మార్చబడవు.

---

## 🤖 టెర్మినల్ / CLI ఏజెంట్లు

### Claude Code (Anthropic-compatible)

Claude Code మరియు Claude Agent SDK టూల్స్ Anthropic-compatible `/v1/messages` ఎండ్‌పాయింట్ ద్వారా కనెక్ట్ అవుతాయి.

```bash
# ANTHROPIC_BASE_URL is the ROOT (no /v1) — the CLI appends /v1/messages itself.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# The official CLI prefers ANTHROPIC_API_KEY; set both to be safe.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ `ANTHROPIC_BASE_URL`లో `/v1`ని **పెట్టవద్దు** — అది `/v1/v1/messages` అయ్యి ఫెయిల్ అవుతుంది. OpenAI-compatible మోడల్స్‌కి రూట్ చేసినప్పుడు కూడా టూల్ కాల్స్ మరియు స్ట్రీమింగ్ ఎండ్-టు-ఎండ్ పనిచేస్తాయి.

### Codex CLI (Responses API)

Codex OpenAI Responses API (`/v1/responses`) ద్వారా కనెక్ట్ అవుతుంది; Chat Completions పాత్ ఫిబ్రవరి 2026లో Codex నుండి తీసివేయబడింది.

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

అప్‌స్ట్రీమ్ Gemini CLIకి బాహ్య OpenAI-compatible ఎండ్‌పాయింట్ల కోసం బలహీనమైన సపోర్ట్ ఉంది; మీకు OpenAI-compatible wrapper లేదా fork అవసరం కావచ్చు.

---

## 🖥 IDE / GUI ఏజెంట్లు

### Cline · Roo Code · Kilo Code · Cursor

ప్రొవైడర్‌గా **OpenAI Compatible** (లేదా **Custom OpenAI**) ఎంచుకుని దీన్ని పేస్ట్ చేయండి:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ ఎల్లప్పుడూ **OpenAI Compatible స్లాట్‌ని** ఉపయోగించండి — డెడికేటెడ్ OpenRouter ఎంట్రీ openrouter.aiకి హార్డ్‌కోడ్ చేయబడింది మరియు ఫెయిల్ అవుతుంది. **Cursor**కి బేస్ URLలో `/v1` మరియు నాన్-ఎంప్టీ కీ ఫీల్డ్ అవసరం. **Kilo Code**కి ఒక తెలిసిన సమస్య (#681) ఉంది, ఇందులో కస్టమ్ బేస్ URL మోడల్ లిస్టింగ్‌కి పంపబడదు — మోడల్ IDని మాన్యువల్‌గా ఎంటర్ చేయండి.

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

`model: AUTODETECT`తో Continue మోడల్ లిస్ట్‌ని ఆటోమేటిక్‌గా పుల్ చేస్తుంది.

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

ఫీల్డ్ పేర్లు Zed వెర్షన్‌ని బట్టి మారవచ్చు — Zed డాక్స్‌ని చెక్ చేయండి.

---

## 📦 SDKలు

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

## 🎨 మల్టీమోడల్ — ఇమేజ్ · ఆడియో · వీడియో

అన్ని మోడాలిటీలు ఒకే కీపై OpenAI-compatible HTTP ఎండ్‌పాయింట్లు. [`GET /v1/models`](https://pleum.ai/models) నుండి మోడాలిటీని సపోర్ట్ చేసే మోడల్‌ని ఎంచుకోండి.

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

### API సర్ఫేస్

| ఎండ్‌పాయింట్ | ప్రోటోకాల్ |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (streaming, tools, vision) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | ఇమేజ్ జనరేషన్ |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | ఏసింక్ వీడియో |
| `GET /v1/models` | మోడల్ కేటలాగ్ (పబ్లిక్) |
| `GET /v1/credits` | బ్యాలెన్స్ |

---

## 🔌 మరిన్ని ఏజెంట్లు

ఇక్కడ లిస్ట్ చేయని చాలా ఏజెంట్లు అదే విధంగా పనిచేస్తాయి — OpenAI-compatible బేస్ URLని సెట్ చేయండి:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** మరియు మరెన్నో.

Anthropic-compatible `/v1/messages` ద్వారా: **claude-code-router** కూడా `ANTHROPIC_BASE_URL`తో కనెక్ట్ అవుతుంది.

**మోడల్ IDలు**: వాటిని `GET /v1/models` వద్ద లేదా [మోడల్స్ పేజీ](https://pleum.ai/models)లో కనుగొనండి. Cline, Continue, OpenCode మరియు ఇతరులు లిస్ట్‌ని ఆటోమేటిక్‌గా ఫెచ్ చేస్తారు. OpenRouter-ఫార్మాట్ IDలు (`openai/gpt-5.5`) ఆటోమేటిక్‌గా కన్వర్ట్ చేయబడతాయి.

**LiteLLM proxy** (Aider, OpenHands, Open Interpreter, SWE-agent మరియు gptme LiteLLM-ఆధారితమైనవి మరియు నేరుగా కనెక్ట్ అవుతాయి — కానీ మీరు LiteLLM proxyని ఉంచుకుంటే):

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

## కంట్రిబ్యూటింగ్

ఇక్కడ లిస్ట్ చేయని ఏదైనా టూల్‌తో PleumRouter పని చేయించారా? PRలకు స్వాగతం — **టెస్ట్ చేసిన** కాన్ఫిగ్ స్నిప్పెట్‌తో (బేస్ URL, కీ env, మోడల్ ID ఫార్మాట్, మరియు ఏవైనా గోచాలు) ఒక సెక్షన్‌ని జోడించండి.

## లైసెన్స్

[MIT](LICENSE)
