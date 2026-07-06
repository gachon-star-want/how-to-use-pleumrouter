<div align="center">

# Cara menggunakan PleumRouter

**Satu kunci API untuk 200+ model AI — serasi OpenAI, dibilkan dalam KRW.**

[Laman Web](https://pleum.ai) · [Dokumen](https://pleum.ai/docs) · [Model](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · Bahasa Melayu · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter ialah get laluan AI (AI gateway): satu kunci (`plm_…`), satu URL asas, 210+ model daripada 18 penyedia — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE dan banyak lagi. Ia menyokong **OpenAI Chat Completions**, **Anthropic Messages**, dan **OpenAI Responses**, jadi hampir semua ejen pengekodan, plugin IDE, dan SDK dapat disambungkan hanya dengan satu baris perubahan konfigurasi. Teks, embedding, imej, pertuturan dan video semuanya berjalan melalui kunci yang sama.

Repo ini mengumpulkan **resipi integrasi yang telah disahkan**. Setiap petikan kod di bawah telah diuji terhadap get laluan (gateway) langsung.

## Bermula

1. [Daftar](https://pleum.ai/signup) → Dashboard → **API Keys** → keluarkan satu kunci (bermula dengan `plm_`).
2. Arahkan alat anda ke URL asas:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Some agents (OpenCode, Crush) read PLEUM_API_KEY — same key, set both.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Uji ringkas (smoke test):

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Anda mendapat kredit percuma ₩1,000 semasa mendaftar dan bonus ₩5,000 pada pengecasan semula (top-up) pertama anda.

## Integrasi

| Kategori | Alat |
|---|---|
| [⚡ Pelancar satu-arahan](#-pleum-cli--laluan-pantas) | CLI `pleum` |
| [🤖 Ejen pengekodan terminal](#-ejen-terminal--cli) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 Ejen IDE / GUI](#-ejen-ide--gui) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK](#-sdk) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 API Multimodal](#-multimodal--imej--audio--video) | Imej, TTS, STT, Video, Embedding |
| [🔌 Selain itu](#-lebih-banyak-ejen) | ID gaya OpenRouter, proksi LiteLLM, 15+ ejen lain |

---

## ⚡ pleum CLI — laluan pantas

CLI rasmi ini melancarkan ejen kegemaran anda yang sudah tersambung terus ke PleumRouter. Tiada fail konfigurasi disentuh.

```bash
npm install -g pleumrouter        # or: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # browser login, key auto-issued & saved
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # terminal chat REPL
pleum models                      # list all models with pricing
```

Disokong untuk pelancaran automatik: `claude` · `aider` · `codex` · `goose` · `openhands` (ditambah petikan konfigurasi untuk `opencode` · `crush`). Konfigurasi alat sedia ada anda tidak pernah diubah suai.

---

## 🤖 Ejen Terminal / CLI

### Claude Code (serasi Anthropic)

Claude Code dan alat Claude Agent SDK bersambung melalui titik akhir (endpoint) `/v1/messages` yang serasi Anthropic.

```bash
# ANTHROPIC_BASE_URL is the ROOT (no /v1) — the CLI appends /v1/messages itself.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# The official CLI prefers ANTHROPIC_API_KEY; set both to be safe.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ **Jangan** letakkan `/v1` dalam `ANTHROPIC_BASE_URL` — ia akan menjadi `/v1/v1/messages` dan gagal. Panggilan alat (tool calls) dan penstriman (streaming) berfungsi sepenuhnya hujung ke hujung, walaupun dilaluikan ke model serasi OpenAI.

### Codex CLI (Responses API)

Codex bersambung melalui OpenAI Responses API (`/v1/responses`); laluan Chat Completions telah dibuang daripada Codex pada Februari 2026.

```toml
# ~/.codex/config.toml
# model / model_provider are document-root keys (must be above the [table]).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex appends /responses → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex supports only the Responses API
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
// opencode.json   (or: /connect → Other)
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

# Goose / OpenHands: prefix the model id with openai/
#   model = openai/gpt-4.1
```

### Gemini CLI

Gemini CLI hulu (upstream) mempunyai sokongan yang lemah untuk titik akhir luaran yang serasi OpenAI; anda mungkin memerlukan pembungkus (wrapper) atau fork yang serasi OpenAI.

---

## 🖥 Ejen IDE / GUI

### Cline · Roo Code · Kilo Code · Cursor

Pilih **OpenAI Compatible** (atau **Custom OpenAI**) sebagai penyedia dan tampal:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Sentiasa gunakan **slot OpenAI Compatible** — entri OpenRouter khusus telah dikodkan-keras (hardcoded) kepada openrouter.ai dan akan gagal. **Cursor** memerlukan `/v1` dalam URL asas dan medan kunci yang tidak kosong. **Kilo Code** mempunyai isu yang diketahui (#681) di mana URL asas tersuai tidak dihantar ke penyenaraian model — masukkan ID model secara manual.

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

Dengan `model: AUTODETECT`, Continue menarik senarai model secara automatik.

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

Nama medan boleh berbeza mengikut versi Zed — semak dokumen Zed.

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
    base_url="https://router.pleum.ai",   # root, no /v1 — SDK appends /v1/messages
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # any PleumRouter model works
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Multimodal — imej · audio · video

Semua modaliti adalah titik akhir HTTP yang serasi OpenAI pada kunci yang sama. Pilih model yang menyokong modaliti tersebut daripada [`GET /v1/models`](https://pleum.ai/models).

```bash
# Image generation
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Text-to-speech (returns audio bytes; cost in X-Cost-Krw header)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Speech-to-text (multipart upload)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# Video generation is async: POST returns a job_id, then poll GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### Permukaan API

| Titik Akhir | Protokol |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (penstriman, alat, penglihatan) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Penjanaan imej |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Video tak segerak (async) |
| `GET /v1/models` | Katalog model (awam) |
| `GET /v1/credits` | Baki |

---

## 🔌 Lebih banyak ejen

Kebanyakan ejen yang tidak disenaraikan di sini berfungsi dengan cara yang sama — tetapkan URL asas yang serasi OpenAI:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** dan banyak lagi.

Melalui `/v1/messages` yang serasi Anthropic: **claude-code-router** juga bersambung dengan `ANTHROPIC_BASE_URL`.

**ID Model**: cari di `GET /v1/models` atau di [halaman model](https://pleum.ai/models). Cline, Continue, OpenCode dan lain-lain menarik senarai secara automatik. ID format OpenRouter (`openai/gpt-5.5`) ditukar secara automatik.

**Proksi LiteLLM** (Aider, OpenHands, Open Interpreter, SWE-agent dan gptme adalah berasaskan LiteLLM dan bersambung terus — tetapi jika anda mengekalkan proksi LiteLLM):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # openai/ prefix → OpenAI-compat route
      api_base: https://router.pleum.ai/v1           # do NOT append /chat/completions
      api_key: os.environ/PLEUM_API_KEY
```

---

## Sumbangan

Berjaya menjalankan PleumRouter dengan alat yang tidak disenaraikan di sini? PR dialu-alukan — tambah satu seksyen dengan petikan konfigurasi yang **telah diuji** (URL asas, env kunci, format ID model, dan sebarang perangkap/isu).

## Lesen

[MIT](LICENSE)
