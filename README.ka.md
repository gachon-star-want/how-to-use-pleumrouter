<div align="center">

# როგორ გამოვიყენოთ PleumRouter

**ერთი API გასაღები 200+ AI მოდელისთვის — OpenAI-თან თავსებადი, ფასდება KRW-ში.**

[ვებსაიტი](https://pleum.ai) · [დოკუმენტაცია](https://pleum.ai/docs) · [მოდელები](https://pleum.ai/models) · [სავარჯიშო სივრცე](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · ქართული · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter არის AI გეითვეი: ერთი გასაღები (`plm_…`), ერთი საბაზისო URL, 210+ მოდელი 18 პროვაიდერისგან — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE და სხვა. ის მხარს უჭერს **OpenAI Chat Completions**, **Anthropic Messages** და **OpenAI Responses** პროტოკოლებს, ასე რომ თითქმის ყველა კოდირების აგენტი, IDE დანამატი და SDK უერთდება ერთი ხაზის კონფიგურაციის ცვლილებით. ტექსტი, ჩაშენებები (embeddings), სურათი, ხმა და ვიდეო — ყველაფერი მუშაობს ერთი და იმავე გასაღებით.

ეს რეპოზიტორია აგროვებს **გადამოწმებულ ინტეგრაციის რეცეპტებს**. ქვემოთ მოცემული ყველა კოდის ნაწყვეტი ტესტირებულია რეალურ გეითვეიზე.

## დაწყება

1. [დარეგისტრირდით](https://pleum.ai/signup) → პანელი (Dashboard) → **API Keys** → გამოსცით გასაღები (იწყება `plm_`-ით).
2. მიმართეთ თქვენი ინსტრუმენტი საბაზისო URL-ისკენ:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# ზოგიერთი აგენტი (OpenCode, Crush) კითხულობს PLEUM_API_KEY-ს — იგივე გასაღები, დააყენეთ ორივე.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. სწრაფი ტესტი:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

რეგისტრაციისას იღებთ ₩1,000 უფასო კრედიტს, ხოლო პირველი დამატებისას — ₩5,000 ბონუსს.

## ინტეგრაციები

| კატეგორია | ინსტრუმენტები |
|---|---|
| [⚡ ერთბრძანებიანი გამშვები](#-pleum-cli--სწრაფი-გზა) | `pleum` CLI |
| [🤖 ტერმინალის კოდირების აგენტები](#-ტერმინალი--cli-აგენტები) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE / GUI აგენტები](#-ide--gui-აგენტები) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK-ები](#-sdk-ები) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 მულტიმოდალური API](#-მულტიმოდალური--სურათი--აუდიო--ვიდეო) | სურათები, TTS, STT, ვიდეო, ჩაშენებები |
| [🔌 ყველაფერი დანარჩენი](#-სხვა-აგენტები) | OpenRouter-სტილის ID-ები, LiteLLM პროქსი, 15+ სხვა აგენტი |

---

## ⚡ pleum CLI — სწრაფი გზა

ოფიციალური CLI უშვებს თქვენს საყვარელ აგენტს, რომელიც უკვე დაკავშირებულია PleumRouter-თან. კონფიგურაციის ფაილებს არაფერი ეხება.

```bash
npm install -g pleumrouter        # ან: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # ბრაუზერით შესვლა, გასაღები ავტომატურად გამოიცემა და ინახება
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # ტერმინალის ჩატის REPL
pleum models                      # ყველა მოდელის სია ფასებთან ერთად
```

ავტომატური გაშვება მხარდაჭერილია: `claude` · `aider` · `codex` · `goose` · `openhands` (პლუს კონფიგურაციის ნაწყვეტები `opencode`-სთვის · `crush`-ისთვის). თქვენს არსებულ ინსტრუმენტების კონფიგურაციებს არასდროს ეხებიან.

---

## 🤖 ტერმინალი / CLI აგენტები

### Claude Code (Anthropic-თან თავსებადი)

Claude Code და Claude Agent SDK ინსტრუმენტები უერთდებიან Anthropic-თან თავსებადი `/v1/messages` ბოლოწერტილის მეშვეობით.

```bash
# ANTHROPIC_BASE_URL არის ძირეული (root) — /v1-ის გარეშე — CLI თავად ამატებს /v1/messages-ს.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# ოფიციალურ CLI-ს ურჩევნია ANTHROPIC_API_KEY; დააყენეთ ორივე უსაფრთხოებისთვის.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ **არ** ჩასვათ `/v1` `ANTHROPIC_BASE_URL`-ში — ის იქცევა `/v1/v1/messages`-ად და ჩავარდება. ხელსაწყოების გამოძახებები (tool calls) და სტრიმინგი მუშაობს ბოლომდე, თუნდაც OpenAI-თან თავსებადი მოდელებისკენ იყოს მარშრუტიზებული.

### Codex CLI (Responses API)

Codex უერთდება OpenAI Responses API-ს (`/v1/responses`) მეშვეობით; Chat Completions გზა ამოღებულ იქნა Codex-იდან 2026 წლის თებერვალში.

```toml
# ~/.codex/config.toml
# model / model_provider არის დოკუმენტის ძირის (document-root) გასაღებები (უნდა იყოს [table]-ის ზემოთ).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex ამატებს /responses → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex მხარს უჭერს მხოლოდ Responses API-ს
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
// opencode.json   (ან: /connect → Other)
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

# Goose / OpenHands: მოდელის id-ს დაურთეთ პრეფიქსი openai/
#   model = openai/gpt-4.1
```

### Gemini CLI

Gemini CLI-ის საწყისს (upstream) აქვს სუსტი მხარდაჭერა გარე OpenAI-თან თავსებადი ბოლოწერტილებისთვის; შესაძლოა დაგჭირდეთ OpenAI-თან თავსებადი გამომფარგვლი (wrapper) ან ფორკი.

---

## 🖥 IDE / GUI აგენტები

### Cline · Roo Code · Kilo Code · Cursor

აირჩიეთ **OpenAI Compatible** (ან **Custom OpenAI**) პროვაიდერად და ჩასვით:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ ყოველთვის გამოიყენეთ **OpenAI Compatible სლოტი** — გამორჩეული OpenRouter ველი მყარადაა მიბმული openrouter.ai-ზე და ჩავარდება. **Cursor**-ს სჭირდება `/v1` საბაზისო URL-ში და არაცარიელი გასაღების ველი. **Kilo Code**-ს აქვს ცნობილი პრობლემა (#681), როცა მორგებული საბაზისო URL არ გადაეცემა მოდელების ჩამონათვალს — შეიყვანეთ მოდელის ID ხელით.

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

`model: AUTODETECT`-ის მეშვეობით Continue ავტომატურად იღებს მოდელების ჩამონათვალს.

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

ველების სახელები შეიძლება განსხვავდებოდეს Zed-ის ვერსიის მიხედვით — გადაამოწმეთ Zed-ის დოკუმენტაცია.

---

## 📦 SDK-ები

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
    base_url="https://router.pleum.ai",   # ძირი, /v1-ის გარეშე — SDK ამატებს /v1/messages-ს
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # ნებისმიერი PleumRouter მოდელი მუშაობს
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 მულტიმოდალური — სურათი · აუდიო · ვიდეო

ყველა მოდალობა OpenAI-თან თავსებადი HTTP ბოლოწერტილია ერთსა და იმავე გასაღებზე. აირჩიეთ მოდელი, რომელიც მხარს უჭერს ამ მოდალობას [`GET /v1/models`](https://pleum.ai/models)-იდან.

```bash
# სურათის გენერაცია
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# ტექსტიდან მეტყველებაზე (აბრუნებს აუდიო ბაიტებს; ღირებულება X-Cost-Krw თავსართში)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# მეტყველებიდან ტექსტზე (მრავალნაწილიანი ატვირთვა)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# ვიდეო გენერაცია ასინქრონულია: POST აბრუნებს job_id-ს, შემდეგ დაათვალიერეთ GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### API ზედაპირი

| ბოლოწერტილი | პროტოკოლი |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (სტრიმინგი, ხელსაწყოები, ხედვა) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | სურათის გენერაცია |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | ასინქრონული ვიდეო |
| `GET /v1/models` | მოდელების კატალოგი (საჯარო) |
| `GET /v1/credits` | ბალანსი |

---

## 🔌 სხვა აგენტები

აქ ჩამოუთვლელი აგენტების უმეტესობა მუშაობს იმავე გზით — დააყენეთ OpenAI-თან თავსებადი საბაზისო URL:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** და სხვები.

Anthropic-თან თავსებადი `/v1/messages`-ის მეშვეობით: **claude-code-router**-იც უერთდება `ANTHROPIC_BASE_URL`-ით.

**მოდელის ID-ები**: მოიძიეთ `GET /v1/models`-ზე ან [მოდელების გვერდზე](https://pleum.ai/models). Cline, Continue, OpenCode და სხვები ავტომატურად იღებენ ჩამონათვალს. OpenRouter-ფორმატის ID-ები (`openai/gpt-5.5`) ავტომატურად გარდაიქმნება.

**LiteLLM პროქსი** (Aider, OpenHands, Open Interpreter, SWE-agent და gptme LiteLLM-ზეა დაფუძნებული და პირდაპირ უერთდება — მაგრამ თუ ინახავთ LiteLLM პროქსის):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # openai/ პრეფიქსი → OpenAI-თან თავსებადი მარშრუტი
      api_base: https://router.pleum.ai/v1           # ნუ დაურთავთ /chat/completions-ს
      api_key: os.environ/PLEUM_API_KEY
```

---

## წვლილის შეტანა

ჩართეთ PleumRouter აქ ჩამოუთვლელ ინსტრუმენტთან? PR-ები კეთილმოსულია — დაამატეთ განყოფილება **ტესტირებული** კონფიგურაციის ნაწყვეტით (საბაზისო URL, გასაღების გარემოს ცვლადი, მოდელის ID-ის ფორმატი და ნებისმიერი ხაფანგი).

## ლიცენზია

[MIT](LICENSE)
