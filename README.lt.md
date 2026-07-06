<div align="center">

# Kaip naudoti „PleumRouter“

**Vienas API raktas 200+ DI modelių — suderinama su „OpenAI“, apmokestinama KRW.**

[Svetainė](https://pleum.ai) · [Dokumentacija](https://pleum.ai/docs) · [Modeliai](https://pleum.ai/models) · [Žaidimų aikštelė](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · Lietuvių · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

„PleumRouter“ yra DI šliuzas: vienas raktas (`plm_…`), vienas bazinis URL, 210+ modelių iš 18 tiekėjų — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE ir kt. Jis palaiko **„OpenAI“ Chat Completions**, **„Anthropic“ Messages** ir **„OpenAI“ Responses** protokolus, todėl beveik kiekvienas kodavimo agentas, IDE papildinys ir SDK prisijungia pakeitus vos vieną konfigūracijos eilutę. Tekstas, embedingai, vaizdas, garsas ir vaizdo įrašai — visi veikia per tą patį raktą.

Šioje saugykloje sukauptos **patikrintos integravimo receptūros**. Kiekvienas toliau pateiktas kodo fragmentas išbandytas prieš veikiančią sistemą (live gateway).

## Pradžia

1. [Registruokitės](https://pleum.ai/signup) → Valdymo skydelis (Dashboard) → **API raktai** → išduokite raktą (prasideda `plm_`).
2. Nukreipkite savo įrankį į bazinį URL:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Kai kurie agentai (OpenCode, Crush) skaito PLEUM_API_KEY — tas pats raktas, nustatykite abu.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Bandomasis testas:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Registruodamiesi gaunate ₩1,000 nemokamo kredito, o pirmojo papildymo metu — ₩5,000 premiją.

## Integracijos

| Kategorija | Įrankiai |
|---|---|
| [⚡ Vienos komandos paleidiklis](#-pleum-cli--greitasis-kelias) | `pleum` CLI |
| [🤖 Terminalo kodavimo agentai](#-terminalo--cli-agentai) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE / GUI agentai](#-ide--gui-agentai) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK](#-sdk) | „OpenAI“ SDK (Python/JS), „Anthropic“ SDK |
| [🎨 Multimodalinis API](#-multimodalinis--vaizdas--garsas--video) | Vaizdai, TTS, STT, vaizdo įrašai, embedingai |
| [🔌 Visa kita](#-daugiau-agentu) | „OpenRouter“ stiliaus ID, „LiteLLM“ tarpinis serveris, 15+ kitų agentų |

---

## ⚡ pleum CLI — greitasis kelias

Oficialus CLI įrankis paleidžia jūsų mėgstamą agentą, jau sujungtą su „PleumRouter“. Jokių konfigūracijos failų liesti nereikia.

```bash
npm install -g pleumrouter        # arba: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # prisijungimas per naršyklę, raktas išduodamas ir išsaugomas automatiškai
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # terminalo pokalbių REPL
pleum models                      # visų modelių sąrašas su kainomis
```

Automatinis paleidimas palaikomas: `claude` · `aider` · `codex` · `goose` · `openhands` (taip pat konfigūracijos fragmentai skirti `opencode` · `crush`). Jūsų esami įrankių konfigūracijos failai niekada nekeičiami.

---

## 🤖 Terminalo / CLI agentai

### Claude Code (suderinama su „Anthropic“)

Claude Code ir Claude Agent SDK įrankiai jungiasi per su „Anthropic“ suderinamą `/v1/messages` galinį tašką.

```bash
# ANTHROPIC_BASE_URL yra ŠAKNIS (be /v1) — CLI pats prideda /v1/messages.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# Oficialus CLI pirmenybę teikia ANTHROPIC_API_KEY; nustatykite abu saugumo dėlei.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ **Neįrašykite** `/v1` į `ANTHROPIC_BASE_URL` — tuomet gaunasi `/v1/v1/messages` ir įvyksta klaida. Įrankių iškvietimai ir srautinis perdavimas (streaming) veikia visapusiškai, net kai nukreipiama į su „OpenAI“ suderinamus modelius.

### Codex CLI (Responses API)

Codex jungiasi per „OpenAI“ Responses API (`/v1/responses`); Chat Completions kelias iš Codex buvo pašalintas 2026 m. vasarį.

```toml
# ~/.codex/config.toml
# model / model_provider yra dokumento šakninio lygio raktai (turi būti virš [lentelės]).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex prideda /responses → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex palaiko tik Responses API
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
// opencode.json   (arba: /connect → Other)
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

# Goose / OpenHands: prieš modelio ID pridėkite openai/
#   model = openai/gpt-4.1
```

### Gemini CLI

Oficiali „Gemini CLI“ silpnai palaiko išorinius, su „OpenAI“ suderinamus galinius taškus; gali prireikti su „OpenAI“ suderinamo apvalkalo (wrapper) ar šakės (fork).

---

## 🖥 IDE / GUI agentai

### Cline · Roo Code · Kilo Code · Cursor

Pasirinkite **OpenAI Compatible** (arba **Custom OpenAI**) kaip tiekėją ir įklijuokite:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Visada naudokite **OpenAI Compatible langelį** — specialus „OpenRouter“ laukas yra fiksuotas ties openrouter.ai ir neveiks. **Cursor** reikalauja `/v1` bazinio URL adrese ir neturi likti tuščias rakto laukas. **Kilo Code** turi žinomą problemą (#681), kai pasirinktinis bazinis URL neperduodamas modelių sąrašo formavimui — modelio ID įveskite rankiniu būdu.

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

Su `model: AUTODETECT` „Continue“ automatiškai gauna modelių sąrašą.

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

Laukų pavadinimai gali skirtis priklausomai nuo „Zed“ versijos — pasitikrinkite „Zed“ dokumentacijoje.

---

## 📦 SDK

### „OpenAI“ SDK (Python)

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

### „OpenAI“ SDK (JavaScript / TypeScript)

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

### „Anthropic“ SDK

```python
import anthropic

client = anthropic.Anthropic(
    base_url="https://router.pleum.ai",   # šaknis, be /v1 — SDK pats prideda /v1/messages
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # veikia bet kuris „PleumRouter“ modelis
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Multimodalinis — vaizdas · garsas · video

Visos modalybės yra su „OpenAI“ suderinami HTTP galiniai taškai, veikiantys su tuo pačiu raktu. Pasirinkite modalybę palaikantį modelį iš [`GET /v1/models`](https://pleum.ai/models).

```bash
# Vaizdo generavimas
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Teksto konvertavimas į kalbą (Text-to-speech; grąžina garso baitus; kaina X-Cost-Krw antraštėje)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Kalbos atpažinimas į tekstą (Speech-to-text; kelių dalių (multipart) įkėlimas)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# Vaizdo įrašo generavimas yra asinchroninis: POST grąžina job_id, tada tikrinkite GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### API paviršius

| Galinis taškas | Protokolas |
|---|---|
| `POST /v1/chat/completions` | „OpenAI“ Chat Completions (srautinis perdavimas, įrankiai, vaizdas) |
| `POST /v1/messages` | „Anthropic“ Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | „OpenAI“ Responses (Codex CLI) |
| `POST /v1/embeddings` | „OpenAI“ Embeddings |
| `POST /v1/images/generations` | Vaizdo generavimas |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Asinchroninis vaizdo įrašas |
| `GET /v1/models` | Modelių katalogas (viešas) |
| `GET /v1/credits` | Likutis |

---

## 🔌 Daugiau agentų

Dauguma čia neišvardytų agentų veikia taip pat — nustatykite su „OpenAI“ suderinamą bazinį URL:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** ir kiti.

Per su „Anthropic“ suderinamą `/v1/messages`: **claude-code-router** taip pat jungiasi naudojant `ANTHROPIC_BASE_URL`.

**Modelių ID**: raskite juos per `GET /v1/models` arba [modelių puslapyje](https://pleum.ai/models). Cline, Continue, OpenCode ir kiti automatiškai gauna sąrašą. „OpenRouter“ formato ID (`openai/gpt-5.5`) konvertuojami automatiškai.

**„LiteLLM“ tarpinis serveris** (Aider, OpenHands, Open Interpreter, SWE-agent ir gptme yra pagrįsti „LiteLLM“ ir jungiasi tiesiogiai — bet jei naudojate „LiteLLM“ tarpinį serverį):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # openai/ priešdėlis → su OpenAI suderintas maršrutas
      api_base: https://router.pleum.ai/v1           # NEpridėkite /chat/completions
      api_key: os.environ/PLEUM_API_KEY
```

---

## Prisidėjimas

Pavyko paleisti „PleumRouter“ su čia neišvardytu įrankiu? Laukiame PR — pridėkite skyrių su **išbandytu** konfigūracijos fragmentu (bazinis URL, rakto aplinkos kintamasis, modelio ID formatas ir bet kokios spąstų vietos).

## Licencija

[MIT](LICENSE)
