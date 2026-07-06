<div align="center">

# So verwendest du PleumRouter

**Ein API-Schlüssel für 200+ KI-Modelle — OpenAI-kompatibel, abgerechnet in KRW.**

[Website](https://pleum.ai) · [Docs](https://pleum.ai/docs) · [Modelle](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · Deutsch · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter ist ein KI-Gateway: ein Schlüssel (`plm_…`), eine Basis-URL, 210+ Modelle von 18 Anbietern — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE und mehr. Es unterstützt **OpenAI Chat Completions**, **Anthropic Messages** und **OpenAI Responses**, sodass sich fast jeder Coding-Agent, jedes IDE-Plugin und jedes SDK mit einer einzigen Konfigurationszeile verbinden lässt. Text, Embeddings, Bild, Sprache und Video laufen alle über denselben Schlüssel.

Dieses Repo sammelt **verifizierte Integrations-Rezepte**. Jeder Codeausschnitt unten wurde gegen das Live-Gateway getestet.

## Erste Schritte

1. [Registrieren](https://pleum.ai/signup) → Dashboard → **API Keys** → einen Schlüssel ausstellen (beginnt mit `plm_`).
2. Richte dein Tool auf die Basis-URL:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Manche Agenten (OpenCode, Crush) lesen PLEUM_API_KEY — derselbe Schlüssel, beide setzen.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Funktionstest:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Bei der Registrierung erhältst du ₩1.000 Startguthaben und bei der ersten Aufladung einen Bonus von ₩5.000.

## Integrationen

| Kategorie | Tools |
|---|---|
| [⚡ Ein-Kommando-Starter](#-pleum-cli--der-schnelle-weg) | `pleum` CLI |
| [🤖 Terminal-Coding-Agenten](#-terminal--cli-agenten) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE-/GUI-Agenten](#-ide--gui-agenten) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDKs](#-sdks) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 Multimodale API](#-multimodal--bild--audio--video) | Bilder, TTS, STT, Video, Embeddings |
| [🔌 Alles andere](#-weitere-agenten) | OpenRouter-artige IDs, LiteLLM-Proxy, 15+ weitere Agenten |

---

## ⚡ pleum CLI — der schnelle Weg

Die offizielle CLI startet deinen bevorzugten Agenten bereits vorkonfiguriert mit PleumRouter. Keine Konfigurationsdateien werden angefasst.

```bash
npm install -g pleumrouter        # oder: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # Browser-Login, Schlüssel wird automatisch ausgestellt & gespeichert
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # Terminal-Chat-REPL
pleum models                      # alle Modelle mit Preisen auflisten
```

Unterstützt für Auto-Start: `claude` · `aider` · `codex` · `goose` · `openhands` (plus Konfigurations-Snippets für `opencode` · `crush`). Deine bestehenden Tool-Konfigurationen werden nie verändert.

---

## 🤖 Terminal / CLI-Agenten

### Claude Code (Anthropic-kompatibel)

Claude Code und die Claude Agent SDK-Tools verbinden sich über den Anthropic-kompatiblen `/v1/messages`-Endpunkt.

```bash
# ANTHROPIC_BASE_URL ist die WURZEL (ohne /v1) — die CLI hängt /v1/messages selbst an.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# Die offizielle CLI bevorzugt ANTHROPIC_API_KEY; setze sicherheitshalber beide.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ Füge **kein** `/v1` in `ANTHROPIC_BASE_URL` ein — daraus wird `/v1/v1/messages`, was fehlschlägt. Tool-Aufrufe und Streaming funktionieren durchgängig, auch wenn zu OpenAI-kompatiblen Modellen geroutet wird.

### Codex CLI (Responses API)

Codex verbindet sich über die OpenAI Responses API (`/v1/responses`); der Chat-Completions-Pfad wurde im Februar 2026 aus Codex entfernt.

```toml
# ~/.codex/config.toml
# model / model_provider sind Document-Root-Keys (müssen über der [table] stehen).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex hängt /responses an → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex unterstützt nur die Responses API
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
// opencode.json   (oder: /connect → Other)
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

# Goose / OpenHands: der Modell-ID das Präfix openai/ voranstellen
#   model = openai/gpt-4.1
```

### Gemini CLI

Die Upstream-Gemini-CLI hat nur schwache Unterstützung für externe OpenAI-kompatible Endpunkte; möglicherweise benötigst du einen OpenAI-kompatiblen Wrapper oder Fork.

---

## 🖥 IDE-/GUI-Agenten

### Cline · Roo Code · Kilo Code · Cursor

Wähle **OpenAI Compatible** (oder **Custom OpenAI**) als Provider und füge ein:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Verwende immer den **OpenAI-Compatible-Slot** — der dedizierte OpenRouter-Eintrag ist fest auf openrouter.ai verdrahtet und schlägt fehl. **Cursor** benötigt `/v1` in der Basis-URL und ein nicht leeres Schlüsselfeld. **Kilo Code** hat ein bekanntes Problem (#681), bei dem die benutzerdefinierte Basis-URL nicht an die Modellauflistung übergeben wird — gib die Modell-ID manuell ein.

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

Mit `model: AUTODETECT` ruft Continue die Modellliste automatisch ab.

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

Feldnamen können je nach Zed-Version variieren — sieh in der Zed-Dokumentation nach.

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
    base_url="https://router.pleum.ai",   # Wurzel, ohne /v1 — SDK hängt /v1/messages an
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # jedes PleumRouter-Modell funktioniert
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Multimodal — Bild · Audio · Video

Alle Modalitäten sind OpenAI-kompatible HTTP-Endpunkte mit demselben Schlüssel. Wähle unter [`GET /v1/models`](https://pleum.ai/models) ein Modell, das die Modalität unterstützt.

```bash
# Bilderzeugung
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Text-zu-Sprache (liefert Audio-Bytes zurück; Kosten im X-Cost-Krw-Header)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Sprache-zu-Text (Multipart-Upload)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# Videoerzeugung ist asynchron: POST liefert eine job_id, dann per Polling GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### API-Oberfläche

| Endpunkt | Protokoll |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (Streaming, Tools, Vision) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Bilderzeugung |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Asynchrones Video |
| `GET /v1/models` | Modellkatalog (öffentlich) |
| `GET /v1/credits` | Guthaben |

---

## 🔌 Weitere Agenten

Die meisten hier nicht aufgeführten Agenten funktionieren auf die gleiche Weise — setze die OpenAI-kompatible Basis-URL:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** und weitere.

Über das Anthropic-kompatible `/v1/messages`: **claude-code-router** verbindet sich ebenfalls mit `ANTHROPIC_BASE_URL`.

**Modell-IDs**: findest du unter `GET /v1/models` oder auf der [Modellseite](https://pleum.ai/models). Cline, Continue, OpenCode und andere rufen die Liste automatisch ab. IDs im OpenRouter-Format (`openai/gpt-5.5`) werden automatisch umgewandelt.

**LiteLLM-Proxy** (Aider, OpenHands, Open Interpreter, SWE-agent und gptme basieren auf LiteLLM und verbinden sich direkt — falls du jedoch einen LiteLLM-Proxy betreibst):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # openai/-Präfix → OpenAI-Compat-Route
      api_base: https://router.pleum.ai/v1           # NICHT /chat/completions anhängen
      api_key: os.environ/PLEUM_API_KEY
```

---

## Mitwirken

Hast du PleumRouter mit einem hier nicht aufgeführten Tool zum Laufen gebracht? PRs sind willkommen — füge einen Abschnitt mit einem **getesteten** Konfigurations-Snippet hinzu (Basis-URL, Schlüssel-Env, Modell-ID-Format und etwaige Fallstricke).

## Lizenz

[MIT](LICENSE)
