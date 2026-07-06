<div align="center">

# Jak používat PleumRouter

**Jeden API klíč pro 200+ AI modelů — kompatibilní s OpenAI, účtováno v KRW.**

[Web](https://pleum.ai) · [Dokumentace](https://pleum.ai/docs) · [Modely](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · Čeština · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter je AI brána: jeden klíč (`plm_…`), jedna základní URL adresa, 210+ modelů od 18 poskytovatelů — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE a další. Podporuje **OpenAI Chat Completions**, **Anthropic Messages** a **OpenAI Responses**, takže se s ní téměř každý kódovací agent, IDE plugin a SDK propojí jedinou úpravou konfigurace. Text, embeddingy, obraz, řeč i video běží přes stejný klíč.

Tento repozitář shromažďuje **ověřené integrační recepty**. Každá ukázka níže je otestována proti živé bráně.

## Začínáme

1. [Zaregistrujte se](https://pleum.ai/signup) → Dashboard → **API Keys** → vygenerujte klíč (začíná na `plm_`).
2. Nasměrujte svůj nástroj na základní URL adresu:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Někteří agenti (OpenCode, Crush) čtou PLEUM_API_KEY — stejný klíč, nastavte oba.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Rychlý test:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Při registraci získáte ₩1 000 kredit zdarma a ₩5 000 bonus při první dobíjení.

## Integrace

| Kategorie | Nástroje |
|---|---|
| [⚡ Spouštěč na jeden příkaz](#-pleum-cli--rychlá-cesta) | CLI `pleum` |
| [🤖 Termináloví kódovací agenti](#-terminálcli-agenti) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE / GUI agenti](#-ide--gui-agenti) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK](#-sdk) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 Multimodální API](#-multimodální--obraz--zvuk--video) | Obrázky, TTS, STT, Video, Embeddingy |
| [🔌 Vše ostatní](#-další-agenti) | ID ve stylu OpenRouter, LiteLLM proxy, 15+ dalších agentů |

---

## ⚡ pleum CLI — rychlá cesta

Oficiální CLI spustí vašeho oblíbeného agenta již propojeného s PleumRouter. Žádné konfigurační soubory se nemění.

```bash
npm install -g pleumrouter        # nebo: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # přihlášení přes prohlížeč, klíč se automaticky vygeneruje a uloží
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # terminálový chatovací REPL
pleum models                      # seznam všech modelů s cenami
```

Podporováno pro automatické spuštění: `claude` · `aider` · `codex` · `goose` · `openhands` (plus konfigurační úryvky pro `opencode` · `crush`). Vaše stávající konfigurace nástrojů se nikdy neupravují.

---

## 🤖 Terminál / CLI agenti

### Claude Code (kompatibilní s Anthropic)

Claude Code a nástroje Claude Agent SDK se připojují přes endpoint `/v1/messages` kompatibilní s Anthropic.

```bash
# ANTHROPIC_BASE_URL je KOŘENOVÁ adresa (bez /v1) — CLI si samo připojí /v1/messages.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# Oficiální CLI preferuje ANTHROPIC_API_KEY; pro jistotu nastavte oba.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ **Nedávejte** `/v1` do `ANTHROPIC_BASE_URL` — vznikne z toho `/v1/v1/messages` a selže to. Volání nástrojů i streamování fungují od začátku do konce, i když jsou směrována na modely kompatibilní s OpenAI.

### Codex CLI (Responses API)

Codex se připojuje přes OpenAI Responses API (`/v1/responses`); cesta Chat Completions byla z Codexu odstraněna v únoru 2026.

```toml
# ~/.codex/config.toml
# model / model_provider jsou klíče na úrovni kořene dokumentu (musí být nad [table]).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex si připojí /responses → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex podporuje pouze Responses API
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
// opencode.json   (nebo: /connect → Other)
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

# Goose / OpenHands: ID modelu opatřete předponou openai/
#   model = openai/gpt-4.1
```

### Gemini CLI

Upstream Gemini CLI má slabou podporu pro externí endpointy kompatibilní s OpenAI; možná budete potřebovat wrapper nebo fork kompatibilní s OpenAI.

---

## 🖥 IDE / GUI agenti

### Cline · Roo Code · Kilo Code · Cursor

Vyberte **OpenAI Compatible** (nebo **Custom OpenAI**) jako poskytovatele a vložte:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Vždy použijte **slot OpenAI Compatible** — vyhrazený záznam pro OpenRouter je napevno nastaven na openrouter.ai a selže. **Cursor** vyžaduje `/v1` v základní URL adrese a neprázdné pole klíče. **Kilo Code** má známý problém (#681), kdy se vlastní základní URL adresa nepředává do výpisu modelů — zadejte ID modelu ručně.

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

S nastavením `model: AUTODETECT` si Continue seznam modelů stáhne automaticky.

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

Názvy polí se mohou lišit podle verze Zed — ověřte v dokumentaci Zed.

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
    base_url="https://router.pleum.ai",   # kořen, bez /v1 — SDK si připojí /v1/messages
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # funguje jakýkoli model PleumRouter
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Multimodální — obraz · zvuk · video

Všechny modality jsou HTTP endpointy kompatibilní s OpenAI na stejném klíči. Vyberte model, který danou modalitu podporuje, z [`GET /v1/models`](https://pleum.ai/models).

```bash
# Generování obrázků
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Převod textu na řeč (vrací zvukové bajty; náklady v hlavičce X-Cost-Krw)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Převod řeči na text (multipart upload)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# Generování videa je asynchronní: POST vrátí job_id, poté sledujte GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### Rozhraní API

| Endpoint | Protokol |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (streamování, nástroje, vidění) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Generování obrázků |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Asynchronní video |
| `GET /v1/models` | Katalog modelů (veřejný) |
| `GET /v1/credits` | Zůstatek |

---

## 🔌 Další agenti

Většina agentů, kteří zde nejsou uvedeni, funguje stejným způsobem — nastavte základní URL adresu kompatibilní s OpenAI:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** a další.

Přes endpoint `/v1/messages` kompatibilní s Anthropic: **claude-code-router** se rovněž připojuje pomocí `ANTHROPIC_BASE_URL`.

**ID modelů**: najdete je na `GET /v1/models` nebo na [stránce s modely](https://pleum.ai/models). Cline, Continue, OpenCode a další si seznam stahují automaticky. ID ve formátu OpenRouter (`openai/gpt-5.5`) se převádějí automaticky.

**LiteLLM proxy** (Aider, OpenHands, Open Interpreter, SWE-agent a gptme jsou založené na LiteLLM a připojují se přímo — ale pokud používáte LiteLLM proxy):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # předpona openai/ → route kompatibilní s OpenAI
      api_base: https://router.pleum.ai/v1           # NEpřipojujte /chat/completions
      api_key: os.environ/PLEUM_API_KEY
```

---

## Přispívání

Podařilo se vám rozjet PleumRouter s nástrojem, který zde není uveden? Uvítáme PR — přidejte sekci s **otestovaným** konfiguračním úryvkem (základní URL adresa, proměnná prostředí pro klíč, formát ID modelu a případné háčky).

## Licence

[MIT](LICENSE)
