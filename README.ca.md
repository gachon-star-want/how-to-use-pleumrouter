<div align="center">

# Com utilitzar PleumRouter

**Una sola clau API per a més de 200 models d'IA — compatible amb OpenAI, facturat en KRW.**

[Lloc web](https://pleum.ai) · [Documentació](https://pleum.ai/docs) · [Models](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · Català · [Íslenska](README.is.md)

</div>

PleumRouter és una passarel·la d'IA: una clau (`plm_…`), un URL base, més de 210 models de 18 proveïdors — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE i més. Parla **OpenAI Chat Completions**, **Anthropic Messages** i **OpenAI Responses**, de manera que gairebé qualsevol agent de codi, connector d'IDE i SDK es connecta amb un canvi de configuració d'una sola línia. Text, incrustacions (embeddings), imatge, veu i vídeo funcionen tots amb la mateixa clau.

Aquest repositori recull **receptes d'integració verificades**. Cada fragment de codi de més avall s'ha provat contra la passarel·la real en producció.

## Primers passos

1. [Registra't](https://pleum.ai/signup) → Tauler → **Claus API** → emet una clau (comença amb `plm_`).
2. Apunta la teva eina a l'URL base:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Alguns agents (OpenCode, Crush) llegeixen PLEUM_API_KEY — mateixa clau, defineix totes dues.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Prova de fum:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Reps ₩1.000 de crèdit gratuït en registrar-te i un bonus de ₩5.000 en la teva primera recàrrega.

## Integracions

| Categoria | Eines |
|---|---|
| [⚡ Llançador d'una sola ordre](#-pleum-cli--el-camí-ràpid) | CLI `pleum` |
| [🤖 Agents de codi de terminal](#-agents-de-terminal--cli) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 Agents d'IDE / GUI](#-agents-dide--gui) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDKs](#-sdks) | SDK d'OpenAI (Python/JS), SDK d'Anthropic |
| [🎨 API multimodal](#-multimodal--imatge--àudio--vídeo) | Imatges, TTS, STT, Vídeo, Incrustacions |
| [🔌 Tota la resta](#-més-agents) | IDs a l'estil OpenRouter, proxy LiteLLM, més de 15 agents addicionals |

---

## ⚡ pleum CLI — el camí ràpid

La CLI oficial llança el teu agent preferit ja connectat a PleumRouter. No es toca cap fitxer de configuració.

```bash
npm install -g pleumrouter        # o: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # inici de sessió al navegador, clau emesa i desada automàticament
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # REPL de xat de terminal
pleum models                      # llista tots els models amb els seus preus
```

Compatible amb llançament automàtic: `claude` · `aider` · `codex` · `goose` · `openhands` (a més de fragments de configuració per a `opencode` · `crush`). Les configuracions de les teves eines existents mai es modifiquen.

---

## 🤖 Agents de terminal / CLI

### Claude Code (compatible amb Anthropic)

Claude Code i les eines del SDK d'agents de Claude es connecten a través de l'endpoint `/v1/messages`, compatible amb Anthropic.

```bash
# ANTHROPIC_BASE_URL és l'ARREL (sense /v1) — la CLI hi afegeix /v1/messages ella mateixa.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# La CLI oficial prefereix ANTHROPIC_API_KEY; defineix totes dues per anar sobre segur.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ **No** posis `/v1` a `ANTHROPIC_BASE_URL` — es converteix en `/v1/v1/messages` i falla. Les crides a eines i el streaming funcionen de cap a cap, fins i tot quan s'encaminen a models compatibles amb OpenAI.

### Codex CLI (API de Responses)

Codex es connecta a través de l'API de Responses d'OpenAI (`/v1/responses`); el camí de Chat Completions es va eliminar de Codex el febrer de 2026.

```toml
# ~/.codex/config.toml
# model / model_provider són claus de l'arrel del document (han d'anar per sobre de la [taula]).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex hi afegeix /responses → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex només admet l'API de Responses
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
// opencode.json   (o: /connect → Other)
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

# Goose / OpenHands: anteposa openai/ a l'id del model
#   model = openai/gpt-4.1
```

### Gemini CLI

La versió original de Gemini CLI té un suport feble per a endpoints externs compatibles amb OpenAI; potser necessitaràs un embolcall (wrapper) o una bifurcació (fork) compatible amb OpenAI.

---

## 🖥 Agents d'IDE / GUI

### Cline · Roo Code · Kilo Code · Cursor

Selecciona **OpenAI Compatible** (o **Custom OpenAI**) com a proveïdor i enganxa:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Utilitza sempre la **ranura OpenAI Compatible** — l'entrada dedicada a OpenRouter està codificada de manera fixa a openrouter.ai i fallarà. **Cursor** requereix `/v1` a l'URL base i un camp de clau no buit. **Kilo Code** té un problema conegut (#681) en què l'URL base personalitzat no es passa al llistat de models — introdueix l'id del model manualment.

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

Amb `model: AUTODETECT`, Continue obté automàticament la llista de models.

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

Els noms dels camps poden variar segons la versió de Zed — consulta la documentació de Zed.

---

## 📦 SDKs

### SDK d'OpenAI (Python)

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

### SDK d'OpenAI (JavaScript / TypeScript)

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

### SDK d'Anthropic

```python
import anthropic

client = anthropic.Anthropic(
    base_url="https://router.pleum.ai",   # arrel, sense /v1 — el SDK hi afegeix /v1/messages
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # funciona amb qualsevol model de PleumRouter
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Multimodal — imatge · àudio · vídeo

Totes les modalitats són endpoints HTTP compatibles amb OpenAI que utilitzen la mateixa clau. Tria un model que admeti la modalitat des de [`GET /v1/models`](https://pleum.ai/models).

```bash
# Generació d'imatges
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Text a veu (retorna bytes d'àudio; cost a la capçalera X-Cost-Krw)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Veu a text (càrrega multipart)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# La generació de vídeo és asíncrona: el POST retorna un job_id, després consulta GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### Superfície de l'API

| Endpoint | Protocol |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (streaming, eines, visió) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, SDK d'agents) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Generació d'imatges |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Vídeo asíncron |
| `GET /v1/models` | Catàleg de models (públic) |
| `GET /v1/credits` | Saldo |

---

## 🔌 Més agents

La majoria d'agents que no figuren aquí funcionen igual — defineix l'URL base compatible amb OpenAI:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** i més.

Via l'endpoint `/v1/messages` compatible amb Anthropic: **claude-code-router** també es connecta amb `ANTHROPIC_BASE_URL`.

**IDs de models**: troba'ls a `GET /v1/models` o a la [pàgina de models](https://pleum.ai/models). Cline, Continue, OpenCode i altres obtenen la llista automàticament. Els IDs en format OpenRouter (`openai/gpt-5.5`) es converteixen automàticament.

**Proxy LiteLLM** (Aider, OpenHands, Open Interpreter, SWE-agent i gptme es basen en LiteLLM i es connecten directament — però si manténs un proxy LiteLLM):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # prefix openai/ → ruta compatible amb OpenAI
      api_base: https://router.pleum.ai/v1           # NO hi afegeixis /chat/completions
      api_key: os.environ/PLEUM_API_KEY
```

---

## Contribucions

Has fet funcionar PleumRouter amb una eina que no figura aquí? Les PR són benvingudes — afegeix una secció amb un fragment de configuració **provat** (URL base, variable d'entorn de la clau, format de l'id del model i qualsevol parany a evitar).

## Llicència

[MIT](LICENSE)
