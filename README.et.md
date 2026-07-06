<div align="center">

# Kuidas kasutada PleumRouterit

**Üks API-võti 200+ AI-mudeli jaoks — OpenAI-ga ühilduv, arveldatakse KRW-s.**

[Veebisait](https://pleum.ai) · [Dokumentatsioon](https://pleum.ai/docs) · [Mudelid](https://pleum.ai/models) · [Mänguväljak](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · Eesti · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter on AI-lüüs: üks võti (`plm_…`), üks baas-URL, 210+ mudelit 18 pakkujalt — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE ja teised. See toetab **OpenAI Chat Completions**, **Anthropic Messages** ja **OpenAI Responses** protokolle, nii et peaaegu iga kodeerimisagent, IDE plugin ja SDK ühendub ühe konfiguratsioonimuudatusega. Tekst, manused (embeddings), pilt, kõne ja video töötavad kõik sama võtme kaudu.

See repositoorium kogub kokku **kontrollitud integratsiooniretseptid**. Iga allolev koodilõik on testitud reaalse lüüsi vastu.

## Alustamine

1. [Registreeru](https://pleum.ai/signup) → Töölaud (Dashboard) → **API Keys** → väljasta võti (algab `plm_`-ga).
2. Suuna oma tööriist baas-URL-ile:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Mõned agendid (OpenCode, Crush) loevad PLEUM_API_KEY — sama võti, määra mõlemad.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Suitsutest:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Registreerumisel saad ₩1,000 tasuta krediiti ja esimese laadimise puhul ₩5,000 boonust.

## Integratsioonid

| Kategooria | Tööriistad |
|---|---|
| [⚡ Ühe käsuga käivitaja](#-pleum-cli--kiire-tee) | `pleum` CLI |
| [🤖 Terminali kodeerimisagendid](#-terminali--cli-agendid) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE / GUI agendid](#-ide--gui-agendid) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK-d](#-sdk-d) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 Multimodaalne API](#-multimodaalne--pilt--heli--video) | Pildid, TTS, STT, Video, Manused (Embeddings) |
| [🔌 Kõik muu](#-veel-agente) | OpenRouteri-stiilis ID-d, LiteLLM proksi, 15+ muud agenti |

---

## ⚡ pleum CLI — kiire tee

Ametlik CLI käivitab su lemmikagendi juba PleumRouteriga ühendatuna. Konfiguratsioonifaile ei puudutata.

```bash
npm install -g pleumrouter        # või: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # sisselogimine brauseris, võti väljastatakse ja salvestatakse automaatselt
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # terminali vestluse REPL
pleum models                      # loetle kõik mudelid koos hindadega
```

Automaatkäivituseks toetatud: `claude` · `aider` · `codex` · `goose` · `openhands` (pluss konfiguratsioonilõigud `opencode` · `crush` jaoks). Su olemasolevaid tööriistade seadeid ei muudeta kunagi.

---

## 🤖 Terminali / CLI agendid

### Claude Code (Anthropic-ühilduv)

Claude Code ja Claude Agent SDK tööriistad ühenduvad Anthropic-ühilduva `/v1/messages` lõpp-punkti kaudu.

```bash
# ANTHROPIC_BASE_URL on JUUR (ilma /v1) — CLI lisab ise /v1/messages.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# Ametlik CLI eelistab ANTHROPIC_API_KEY; määra kindluse mõttes mõlemad.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ **Ära** pane `/v1` väärtusesse `ANTHROPIC_BASE_URL` — see muutub kujule `/v1/v1/messages` ja ebaõnnestub. Tööriistakutsed (tool calls) ja voogedastus (streaming) töötavad tervikuna, isegi kui suunatud OpenAI-ühilduvatele mudelitele.

### Codex CLI (Responses API)

Codex ühendub OpenAI Responses API (`/v1/responses`) kaudu; Chat Completions tee eemaldati Codexist 2026. aasta veebruaris.

```toml
# ~/.codex/config.toml
# model / model_provider on dokumendi juurtasandi võtmed (peavad olema enne [tabelit]).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex lisab /responses → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex toetab ainult Responses API-t
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
// opencode.json   (või: /connect → Other)
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

# Goose / OpenHands: lisa mudeli ID-le eesliide openai/
#   model = openai/gpt-4.1
```

### Gemini CLI

Ülesvoolu (upstream) Gemini CLI-l on nõrk tugi väliste OpenAI-ühilduvate lõpp-punktide jaoks; võid vajada OpenAI-ühilduvat ümbrist (wrapper) või harudest (fork) versiooni.

---

## 🖥 IDE / GUI agendid

### Cline · Roo Code · Kilo Code · Cursor

Vali pakkujaks **OpenAI Compatible** (või **Custom OpenAI**) ja kleebi:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Kasuta alati **OpenAI Compatible pesa** — spetsiaalne OpenRouteri kirje on kõvakodeeritud domeenile openrouter.ai ja ebaõnnestub. **Cursor** nõuab `/v1` baas-URL-is ja tühjast väärtusest erinevat võtmevälja. **Kilo Code'il** on teadaolev probleem (#681), kus kohandatud baas-URL-i ei edastata mudelite loetelusse — sisesta mudeli ID käsitsi.

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

Kui `model: AUTODETECT`, tõmbab Continue mudelite loetelu automaatselt.

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

Väljanimed võivad Zedi versiooniti erineda — kontrolli Zedi dokumentatsiooni.

---

## 📦 SDK-d

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
    base_url="https://router.pleum.ai",   # juur, ilma /v1 — SDK lisab /v1/messages
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # töötab iga PleumRouteri mudeliga
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Multimodaalne — pilt · heli · video

Kõik modaalsused on OpenAI-ühilduvad HTTP-lõpp-punktid sama võtme peal. Vali modaalsust toetav mudel [`GET /v1/models`](https://pleum.ai/models) kaudu.

```bash
# Pildi genereerimine
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Tekst-kõneks (Text-to-speech; tagastab helibaidid; hind X-Cost-Krw päises)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Kõne-tekstiks (Speech-to-text; multipart üleslaadimine)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# Video genereerimine on asünkroonne: POST tagastab job_id, seejärel küsi GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### API pind

| Lõpp-punkt | Protokoll |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (voogedastus, tööriistad, nägemine) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Pildi genereerimine |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Asünkroonne video |
| `GET /v1/models` | Mudelikataloog (avalik) |
| `GET /v1/credits` | Saldo |

---

## 🔌 Veel agente

Enamik siin loetlemata agente töötab samamoodi — määra OpenAI-ühilduv baas-URL:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** ja teised.

Anthropic-ühilduva `/v1/messages` kaudu: **claude-code-router** ühendub samuti muutuja `ANTHROPIC_BASE_URL` abil.

**Mudeli ID-d**: leia need `GET /v1/models` kaudu või [mudelite lehelt](https://pleum.ai/models). Cline, Continue, OpenCode ja teised tõmbavad loetelu automaatselt. OpenRouter-vormingus ID-d (`openai/gpt-5.5`) teisendatakse automaatselt.

**LiteLLM proksi** (Aider, OpenHands, Open Interpreter, SWE-agent ja gptme põhinevad LiteLLM-il ning ühenduvad otse — aga kui pead LiteLLM proksit):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # openai/ eesliide → OpenAI-ühilduv marsruut
      api_base: https://router.pleum.ai/v1           # ÄRA lisa /chat/completions
      api_key: os.environ/PLEUM_API_KEY
```

---

## Panustamine

Said PleumRouteri tööle mõne siin loetlemata tööriistaga? PR-id on teretulnud — lisa jaotis koos **testitud** konfiguratsiooniga (baas-URL, võtme keskkonnamuutuja, mudeli ID formaat ja kõik nüansid).

## Litsents

[MIT](LICENSE)
