<div align="center">

# Hogyan használjuk a PleumRoutert

**Egyetlen API-kulcs 200+ AI-modellhez — OpenAI-kompatibilis, KRW-ben számlázva.**

[Weboldal](https://pleum.ai) · [Dokumentáció](https://pleum.ai/docs) · [Modellek](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · Magyar · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

A PleumRouter egy AI-átjáró (gateway): egy kulcs (`plm_…`), egy alap URL, 210+ modell 18 szolgáltatótól — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE és még sok más. Beszéli az **OpenAI Chat Completions**, az **Anthropic Messages** és az **OpenAI Responses** protokollokat, így szinte minden kódoló ügynök, IDE-bővítmény és SDK egyetlen soros konfigurációváltoztatással csatlakoztatható hozzá. A szöveg, a beágyazások (embeddings), a kép, a beszéd és a videó mind ugyanazon a kulcson keresztül fut.

Ez a repó **ellenőrzött integrációs recepteket** gyűjt össze. Az alábbi kódrészletek mindegyikét teszteltük az élő átjáró (gateway) ellen.

## Kezdő lépések

1. [Regisztráció](https://pleum.ai/signup) → Vezérlőpult → **API-kulcsok** → kulcs kiállítása (`plm_`-vel kezdődik).
2. Irányítsd az eszközödet az alap URL-re:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Néhány ügynök (OpenCode, Crush) a PLEUM_API_KEY-t olvassa be — ugyanaz a kulcs, mindkettőt állítsd be.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Füstteszt:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Regisztrációkor ₩1 000 ingyenes kreditet kapsz, első feltöltésnél pedig ₩5 000 bónuszt.

## Integrációk

| Kategória | Eszközök |
|---|---|
| [⚡ Egyparancsos indító](#-pleum-cli--a-gyors-út) | `pleum` CLI |
| [🤖 Terminálos kódoló ügynökök](#-terminál--cli-ügynökök) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE / GUI ügynökök](#-ide--gui-ügynökök) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK-k](#-sdk-k) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 Multimodális API](#-multimodális--kép--hang--videó) | Képek, TTS, STT, Videó, Beágyazások |
| [🔌 Minden más](#-további-ügynökök) | OpenRouter-stílusú azonosítók, LiteLLM proxy, 15+ további ügynök |

---

## ⚡ pleum CLI — a gyors út

A hivatalos CLI úgy indítja el a kedvenc ügynöködet, hogy az már be van drótozva a PleumRouterhez. Semmilyen konfigurációs fájlhoz nem nyúl.

```bash
npm install -g pleumrouter        # vagy: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # böngészős bejelentkezés, a kulcs automatikusan kiállításra és elmentésre kerül
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # terminálos chat REPL
pleum models                      # az összes modell listázása árazással
```

Automatikus indításhoz támogatott: `claude` · `aider` · `codex` · `goose` · `openhands` (ezenkívül konfigurációs kódrészletek a `opencode` · `crush` eszközökhöz). A meglévő eszközkonfigurációidat sosem módosítja.

---

## 🤖 Terminál / CLI ügynökök

### Claude Code (Anthropic-kompatibilis)

A Claude Code és a Claude Agent SDK eszközök az Anthropic-kompatibilis `/v1/messages` végponton keresztül csatlakoznak.

```bash
# Az ANTHROPIC_BASE_URL a GYÖKÉR (nincs /v1) — a CLI maga fűzi hozzá a /v1/messages részt.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# A hivatalos CLI az ANTHROPIC_API_KEY-t preferálja; a biztonság kedvéért mindkettőt állítsd be.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ **Ne** tedd bele a `/v1`-et az `ANTHROPIC_BASE_URL`-be — ekkor `/v1/v1/messages` lesz belőle, és nem fog működni. Az eszközhívások (tool calls) és a streaming végig-a-vonalon (end-to-end) működnek, még akkor is, ha OpenAI-kompatibilis modellekre irányítod őket.

### Codex CLI (Responses API)

A Codex az OpenAI Responses API-n (`/v1/responses`) keresztül csatlakozik; a Chat Completions útvonalat 2026 februárjában eltávolították a Codexből.

```toml
# ~/.codex/config.toml
# a model / model_provider dokumentumgyökér-szintű kulcsok (a [táblázat] fölött kell lenniük).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # a Codex hozzáfűzi a /responses-t → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # a Codex csak a Responses API-t támogatja
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
// opencode.json   (vagy: /connect → Other)
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

# Goose / OpenHands: a modellazonosító elé illeszd az openai/ előtagot
#   model = openai/gpt-4.1
```

### Gemini CLI

A felsőbb szintű (upstream) Gemini CLI gyengén támogatja a külső, OpenAI-kompatibilis végpontokat; szükséged lehet egy OpenAI-kompatibilis wrapperre vagy forkra.

---

## 🖥 IDE / GUI ügynökök

### Cline · Roo Code · Kilo Code · Cursor

Válaszd az **OpenAI Compatible** (vagy **Custom OpenAI**) opciót szolgáltatóként, és illeszd be:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Mindig az **OpenAI Compatible mezőt** használd — a dedikált OpenRouter bejegyzés keményen az openrouter.ai-ra van kódolva, és nem fog működni. A **Cursor** megköveteli a `/v1`-et az alap URL-ben és egy nem üres kulcsmezőt. A **Kilo Code**-nak van egy ismert hibája (#681), amelynél az egyéni alap URL nem kerül átadásra a modell listázásához — add meg kézzel a modellazonosítót.

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

A `model: AUTODETECT` beállítással a Continue automatikusan lehívja a modell listát.

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

A mezőnevek Zed-verziónként eltérhetnek — ellenőrizd a Zed dokumentációját.

---

## 📦 SDK-k

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
    base_url="https://router.pleum.ai",   # gyökér, nincs /v1 — az SDK hozzáfűzi a /v1/messages-t
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # bármelyik PleumRouter-modell működik
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Multimodális — kép · hang · videó

Minden modalitás OpenAI-kompatibilis HTTP-végpontokon keresztül érhető el, ugyanazon a kulcson. Válassz egy olyan modellt, amely támogatja az adott modalitást a [`GET /v1/models`](https://pleum.ai/models) alapján.

```bash
# Kép generálás
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Szövegből beszéd (audio bájtokat ad vissza; a költség az X-Cost-Krw fejlécben van)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Beszédből szöveg (multipart feltöltés)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# A videó generálás aszinkron: a POST egy job_id-t ad vissza, majd lekérdezheted a GET /v1/jobs/{job_id} végponttal
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### API felület

| Végpont | Protokoll |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (streaming, eszközök, látás) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Kép generálás |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Aszinkron videó |
| `GET /v1/models` | Modellkatalógus (nyilvános) |
| `GET /v1/credits` | Egyenleg |

---

## 🔌 További ügynökök

A legtöbb itt fel nem sorolt ügynök ugyanúgy működik — állítsd be az OpenAI-kompatibilis alap URL-t:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** és még sok más.

Az Anthropic-kompatibilis `/v1/messages` révén: a **claude-code-router** is csatlakozik az `ANTHROPIC_BASE_URL`-lel.

**Modellazonosítók**: megtalálod őket a `GET /v1/models` végponton vagy a [modellek oldalon](https://pleum.ai/models). A Cline, a Continue, az OpenCode és mások automatikusan lehívják a listát. Az OpenRouter-formátumú azonosítók (`openai/gpt-5.5`) automatikusan konvertálásra kerülnek.

**LiteLLM proxy** (az Aider, az OpenHands, az Open Interpreter, az SWE-agent és a gptme LiteLLM-alapúak, és közvetlenül csatlakoznak — de ha megtartasz egy LiteLLM proxyt):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # openai/ előtag → OpenAI-kompatibilis útvonal
      api_base: https://router.pleum.ai/v1           # NE fűzd hozzá a /chat/completions részt
      api_key: os.environ/PLEUM_API_KEY
```

---

## Közreműködés

Sikerült működésre bírnod a PleumRoutert egy itt nem szereplő eszközzel? Szívesen fogadunk PR-eket — adj hozzá egy szekciót egy **tesztelt** konfigurációs kódrészlettel (alap URL, kulcs env, modellazonosító-formátum és bármilyen buktató).

## Licenc

[MIT](LICENSE)
