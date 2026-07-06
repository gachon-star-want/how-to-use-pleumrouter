<div align="center">

# Cara menggunakan PleumRouter

**Satu kunci API untuk 200+ model AI — kompatibel OpenAI, ditagih dalam KRW.**

[Website](https://pleum.ai) · [Dokumentasi](https://pleum.ai/docs) · [Model](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · Bahasa Indonesia · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter adalah gateway AI: satu kunci (`plm_…`), satu base URL, 210+ model dari 18 penyedia — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE, dan lainnya. Layanan ini mendukung **OpenAI Chat Completions**, **Anthropic Messages**, dan **OpenAI Responses**, sehingga hampir semua agen coding, plugin IDE, dan SDK dapat terhubung hanya dengan mengubah satu baris konfigurasi. Teks, embedding, gambar, suara, dan video semuanya berjalan melalui kunci yang sama.

Repo ini mengumpulkan **resep integrasi yang telah diverifikasi**. Setiap cuplikan kode di bawah telah diuji terhadap gateway langsung (live).

## Memulai

1. [Daftar](https://pleum.ai/signup) → Dashboard → **API Keys** → terbitkan kunci (dimulai dengan `plm_`).
2. Arahkan tool Anda ke base URL:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Beberapa agen (OpenCode, Crush) membaca PLEUM_API_KEY — kunci yang sama, set keduanya.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Uji cepat (smoke test):

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Anda mendapatkan kredit gratis ₩1.000 saat mendaftar dan bonus ₩5.000 pada top-up pertama Anda.

## Integrasi

| Kategori | Tools |
|---|---|
| [⚡ Peluncur satu perintah](#-pleum-cli--jalur-cepat) | CLI `pleum` |
| [🤖 Agen coding terminal](#-agen-terminal--cli) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 Agen IDE / GUI](#-agen-ide--gui) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK](#-sdk) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 API Multimodal](#-multimodal--gambar--audio--video) | Gambar, TTS, STT, Video, Embedding |
| [🔌 Lainnya](#-agen-lainnya) | ID gaya OpenRouter, proxy LiteLLM, 15+ agen lainnya |

---

## ⚡ pleum CLI — jalur cepat

CLI resmi meluncurkan agen favorit Anda yang sudah terhubung langsung ke PleumRouter. Tidak ada file konfigurasi yang perlu disentuh.

```bash
npm install -g pleumrouter        # atau: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # login via browser, kunci diterbitkan & disimpan otomatis
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # REPL chat terminal
pleum models                      # daftar semua model beserta harganya
```

Didukung untuk peluncuran otomatis: `claude` · `aider` · `codex` · `goose` · `openhands` (ditambah cuplikan konfigurasi untuk `opencode` · `crush`). Konfigurasi tool Anda yang sudah ada tidak akan pernah dimodifikasi.

---

## 🤖 Agen terminal / CLI

### Claude Code (kompatibel Anthropic)

Claude Code dan tools Claude Agent SDK terhubung melalui endpoint `/v1/messages` yang kompatibel dengan Anthropic.

```bash
# ANTHROPIC_BASE_URL adalah ROOT (tanpa /v1) — CLI menambahkan /v1/messages sendiri.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# CLI resmi lebih memilih ANTHROPIC_API_KEY; set keduanya agar aman.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ **Jangan** menambahkan `/v1` di `ANTHROPIC_BASE_URL` — ini akan menjadi `/v1/v1/messages` dan gagal. Pemanggilan tool dan streaming berjalan end-to-end, bahkan ketika diarahkan ke model yang kompatibel OpenAI.

### Codex CLI (Responses API)

Codex terhubung melalui OpenAI Responses API (`/v1/responses`); jalur Chat Completions telah dihapus dari Codex sejak Februari 2026.

```toml
# ~/.codex/config.toml
# model / model_provider adalah kunci document-root (harus berada di atas [table]).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex menambahkan /responses → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex hanya mendukung Responses API
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
// opencode.json   (atau: /connect → Other)
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

# Goose / OpenHands: beri prefix openai/ pada model id
#   model = openai/gpt-4.1
```

### Gemini CLI

Gemini CLI upstream memiliki dukungan yang lemah untuk endpoint eksternal yang kompatibel dengan OpenAI; Anda mungkin memerlukan wrapper atau fork yang kompatibel dengan OpenAI.

---

## 🖥 Agen IDE / GUI

### Cline · Roo Code · Kilo Code · Cursor

Pilih **OpenAI Compatible** (atau **Custom OpenAI**) sebagai provider, lalu tempelkan:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Selalu gunakan **slot OpenAI Compatible** — entri OpenRouter khusus sudah di-hardcode ke openrouter.ai dan akan gagal. **Cursor** mengharuskan `/v1` ada di base URL dan kolom kunci tidak boleh kosong. **Kilo Code** memiliki masalah yang sudah diketahui (#681) di mana base URL kustom tidak diteruskan ke pendaftaran model — masukkan model ID secara manual.

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

Dengan `model: AUTODETECT`, Continue akan menarik daftar model secara otomatis.

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

Nama field bisa berbeda tergantung versi Zed — periksa dokumentasi Zed.

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
    base_url="https://router.pleum.ai",   # root, tanpa /v1 — SDK menambahkan /v1/messages
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # model PleumRouter apa pun berfungsi
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Multimodal — gambar · audio · video

Semua modalitas adalah endpoint HTTP yang kompatibel dengan OpenAI, menggunakan kunci yang sama. Pilih model yang mendukung modalitas tersebut dari [`GET /v1/models`](https://pleum.ai/models).

```bash
# Pembuatan gambar
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Text-to-speech (mengembalikan byte audio; biaya ada di header X-Cost-Krw)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Speech-to-text (upload multipart)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# Pembuatan video bersifat async: POST mengembalikan job_id, lalu poll GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### Permukaan API

| Endpoint | Protokol |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (streaming, tools, vision) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Pembuatan gambar |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Video async |
| `GET /v1/models` | Katalog model (publik) |
| `GET /v1/credits` | Saldo |

---

## 🔌 Agen lainnya

Sebagian besar agen yang tidak tercantum di sini bekerja dengan cara yang sama — set base URL yang kompatibel dengan OpenAI:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** dan lainnya.

Melalui `/v1/messages` yang kompatibel dengan Anthropic: **claude-code-router** juga terhubung dengan `ANTHROPIC_BASE_URL`.

**Model ID**: temukan di `GET /v1/models` atau di [halaman model](https://pleum.ai/models). Cline, Continue, OpenCode, dan lainnya mengambil daftar tersebut secara otomatis. ID berformat OpenRouter (`openai/gpt-5.5`) dikonversi secara otomatis.

**Proxy LiteLLM** (Aider, OpenHands, Open Interpreter, SWE-agent, dan gptme berbasis LiteLLM dan terhubung langsung — tetapi jika Anda tetap menggunakan proxy LiteLLM):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # prefix openai/ → rute OpenAI-compat
      api_base: https://router.pleum.ai/v1           # JANGAN tambahkan /chat/completions
      api_key: os.environ/PLEUM_API_KEY
```

---

## Berkontribusi

Berhasil menjalankan PleumRouter dengan tool yang belum tercantum di sini? PR sangat diterima — tambahkan bagian dengan cuplikan konfigurasi yang **telah diuji** (base URL, env kunci, format model ID, dan hal-hal yang perlu diperhatikan).

## Lisensi

[MIT](LICENSE)
