<div align="center">

# Jak korzystać z PleumRouter

**Jeden klucz API dla ponad 200 modeli AI — kompatybilny z OpenAI, rozliczany w KRW.**

[Strona internetowa](https://pleum.ai) · [Dokumentacja](https://pleum.ai/docs) · [Modele](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · Polski · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter to bramka AI (AI gateway): jeden klucz (`plm_…`), jeden adres bazowy URL, ponad 210 modeli od 18 dostawców — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE i inne. Obsługuje **OpenAI Chat Completions**, **Anthropic Messages** oraz **OpenAI Responses**, dzięki czemu niemal każdy agent kodujący, wtyczka IDE i SDK łączy się po zmianie jednej linijki konfiguracji. Tekst, embeddingi, obraz, mowa i wideo — wszystko działa przez ten sam klucz.

To repozytorium zbiera **zweryfikowane przepisy integracyjne**. Każdy poniższy fragment kodu jest testowany na żywej bramce.

## Pierwsze kroki

1. [Zarejestruj się](https://pleum.ai/signup) → Panel → **API Keys** → wygeneruj klucz (zaczyna się od `plm_`).
2. Skieruj swoje narzędzie na adres bazowy URL:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Niektórzy agenci (OpenCode, Crush) czytają PLEUM_API_KEY — ten sam klucz, ustaw oba.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Test dymny:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Przy rejestracji otrzymujesz ₩1000 darmowego kredytu, a przy pierwszym doładowaniu bonus ₩5000.

## Integracje

| Kategoria | Narzędzia |
|---|---|
| [⚡ Launcher jednym poleceniem](#-pleum-cli--najszybsza-ścieżka) | CLI `pleum` |
| [🤖 Terminalowi agenci kodujący](#-agenci-terminalowi--cli) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 Agenci IDE / GUI](#-agenci-ide--gui) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK](#-sdk) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 API multimodalne](#-multimodalność--obraz--audio--wideo) | Obrazy, TTS, STT, wideo, embeddingi |
| [🔌 Wszystko inne](#-pozostali-agenci) | ID w stylu OpenRouter, proxy LiteLLM, ponad 15 innych agentów |

---

## ⚡ pleum CLI — najszybsza ścieżka

Oficjalne CLI uruchamia Twojego ulubionego agenta już podłączonego do PleumRouter. Żadne pliki konfiguracyjne nie są ruszane.

```bash
npm install -g pleumrouter        # lub: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # logowanie przez przeglądarkę, klucz wydawany i zapisywany automatycznie
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # terminalowy REPL czatu
pleum models                      # lista wszystkich modeli z cennikiem
```

Automatyczne uruchamianie obsługiwane dla: `claude` · `aider` · `codex` · `goose` · `openhands` (a także fragmenty konfiguracji dla `opencode` · `crush`). Twoje istniejące konfiguracje narzędzi nigdy nie są modyfikowane.

---

## 🤖 Agenci terminalowi / CLI

### Claude Code (kompatybilny z Anthropic)

Claude Code i narzędzia Claude Agent SDK łączą się przez endpoint `/v1/messages` kompatybilny z Anthropic.

```bash
# ANTHROPIC_BASE_URL to adres GŁÓWNY (bez /v1) — CLI samo dołącza /v1/messages.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# Oficjalne CLI preferuje ANTHROPIC_API_KEY; dla pewności ustaw oba.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ **Nie** umieszczaj `/v1` w `ANTHROPIC_BASE_URL` — powstaje wtedy `/v1/v1/messages`, co kończy się błędem. Wywołania narzędzi (tool calls) i streaming działają od początku do końca, nawet gdy zapytanie trafia do modeli kompatybilnych z OpenAI.

### Codex CLI (Responses API)

Codex łączy się przez OpenAI Responses API (`/v1/responses`); ścieżka Chat Completions została usunięta z Codex w lutym 2026.

```toml
# ~/.codex/config.toml
# model / model_provider to klucze na poziomie głównym dokumentu (muszą być nad [tabelą]).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex dołącza /responses → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex obsługuje wyłącznie Responses API
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
// opencode.json   (lub: /connect → Other)
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

# Goose / OpenHands: poprzedź ID modelu prefiksem openai/
#   model = openai/gpt-4.1
```

### Gemini CLI

Oficjalne (upstream) Gemini CLI ma słabe wsparcie dla zewnętrznych endpointów kompatybilnych z OpenAI; może być potrzebny wrapper lub fork kompatybilny z OpenAI.

---

## 🖥 Agenci IDE / GUI

### Cline · Roo Code · Kilo Code · Cursor

Wybierz **OpenAI Compatible** (lub **Custom OpenAI**) jako dostawcę i wklej:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Zawsze używaj slotu **OpenAI Compatible** — dedykowany wpis OpenRouter ma na stałe zakodowany adres openrouter.ai i zawiedzie. **Cursor** wymaga `/v1` w adresie bazowym URL oraz niepustego pola klucza. **Kilo Code** ma znany błąd (#681), gdzie niestandardowy adres bazowy URL nie jest przekazywany do listowania modeli — wpisz ID modelu ręcznie.

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

Przy `model: AUTODETECT` Continue automatycznie pobiera listę modeli.

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

Nazwy pól mogą się różnić w zależności od wersji Zed — sprawdź dokumentację Zed.

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
    base_url="https://router.pleum.ai",   # adres główny, bez /v1 — SDK dołącza /v1/messages
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # działa dowolny model PleumRouter
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Multimodalność — obraz · audio · wideo

Wszystkie modalności to endpointy HTTP kompatybilne z OpenAI, dostępne pod tym samym kluczem. Wybierz model obsługujący daną modalność z [`GET /v1/models`](https://pleum.ai/models).

```bash
# Generowanie obrazu
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Zamiana tekstu na mowę (zwraca bajty audio; koszt w nagłówku X-Cost-Krw)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Zamiana mowy na tekst (przesyłanie multipart)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# Generowanie wideo jest asynchroniczne: POST zwraca job_id, następnie odpytuj GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### Powierzchnia API

| Endpoint | Protokół |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (streaming, narzędzia, wizja) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Generowanie obrazów |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Asynchroniczne wideo |
| `GET /v1/models` | Katalog modeli (publiczny) |
| `GET /v1/credits` | Saldo |

---

## 🔌 Pozostali agenci

Większość agentów niewymienionych tutaj działa w ten sam sposób — wystarczy ustawić adres bazowy URL kompatybilny z OpenAI:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** i inne.

Przez kompatybilny z Anthropic `/v1/messages`: **claude-code-router** również łączy się za pomocą `ANTHROPIC_BASE_URL`.

**ID modeli**: znajdziesz je pod `GET /v1/models` lub na [stronie modeli](https://pleum.ai/models). Cline, Continue, OpenCode i inne pobierają listę automatycznie. ID w formacie OpenRouter (`openai/gpt-5.5`) są konwertowane automatycznie.

**Proxy LiteLLM** (Aider, OpenHands, Open Interpreter, SWE-agent i gptme są oparte na LiteLLM i łączą się bezpośrednio — ale jeśli utrzymujesz proxy LiteLLM):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # prefiks openai/ → trasa kompatybilna z OpenAI
      api_base: https://router.pleum.ai/v1           # NIE dołączaj /chat/completions
      api_key: os.environ/PLEUM_API_KEY
```

---

## Współpraca

Udało Ci się uruchomić PleumRouter z narzędziem, którego nie ma na tej liście? Zapraszamy do PR-ów — dodaj sekcję z **przetestowanym** fragmentem konfiguracji (adres bazowy URL, zmienna środowiskowa klucza, format ID modelu i wszelkie pułapki).

## Licencja

[MIT](LICENSE)
