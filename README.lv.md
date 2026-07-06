<div align="center">

# Kā izmantot PleumRouter

**Viena API atslēga 200+ AI modeļiem — savietojama ar OpenAI, norēķini KRW.**

[Tīmekļa vietne](https://pleum.ai) · [Dokumentācija](https://pleum.ai/docs) · [Modeļi](https://pleum.ai/models) · [Spēļu laukums](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · Latviešu · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter ir AI vārteja: viena atslēga (`plm_…`), viens bāzes URL, 210+ modeļi no 18 nodrošinātājiem — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE un citi. Tā atbalsta **OpenAI Chat Completions**, **Anthropic Messages** un **OpenAI Responses**, tāpēc gandrīz katrs koda aģents, IDE spraudnis un SDK pieslēdzas ar vienas rindas konfigurācijas izmaiņu. Teksts, iegulumi (embeddings), attēli, runa un video — viss darbojas ar to pašu atslēgu.

Šis repozitorijs apkopo **pārbaudītas integrācijas receptes**. Katrs zemāk redzamais koda fragments ir testēts pret aktīvo (live) vārteju.

## Darba sākšana

1. [Reģistrējieties](https://pleum.ai/signup) → Vadības panelis → **API atslēgas** → izsniedziet atslēgu (sākas ar `plm_`).
2. Norādiet savam rīkam bāzes URL:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Daži aģenti (OpenCode, Crush) lasa PLEUM_API_KEY — tā pati atslēga, iestatiet abus.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Pārbaudes tests:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Reģistrējoties jūs saņemat ₩1,000 bezmaksas kredītu un ₩5,000 bonusu par pirmo uzlādi.

## Integrācijas

| Kategorija | Rīki |
|---|---|
| [⚡ Vienas komandas palaidējs](#-pleum-cli--ātrais-ceļš) | `pleum` CLI |
| [🤖 Termināļa koda aģenti](#-termināļa--cli-aģenti) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE / GUI aģenti](#-ide--gui-aģenti) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK](#-sdk) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 Multimodālais API](#-multimodālais--attēli--audio--video) | Attēli, TTS, STT, video, iegulumi (embeddings) |
| [🔌 Viss pārējais](#-vairāk-aģentu) | OpenRouter stila ID, LiteLLM starpniekserveris, 15+ citu aģentu |

---

## ⚡ pleum CLI — ātrais ceļš

Oficiālais CLI palaiž jūsu iecienītāko aģentu, kas jau ir pieslēgts PleumRouter. Nekādi konfigurācijas faili netiek skarti.

```bash
npm install -g pleumrouter        # vai: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # pieteikšanās pārlūkā, atslēga tiek automātiski izsniegta un saglabāta
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # termināļa tērzēšanas REPL
pleum models                      # visu modeļu saraksts ar cenām
```

Automātiskā palaišana atbalstīta priekš: `claude` · `aider` · `codex` · `goose` · `openhands` (turklāt konfigurācijas fragmenti priekš `opencode` · `crush`). Jūsu esošās rīku konfigurācijas nekad netiek mainītas.

---

## 🤖 Termināļa / CLI aģenti

### Claude Code (savietojams ar Anthropic)

Claude Code un Claude Agent SDK rīki pieslēdzas, izmantojot ar Anthropic savietojamo `/v1/messages` galapunktu.

```bash
# ANTHROPIC_BASE_URL ir SAKNE (bez /v1) — CLI pats pievieno /v1/messages.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# Oficiālais CLI dod priekšroku ANTHROPIC_API_KEY; drošības labad iestatiet abus.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ **Nelieciet** `/v1` iekš `ANTHROPIC_BASE_URL` — tas pārvēršas par `/v1/v1/messages` un neizdodas. Rīku izsaukumi un straumēšana darbojas pilnībā, pat ja tiek novirzīti uz ar OpenAI savietojamiem modeļiem.

### Codex CLI (Responses API)

Codex pieslēdzas, izmantojot OpenAI Responses API (`/v1/responses`); Chat Completions ceļš no Codex tika izņemts 2026. gada februārī.

```toml
# ~/.codex/config.toml
# model / model_provider ir dokumenta saknes atslēgas (jābūt virs [tabulas]).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex pievieno /responses → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex atbalsta tikai Responses API
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
// opencode.json   (vai: /connect → Other)
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

# Goose / OpenHands: pievienojiet modeļa ID priekšā openai/
#   model = openai/gpt-4.1
```

### Gemini CLI

Oficiālajam Gemini CLI ir vāja ārējo, ar OpenAI savietojamo, galapunktu atbalsts; jums var būt nepieciešams ar OpenAI savietojams ietinējs (wrapper) vai atzars (fork).

---

## 🖥 IDE / GUI aģenti

### Cline · Roo Code · Kilo Code · Cursor

Izvēlieties **OpenAI Compatible** (vai **Custom OpenAI**) kā nodrošinātāju un ielīmējiet:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Vienmēr izmantojiet **OpenAI Compatible slotu** — dedicētais OpenRouter ieraksts ir cietkodēts uz openrouter.ai un neizdosies. **Cursor** pieprasa `/v1` bāzes URL un netukšu atslēgas lauku. **Kilo Code** ir zināma kļūda (#681), kur pielāgotais bāzes URL netiek nodots modeļu saraksta veidošanai — ievadiet modeļa ID manuāli.

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

Ar `model: AUTODETECT` Continue automātiski ielādē modeļu sarakstu.

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

Lauku nosaukumi var atšķirties atkarībā no Zed versijas — pārbaudiet Zed dokumentāciju.

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
    base_url="https://router.pleum.ai",   # sakne, bez /v1 — SDK pievieno /v1/messages
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # darbojas jebkurš PleumRouter modelis
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Multimodālais — attēli · audio · video

Visas modalitātes ir ar OpenAI savietojami HTTP galapunkti ar to pašu atslēgu. Izvēlieties modeli, kas atbalsta attiecīgo modalitāti, no [`GET /v1/models`](https://pleum.ai/models).

```bash
# Attēlu ģenerēšana
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Teksts uz runu (atgriež audio baitus; izmaksas X-Cost-Krw galvenē)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Runa uz tekstu (multipart augšupielāde)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# Video ģenerēšana ir asinhrona: POST atgriež job_id, tad aptaujājiet GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### API virsma

| Galapunkts | Protokols |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (straumēšana, rīki, redze) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Attēlu ģenerēšana |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Asinhronais video |
| `GET /v1/models` | Modeļu katalogs (publisks) |
| `GET /v1/credits` | Bilance |

---

## 🔌 Vairāk aģentu

Lielākā daļa šeit neminēto aģentu darbojas tāpat — iestatiet ar OpenAI savietojamu bāzes URL:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** un citi.

Ar Anthropic savietojamo `/v1/messages`: **claude-code-router** arī pieslēdzas, izmantojot `ANTHROPIC_BASE_URL`.

**Modeļu ID**: atrodiet tos `GET /v1/models` vai [modeļu lapā](https://pleum.ai/models). Cline, Continue, OpenCode un citi automātiski ielādē sarakstu. OpenRouter formāta ID (`openai/gpt-5.5`) tiek konvertēti automātiski.

**LiteLLM starpniekserveris** (Aider, OpenHands, Open Interpreter, SWE-agent un gptme ir balstīti uz LiteLLM un pieslēdzas tieši — bet, ja jūs uzturat LiteLLM starpniekserveri):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # openai/ prefikss → OpenAI savietojamais ceļš
      api_base: https://router.pleum.ai/v1           # NEpievienojiet /chat/completions
      api_key: os.environ/PLEUM_API_KEY
```

---

## Kontribūcija

Vai jums izdevās palaist PleumRouter ar rīku, kas šeit nav minēts? PR ir gaidīti — pievienojiet sadaļu ar **pārbaudītu** konfigurācijas fragmentu (bāzes URL, atslēgas vides mainīgais, modeļa ID formāts un jebkādas nianses).

## Licence

[MIT](LICENSE)
