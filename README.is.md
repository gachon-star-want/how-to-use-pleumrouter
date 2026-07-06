<div align="center">

# Hvernig á að nota PleumRouter

**Einn API-lykill fyrir 200+ gervigreindarlíkön — OpenAI-samhæft, gjaldfært í KRW.**

[Vefsíða](https://pleum.ai) · [Skjöl](https://pleum.ai/docs) · [Líkön](https://pleum.ai/models) · [Leikvöllur](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · Íslenska

</div>

PleumRouter er gervigreindargátt: einn lykill (`plm_…`), ein grunnslóð, 210+ líkön frá 18 þjónustuveitum — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE og fleiri. Hún talar **OpenAI Chat Completions**, **Anthropic Messages** og **OpenAI Responses**, þannig að nánast hver einasti kóðunaraðstoðarmaður, IDE-viðbót og SDK tengist með einnar línu breytingu á stillingum. Texti, ívafsvektorar (embeddings), mynd, tal og myndband — allt keyrir í gegnum sama lykilinn.

Þetta safn inniheldur **staðfestar samþættingaruppskriftir**. Hvert einasta kóðabrot hér að neðan hefur verið prófað á lifandi gáttinni.

## Að byrja

1. [Skráðu þig](https://pleum.ai/signup) → Mælaborð → **API-lyklar** → gefðu út lykil (byrjar á `plm_`).
2. Beindu tólinu þínu á grunnslóðina:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Sum umboð (OpenCode, Crush) lesa PLEUM_API_KEY — sami lykill, settu bæði.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Reyksprófun:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Þú færð ₩1.000 í frían inneign við skráningu og ₩5.000 bónus við fyrstu innborgun.

## Samþættingar

| Flokkur | Verkfæri |
|---|---|
| [⚡ Eins skipunar ræsir](#-pleum-cli--hraðleiðin) | `pleum` CLI |
| [🤖 Kóðunarumboð í flugstöð](#-umboð-í-flugstöð--cli) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE / GUI-umboð](#-ide--gui-umboð) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK](#-sdk) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 Fjölmiðla-API](#-fjölmiðlun--mynd--hljóð--myndband) | Myndir, TTS, STT, Myndband, Ívafsvektorar |
| [🔌 Allt annað](#-fleiri-umboð) | OpenRouter-stíls auðkenni, LiteLLM-milliþjónn, 15+ umboð til viðbótar |

---

## ⚡ pleum CLI — hraðleiðin

Opinbera skipanalínuviðmótið (CLI) ræsir uppáhalds umboðið þitt sem er nú þegar tengt við PleumRouter. Engum stillingaskrám er breytt.

```bash
npm install -g pleumrouter        # eða: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # innskráning í vafra, lykill gefinn út og vistaður sjálfkrafa
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # spjallviðmót (REPL) í flugstöð
pleum models                      # birtir öll líkön með verðlagningu
```

Stutt fyrir sjálfvirka ræsingu: `claude` · `aider` · `codex` · `goose` · `openhands` (auk stillingabrota fyrir `opencode` · `crush`). Núverandi stillingum tólanna þinna er aldrei breytt.

---

## 🤖 Umboð í flugstöð / CLI

### Claude Code (Anthropic-samhæft)

Claude Code og Claude Agent SDK-tól tengjast í gegnum Anthropic-samhæfa `/v1/messages` endapunktinn.

```bash
# ANTHROPIC_BASE_URL er RÓTIN (engin /v1) — CLI bætir /v1/messages sjálft við.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# Opinbera skipanalínuviðmótið kýs frekar ANTHROPIC_API_KEY; settu bæði til öryggis.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ Ekki setja `/v1` í `ANTHROPIC_BASE_URL` — það verður að `/v1/v1/messages` og mistekst. Verkfæraköll og streymi virka frá enda til enda, jafnvel þegar beint er á OpenAI-samhæf líkön.

### Codex CLI (Responses API)

Codex tengist í gegnum OpenAI Responses API (`/v1/responses`); Chat Completions-leiðin var fjarlægð úr Codex í febrúar 2026.

```toml
# ~/.codex/config.toml
# model / model_provider eru lyklar á rótarstigi skjalsins (verða að vera fyrir ofan [töfluna]).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex bætir /responses við → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex styður einungis Responses API
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
// opencode.json   (eða: /connect → Other)
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

# Goose / OpenHands: settu forskeytið openai/ framan við líkanauðkennið
#   model = openai/gpt-4.1
```

### Gemini CLI

Upprunalega Gemini CLI hefur veikan stuðning við ytra OpenAI-samhæfa endapunkta; þú gætir þurft OpenAI-samhæfan hjúp (wrapper) eða klón (fork).

---

## 🖥 IDE / GUI-umboð

### Cline · Roo Code · Kilo Code · Cursor

Veldu **OpenAI Compatible** (eða **Custom OpenAI**) sem þjónustuveitanda og límdu inn:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Notaðu alltaf **OpenAI Compatible-svæðið** — sérstaki OpenRouter-reiturinn er harðkóðaður á openrouter.ai og mun mistakast. **Cursor** krefst `/v1` í grunnslóðinni og að lykilreiturinn sé ekki tómur. **Kilo Code** er með þekkt vandamál (#681) þar sem sérsniðin grunnslóð er ekki send áfram við uppflettingu líkana — sláðu líkanauðkennið inn handvirkt.

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

Með `model: AUTODETECT` sækir Continue líkanalistann sjálfkrafa.

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

Nöfn reita geta verið mismunandi eftir útgáfu Zed — athugaðu skjöl Zed.

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
    base_url="https://router.pleum.ai",   # rót, engin /v1 — SDK bætir /v1/messages við
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # sérhvert PleumRouter-líkan virkar
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Fjölmiðlun — mynd · hljóð · myndband

Öll form (modalities) eru OpenAI-samhæfir HTTP-endapunktar undir sama lykli. Veldu líkan sem styður formið af [`GET /v1/models`](https://pleum.ai/models).

```bash
# Myndgerð
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Texti í tal (skilar hljóðbætum; kostnaður í X-Cost-Krw haus)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Tal í texta (multipart-upphal)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# Myndbandagerð er ósamstillt (async): POST skilar job_id, síðan er GET /v1/jobs/{job_id} kannað reglulega
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### API-yfirborð

| Endapunktur | Samskiptaregla |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (streymi, verkfæri, sjón) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Myndgerð |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Ósamstillt myndband |
| `GET /v1/models` | Líkanaskrá (opinber) |
| `GET /v1/credits` | Inneign |

---

## 🔌 Fleiri umboð

Flest umboð sem ekki eru talin upp hér virka á sama hátt — settu upp OpenAI-samhæfu grunnslóðina:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** og fleiri.

Í gegnum Anthropic-samhæfa `/v1/messages`: **claude-code-router** tengist einnig með `ANTHROPIC_BASE_URL`.

**Líkanauðkenni**: finndu þau á `GET /v1/models` eða á [líkanasíðunni](https://pleum.ai/models). Cline, Continue, OpenCode og önnur sækja listann sjálfkrafa. Auðkenni á OpenRouter-sniði (`openai/gpt-5.5`) eru umbreytt sjálfkrafa.

**LiteLLM-milliþjónn** (Aider, OpenHands, Open Interpreter, SWE-agent og gptme eru byggð á LiteLLM og tengjast beint — en ef þú heldur úti LiteLLM-milliþjóni):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # openai/ forskeyti → OpenAI-samhæf leið
      api_base: https://router.pleum.ai/v1           # EKKI bæta /chat/completions við
      api_key: os.environ/PLEUM_API_KEY
```

---

## Framlög

Tókst þér að fá PleumRouter til að virka með tóli sem er ekki talið upp hér? PR-beiðnir vel þegnar — bættu við kafla með **prófuðu** stillingabroti (grunnslóð, lykil-umhverfisbreytu, snið líkanauðkennis og hvers kyns gildrur).

## Notkunarleyfi

[MIT](LICENSE)
