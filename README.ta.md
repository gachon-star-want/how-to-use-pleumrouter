<div align="center">

# PleumRouter ஐ எப்படி பயன்படுத்துவது

**200+ AI மாடல்களுக்கு ஒரே API கீ — OpenAI-இணக்கமான, KRW-இல் பில் செய்யப்படும்.**

[வலைத்தளம்](https://pleum.ai) · [ஆவணங்கள்](https://pleum.ai/docs) · [மாடல்கள்](https://pleum.ai/models) · [பிளேகிரவுண்ட்](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · தமிழ் · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter என்பது ஒரு AI கேட்வே: ஒரே கீ (`plm_…`), ஒரே பேஸ் URL, 18 வழங்குநர்களிடமிருந்து 210+ மாடல்கள் — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE மற்றும் மேலும் பல. இது **OpenAI Chat Completions**, **Anthropic Messages**, மற்றும் **OpenAI Responses** ஆகியவற்றைப் பேசுகிறது, எனவே கிட்டத்தட்ட ஒவ்வொரு கோடிங் ஏஜென்ட், IDE பிளக்கின், மற்றும் SDK-யும் ஒரே வரி கான்பிக் மாற்றத்துடன் இணைகின்றன. டெக்ஸ்ட், embeddings, பட, ஒலி மற்றும் வீடியோ அனைத்தும் ஒரே கீ மூலம் இயங்குகின்றன.

இந்த ரெப்போ **சரிபார்க்கப்பட்ட ஒருங்கிணைப்பு ரெசிபிகளை** தொகுக்கிறது. கீழே உள்ள ஒவ்வொரு ஸ்னிப்பெட்டும் லைவ் கேட்வேக்கு எதிராக சோதிக்கப்பட்டது.

## தொடங்குதல்

1. [பதிவு செய்யவும்](https://pleum.ai/signup) → டாஷ்போர்டு → **API Keys** → ஒரு கீயை வழங்கவும் (`plm_` இல் தொடங்கும்).
2. உங்கள் கருவியை பேஸ் URL-க்கு இயக்கவும்:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# சில ஏஜென்ட்கள் (OpenCode, Crush) PLEUM_API_KEY ஐ படிக்கின்றன — அதே கீ, இரண்டையும் அமைக்கவும்.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. ஸ்மோக் டெஸ்ட்:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

பதிவு செய்யும்போது ₩1,000 இலவச கிரெடிட் மற்றும் உங்கள் முதல் டாப்-அப்பில் ₩5,000 போனஸ் கிடைக்கும்.

## ஒருங்கிணைப்புகள்

| வகை | கருவிகள் |
|---|---|
| [⚡ ஒரு-கட்டளை லாஞ்சர்](#-pleum-cli--வேகமான-பாதை) | `pleum` CLI |
| [🤖 டெர்மினல் கோடிங் ஏஜென்ட்கள்](#-டெர்மினல--cli-ஏஜென்ட்கள்) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE / GUI ஏஜென்ட்கள்](#-ide--gui-ஏஜென்ட்கள்) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDKs](#-sdks) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 மல்டிமோடல் API](#-மல்டிமோடல--பட--ஆடியோ--வீடியோ) | படங்கள், TTS, STT, வீடியோ, Embeddings |
| [🔌 மற்ற அனைத்தும்](#-மேலும்-ஏஜென்ட்கள்) | OpenRouter-பாணி ID-கள், LiteLLM ப்ராக்ஸி, 15+ கூடுதல் ஏஜென்ட்கள் |

---

## ⚡ pleum CLI — வேகமான பாதை

அதிகாரப்பூர்வ CLI உங்கள் விருப்பமான ஏஜென்டை ஏற்கனவே PleumRouter உடன் இணைக்கப்பட்டதாக லாஞ்ச் செய்கிறது. கான்பிக் ஃபைல்கள் எதுவும் தொடப்படாது.

```bash
npm install -g pleumrouter        # அல்லது: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # பிரவுசர் லாகின், கீ தானாகவே வழங்கப்பட்டு சேமிக்கப்படும்
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # டெர்மினல் சாட் REPL
pleum models                      # விலை நிர்ணயத்துடன் அனைத்து மாடல்களையும் பட்டியலிடும்
```

தானியங்கி-லாஞ்சிற்கு ஆதரவு: `claude` · `aider` · `codex` · `goose` · `openhands` (மேலும் `opencode` · `crush` க்கான கான்பிக் ஸ்னிப்பெட்கள்). உங்கள் ஏற்கனவே உள்ள கருவி கான்பிகுகள் ஒருபோதும் மாற்றப்படாது.

---

## 🤖 டெர்மினல் / CLI ஏஜென்ட்கள்

### Claude Code (Anthropic-இணக்கமான)

Claude Code மற்றும் Claude Agent SDK கருவிகள் Anthropic-இணக்கமான `/v1/messages` எண்ட்பாயிண்ட் வழியாக இணைகின்றன.

```bash
# ANTHROPIC_BASE_URL என்பது ROOT (/v1 இல்லாமல்) — CLI தானாகவே /v1/messages ஐ இணைக்கிறது.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# அதிகாரப்பூர்வ CLI ANTHROPIC_API_KEY ஐ விரும்புகிறது; பாதுகாப்பாக இருக்க இரண்டையும் அமைக்கவும்.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ `ANTHROPIC_BASE_URL` இல் `/v1` ஐ **சேர்க்க வேண்டாம்** — அது `/v1/v1/messages` ஆக மாறி தோல்வியடையும். OpenAI-இணக்கமான மாடல்களுக்கு ரூட் செய்யப்படும்போது கூட, டூல் அழைப்புகள் மற்றும் ஸ்ட்ரீமிங் இறுதி வரை வேலை செய்கின்றன.

### Codex CLI (Responses API)

Codex OpenAI Responses API (`/v1/responses`) வழியாக இணைகிறது; Chat Completions பாதை பிப்ரவரி 2026 இல் Codex இலிருந்து அகற்றப்பட்டது.

```toml
# ~/.codex/config.toml
# model / model_provider ஆவண-ரூட் கீகள் (அவை [table] க்கு மேலே இருக்க வேண்டும்).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex /responses ஐ இணைக்கிறது → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex Responses API ஐ மட்டுமே ஆதரிக்கிறது
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
// opencode.json   (அல்லது: /connect → Other)
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

# Goose / OpenHands: மாடல் ஐடிக்கு openai/ முன்னொட்டைச் சேர்க்கவும்
#   model = openai/gpt-4.1
```

### Gemini CLI

அப்ஸ்ட்ரீம் Gemini CLI-க்கு வெளிப்புற OpenAI-இணக்கமான எண்ட்பாயிண்ட்களுக்கான ஆதரவு பலவீனமாக உள்ளது; உங்களுக்கு OpenAI-இணக்கமான ரேப்பர் அல்லது ஃபோர்க் தேவைப்படலாம்.

---

## 🖥 IDE / GUI ஏஜென்ட்கள்

### Cline · Roo Code · Kilo Code · Cursor

**OpenAI Compatible** (அல்லது **Custom OpenAI**) ஐ வழங்குநராகத் தேர்ந்தெடுத்து பேஸ்ட் செய்யவும்:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ எப்போதும் **OpenAI Compatible ஸ்லாட்டை** பயன்படுத்தவும் — பிரத்யேக OpenRouter எண்ட்ரி openrouter.ai க்கு ஹார்ட்கோட் செய்யப்பட்டுள்ளது மற்றும் தோல்வியடையும். **Cursor** க்கு பேஸ் URL-இல் `/v1` தேவை மற்றும் காலியில்லாத கீ ஃபீல்ட் தேவை. **Kilo Code** இல் ஒரு அறியப்பட்ட சிக்கல் (#681) உள்ளது, அங்கு custom பேஸ் URL மாடல் லிஸ்டிங்கிற்கு அனுப்பப்படுவதில்லை — மாடல் ஐடியை கைமுறையாக உள்ளிடவும்.

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

`model: AUTODETECT` உடன் Continue மாடல் பட்டியலை தானாகவே இழுக்கிறது.

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

Zed பதிப்பைப் பொறுத்து ஃபீல்ட் பெயர்கள் மாறுபடலாம் — Zed ஆவணங்களைச் சரிபார்க்கவும்.

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
    base_url="https://router.pleum.ai",   # ரூட், /v1 இல்லாமல் — SDK /v1/messages ஐ இணைக்கிறது
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # எந்த PleumRouter மாடலும் வேலை செய்யும்
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 மல்டிமோடல் — பட · ஆடியோ · வீடியோ

அனைத்து மோடாலிட்டிகளும் அதே கீயில் OpenAI-இணக்கமான HTTP எண்ட்பாயிண்ட்கள். [`GET /v1/models`](https://pleum.ai/models) இலிருந்து மோடாலிட்டியை ஆதரிக்கும் ஒரு மாடலைத் தேர்ந்தெடுக்கவும்.

```bash
# பட உருவாக்கம்
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# டெக்ஸ்ட்-டு-ஸ்பீச் (ஆடியோ பைட்களை திருப்பி அளிக்கும்; X-Cost-Krw ஹெடரில் செலவு)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# ஸ்பீச்-டு-டெக்ஸ்ட் (மல்டிபார்ட் அப்லோட்)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# வீடியோ உருவாக்கம் அசின்க் ஆகும்: POST ஒரு job_id ஐ திருப்பி அளிக்கும், பின்னர் GET /v1/jobs/{job_id} ஐ போல் செய்யவும்
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### API சர்ஃபேஸ்

| எண்ட்பாயிண்ட் | ப்ரோட்டோகால் |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (ஸ்ட்ரீமிங், டூல்ஸ், விஷன்) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | பட உருவாக்கம் |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | அசின்க் வீடியோ |
| `GET /v1/models` | மாடல் கேட்டலாக் (பொது) |
| `GET /v1/credits` | இருப்பு |

---

## 🔌 மேலும் ஏஜென்ட்கள்

இங்கே பட்டியலிடப்படாத பெரும்பாலான ஏஜென்ட்கள் அதே வழியில் வேலை செய்கின்றன — OpenAI-இணக்கமான பேஸ் URL ஐ அமைக்கவும்:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** மற்றும் மேலும் பல.

Anthropic-இணக்கமான `/v1/messages` வழியாக: **claude-code-router** ஆனது `ANTHROPIC_BASE_URL` உடன் இணைகிறது.

**மாடல் ஐடிகள்**: அவற்றை `GET /v1/models` இல் அல்லது [மாடல்கள் பக்கத்தில்](https://pleum.ai/models) கண்டறியவும். Cline, Continue, OpenCode மற்றும் பிற பட்டியலை தானாகவே பெறுகின்றன. OpenRouter-வடிவ ஐடிகள் (`openai/gpt-5.5`) தானாகவே மாற்றப்படுகின்றன.

**LiteLLM ப்ராக்ஸி** (Aider, OpenHands, Open Interpreter, SWE-agent மற்றும் gptme LiteLLM-அடிப்படையிலானவை, நேரடியாக இணைகின்றன — ஆனால் நீங்கள் LiteLLM ப்ராக்ஸியை வைத்திருந்தால்):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # openai/ முன்னொட்டு → OpenAI-இணக்க வழி
      api_base: https://router.pleum.ai/v1           # /chat/completions ஐ இணைக்க வேண்டாம்
      api_key: os.environ/PLEUM_API_KEY
```

---

## பங்களிப்பு

இங்கே பட்டியலிடப்படாத ஒரு கருவியுடன் PleumRouter ஐ வேலை செய்ய வைத்தீர்களா? PR-கள் வரவேற்கப்படுகின்றன — ஒரு **சோதிக்கப்பட்ட** கான்பிக் ஸ்னிப்பெட்டுடன் (பேஸ் URL, கீ env, மாடல் ஐடி வடிவம், மற்றும் ஏதேனும் சிக்கல்கள்) ஒரு பிரிவைச் சேர்க்கவும்.

## உரிமம்

[MIT](LICENSE)
