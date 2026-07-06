<div align="center">

# Ինչպես օգտագործել PleumRouter-ը

**Մեկ API բանալի 200+ AI մոդելների համար — OpenAI-ի հետ համատեղելի, հաշվարկվում է KRW-ով.**

[Կայք](https://pleum.ai) · [Փաստաթղթեր](https://pleum.ai/docs) · [Մոդելներ](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · Հայերեն · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter-ը AI դարպաս է. մեկ բանալի (`plm_…`), մեկ base URL, 210+ մոդել 18 մատակարարից — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE և ուրիշներ։ Այն աշխատում է **OpenAI Chat Completions**, **Anthropic Messages** և **OpenAI Responses** ինտերֆեյսներով, ուստի գրեթե ցանկացած կոդագրող գործակալ, IDE հավելուն և SDK միանում է կոնֆիգուրացիայի մեկ տողի փոփոխությամբ։ Տեքստը, ներդրումները (embeddings), պատկերները, խոսքն ու տեսանյութը՝ բոլորը աշխատում են նույն բանալիով։

Այս պահոցը հավաքում է **ստուգված ինտեգրման բաղադրատոմսեր**։ Ստորև բերված յուրաքանչյուր հատված փորձարկված է կենդանի դարպասի վրա։

## Սկսելը

1. [Գրանցվեք](https://pleum.ai/signup) → Dashboard → **API Keys** → թողարկեք բանալի (սկսվում է `plm_`-ով)։
2. Ուղղորդեք ձեր գործիքը դեպի base URL-ը.

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Որոշ գործակալներ (OpenCode, Crush) կարդում են PLEUM_API_KEY — նույն բանալին, սահմանեք երկուսն էլ:
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Փորձարկեք.

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Դուք ստանում եք ₩1,000 անվճար կրեդիտ գրանցվելիս և ₩5,000 բոնուս ձեր առաջին համալրման ժամանակ։

## Ինտեգրումներ

| Կատեգորիա | Գործիքներ |
|---|---|
| [⚡ Մեկ հրամանով գործարկիչ](#-pleum-cli--արագ-ուղին) | `pleum` CLI |
| [🤖 Տերմինալի կոդագրող գործակալներ](#-տերմինալ--cli-գործակալներ) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE / GUI գործակալներ](#-ide--gui-գործակալներ) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK-ներ](#-sdk-ներ) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 Մուլտիմոդալ API](#-մուլտիմոդալ--պատկեր--աուդիո--տեսանյութ) | Պատկերներ, TTS, STT, Video, Embeddings |
| [🔌 Ամեն ինչ մյուսը](#-այլ-գործակալներ) | OpenRouter-ոճի ID-ներ, LiteLLM proxy, 15+ այլ գործակալ |

---

## ⚡ pleum CLI — արագ ուղին

Պաշտոնական CLI-ն գործարկում է ձեր սիրելի գործակալը, որն արդեն միացված է PleumRouter-ին։ Կոնֆիգուրացիայի ֆայլերին ոչինչ չի դիպչում։

```bash
npm install -g pleumrouter        # կամ: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # մուտք բրաուզերով, բանալին ինքնաշխատ թողարկվում և պահվում է
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # տերմինալի զրույցի REPL
pleum models                      # ցուցադրել բոլոր մոդելները գնագոյացմամբ
```

Ինքնագործարկումն աջակցվում է հետևյալների համար՝ `claude` · `aider` · `codex` · `goose` · `openhands` (ինչպես նաև կոնֆիգուրացիայի հատվածներ `opencode` · `crush`-ի համար)։ Ձեր առկա գործիքների կոնֆիգուրացիաները երբեք չեն փոփոխվում։

---

## 🤖 Տերմինալ / CLI գործակալներ

### Claude Code (Anthropic-ի հետ համատեղելի)

Claude Code-ը և Claude Agent SDK գործիքները միանում են Anthropic-ի հետ համատեղելի `/v1/messages` վերջնակետի միջոցով։

```bash
# ANTHROPIC_BASE_URL-ը ROOT-ն է (առանց /v1) — CLI-ն ինքն է հավելում /v1/messages:
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# Պաշտոնական CLI-ն նախընտրում է ANTHROPIC_API_KEY; անվտանգության համար սահմանեք երկուսն էլ:
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ **Մի** դրեք `/v1`-ը `ANTHROPIC_BASE_URL`-ում — այն դառնում է `/v1/v1/messages` և ձախողվում է։ Գործիքների կանչերն ու streaming-ը աշխատում են ամբողջությամբ, նույնիսկ երբ ուղղորդված են OpenAI-ի հետ համատեղելի մոդելների։

### Codex CLI (Responses API)

Codex-ը միանում է OpenAI Responses API-ի (`/v1/responses`) միջոցով; Chat Completions ուղին հեռացվել է Codex-ից 2026 թվականի փետրվարին։

```toml
# ~/.codex/config.toml
# model / model_provider-ը փաստաթղթի արմատի բանալիներ են (պետք է լինեն [table]-ից վերև):
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex-ը հավելում է /responses → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex-ն աջակցում է միայն Responses API-ին
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
// opencode.json   (կամ: /connect → Other)
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

# Goose / OpenHands: մոդելի id-ին ավելացրեք openai/ նախածանցը
#   model = openai/gpt-4.1
```

### Gemini CLI

Gemini CLI-ի սկզբնաղբյուր տարբերակը ունի արտաքին OpenAI-ի հետ համատեղելի վերջնակետերի թույլ աջակցում; գուցե անհրաժեշտ լինի OpenAI-ի հետ համատեղելի փաթաթան (wrapper) կամ ֆորկ։

---

## 🖥 IDE / GUI գործակալներ

### Cline · Roo Code · Kilo Code · Cursor

Ընտրեք **OpenAI Compatible** (կամ **Custom OpenAI**) որպես մատակարար և տեղադրեք.

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Միշտ օգտագործեք **OpenAI Compatible դաշտը** — հատուկ OpenRouter մուտքագրման դաշտը կոշտ կապված է openrouter.ai-ին և կձախողվի։ **Cursor**-ը պահանջում է `/v1`-ը base URL-ում և ոչ դատարկ բանալու դաշտ։ **Kilo Code**-ն ունի հայտնի խնդիր (#681), որտեղ ցանկացած base URL-ը չի փոխանցվում մոդելների ցանկագրմանը — մուտքագրեք մոդելի ID-ն ձեռքով։

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

`model: AUTODETECT`-ով Continue-ն ինքնաշխատ քաշում է մոդելների ցանկը։

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

Դաշտերի անունները կարող են տարբերվել Zed-ի տարբերակից ելնելով — ստուգեք Zed-ի փաստաթղթերը։

---

## 📦 SDK-ներ

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
    base_url="https://router.pleum.ai",   # արմատ, առանց /v1 — SDK-ն հավելում է /v1/messages
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # ցանկացած PleumRouter մոդել աշխատում է
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Մուլտիմոդալ — պատկեր · աուդիո · տեսանյութ

Բոլոր մոդալությունները OpenAI-ի հետ համատեղելի HTTP վերջնակետեր են՝ նույն բանալիով։ Ընտրեք մոդալությանն աջակցող մոդել [`GET /v1/models`](https://pleum.ai/models)-ից։

```bash
# Պատկերի ստեղծում
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Տեքստից խոսք (վերադարձնում է աուդիո բայթեր; ինքնարժեքը X-Cost-Krw վերնագրում)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Խոսքից տեքստ (multipart վերբեռնում)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# Տեսանյութի ստեղծումն ասինխրոն է. POST-ը վերադարձնում է job_id, ապա հարցումով ստուգեք GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### API մակերես

| Վերջնակետ | Արձանագրություն |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (streaming, գործիքներ, տեսողություն) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Պատկերի ստեղծում |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Ասինխրոն տեսանյութ |
| `GET /v1/models` | Մոդելների կատալոգ (հրապարակային) |
| `GET /v1/credits` | Մնացորդ |

---

## 🔌 Այլ գործակալներ

Այստեղ չնշված գործակալների մեծ մասն աշխատում է նույն կերպ — սահմանեք OpenAI-ի հետ համատեղելի base URL-ը.

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** և ուրիշներ։

Anthropic-ի հետ համատեղելի `/v1/messages`-ի միջոցով. **claude-code-router**-ը նույնպես միանում է `ANTHROPIC_BASE_URL`-ով։

**Մոդելի ID-ներ**. գտեք դրանք `GET /v1/models`-ում կամ [մոդելների էջում](https://pleum.ai/models)։ Cline-ը, Continue-ն, OpenCode-ն և ուրիշներն ինքնաշխատ քաշում են ցանկը։ OpenRouter-ձևաչափի ID-ները (`openai/gpt-5.5`) ինքնաշխատ փոխակերպվում են։

**LiteLLM proxy** (Aider, OpenHands, Open Interpreter, SWE-agent և gptme-ը հիմնված են LiteLLM-ի վրա և միանում են ուղղակիորեն — բայց եթե դուք պահպանում եք LiteLLM proxy).

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # openai/ նախածանց → OpenAI-compat ուղի
      api_base: https://router.pleum.ai/v1           # ՄԻ հավելեք /chat/completions
      api_key: os.environ/PLEUM_API_KEY
```

---

## Ներդրում

PleumRouter-ը այստեղ չնշված գործիքի հետ աշխատեցրե՞լ եք։ PR-ները ողջունելի են — ավելացրեք հատված **փորձարկված** կոնֆիգուրացիայի հատվածով (base URL, բանալու env, մոդելի ID-ի ձևաչափ և ցանկացած նրբություն)։

## Լիցենզիա

[MIT](LICENSE)
