<div align="center">

# PleumRouter Nasıl Kullanılır

**200+ yapay zeka modeli için tek API anahtarı — OpenAI uyumlu, KRW olarak faturalandırılır.**

[Web Sitesi](https://pleum.ai) · [Belgeler](https://pleum.ai/docs) · [Modeller](https://pleum.ai/models) · [Oyun Alanı](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · Türkçe · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter bir yapay zeka ağ geçididir: tek anahtar (`plm_…`), tek temel URL, 18 sağlayıcıdan 210+ model — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE ve daha fazlası. **OpenAI Chat Completions**, **Anthropic Messages** ve **OpenAI Responses** protokollerini konuşur, bu yüzden neredeyse her kodlama ajanı, IDE eklentisi ve SDK tek satırlık bir yapılandırma değişikliğiyle bağlanır. Metin, gömme (embedding), görsel, ses ve video hepsi aynı anahtar üzerinden çalışır.

Bu depo **doğrulanmış entegrasyon tariflerini** bir araya getirir. Aşağıdaki her kod parçası canlı ağ geçidine karşı test edilmiştir.

## Başlarken

1. [Kaydolun](https://pleum.ai/signup) → Kontrol Paneli → **API Anahtarları** → bir anahtar oluşturun (`plm_` ile başlar).
2. Aracınızı temel URL'ye yönlendirin:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Bazı ajanlar (OpenCode, Crush) PLEUM_API_KEY okur — aynı anahtar, ikisini de ayarlayın.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Duman testi:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Kayıt olduğunuzda ₩1.000 ücretsiz kredi ve ilk bakiye yüklemenizde ₩5.000 bonus kazanırsınız.

## Entegrasyonlar

| Kategori | Araçlar |
|---|---|
| [⚡ Tek komutla başlatıcı](#-pleum-cli--hızlı-yol) | `pleum` CLI |
| [🤖 Terminal kodlama ajanları](#-terminal--cli-ajanları) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE / GUI ajanları](#-ide--gui-ajanları) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK'lar](#-sdklar) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 Çok modlu API](#-çok-modlu--görsel--ses--video) | Görseller, TTS, STT, Video, Gömmeler (Embeddings) |
| [🔌 Diğer her şey](#-diğer-ajanlar) | OpenRouter tarzı ID'ler, LiteLLM proxy, 15+ ek ajan |

---

## ⚡ pleum CLI — hızlı yol

Resmi CLI, favori ajanınızı zaten PleumRouter'a bağlı olarak başlatır. Hiçbir yapılandırma dosyasına dokunulmaz.

```bash
npm install -g pleumrouter        # veya: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # tarayıcı üzerinden giriş, anahtar otomatik oluşturulup kaydedilir
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # terminal sohbet REPL'i
pleum models                      # fiyatlandırmayla birlikte tüm modelleri listele
```

Otomatik başlatma için desteklenenler: `claude` · `aider` · `codex` · `goose` · `openhands` (ayrıca `opencode` · `crush` için yapılandırma kod parçaları da mevcut). Mevcut araç yapılandırmalarınız asla değiştirilmez.

---

## 🤖 Terminal / CLI ajanları

### Claude Code (Anthropic uyumlu)

Claude Code ve Claude Agent SDK araçları, Anthropic uyumlu `/v1/messages` uç noktası üzerinden bağlanır.

```bash
# ANTHROPIC_BASE_URL KÖK adrestir (sonunda /v1 yok) — CLI /v1/messages kısmını kendisi ekler.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# Resmi CLI, ANTHROPIC_API_KEY'i tercih eder; güvenli olması için ikisini de ayarlayın.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ `ANTHROPIC_BASE_URL` içine **kesinlikle** `/v1` koymayın — `/v1/v1/messages` haline gelir ve başarısız olur. Araç çağrıları ve akış (streaming), OpenAI uyumlu modellere yönlendirildiğinde bile uçtan uca çalışır.

### Codex CLI (Responses API)

Codex, OpenAI Responses API'si (`/v1/responses`) üzerinden bağlanır; Chat Completions yolu Şubat 2026'da Codex'ten kaldırılmıştır.

```toml
# ~/.codex/config.toml
# model / model_provider belge kökü anahtarlarıdır (mutlaka [table] üzerinde yer almalı).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex /responses ekler → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex yalnızca Responses API'sini destekler
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
// opencode.json   (veya: /connect → Other)
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

# Goose / OpenHands: model kimliğinin önüne openai/ önekini ekleyin
#   model = openai/gpt-4.1
```

### Gemini CLI

Yukarı akış (upstream) Gemini CLI, harici OpenAI uyumlu uç noktalar için zayıf destek sunar; bir OpenAI uyumlu sarmalayıcıya veya çatallanmış (fork) sürüme ihtiyacınız olabilir.

---

## 🖥 IDE / GUI ajanları

### Cline · Roo Code · Kilo Code · Cursor

Sağlayıcı olarak **OpenAI Compatible** (veya **Custom OpenAI**) seçeneğini seçin ve şunu yapıştırın:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Her zaman **OpenAI Compatible yuvasını** kullanın — özel OpenRouter girişi openrouter.ai'ye sabit kodlanmıştır (hardcoded) ve başarısız olur. **Cursor**, temel URL'de `/v1` ve boş olmayan bir anahtar alanı gerektirir. **Kilo Code**'da bilinen bir sorun vardır (#681): özel temel URL, model listelemeye aktarılmaz — model kimliğini manuel olarak girin.

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

`model: AUTODETECT` ile Continue, model listesini otomatik olarak çeker.

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

Alan adları Zed sürümüne göre değişebilir — Zed belgelerini kontrol edin.

---

## 📦 SDK'lar

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
    base_url="https://router.pleum.ai",   # kök, /v1 yok — SDK /v1/messages ekler
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # herhangi bir PleumRouter modeli çalışır
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Çok modlu — görsel · ses · video

Tüm modlar, aynı anahtar üzerinde OpenAI uyumlu HTTP uç noktalarıdır. [`GET /v1/models`](https://pleum.ai/models) üzerinden ilgili modu destekleyen bir model seçin.

```bash
# Görsel oluşturma
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Metinden konuşmaya (ses baytlarını döndürür; maliyet X-Cost-Krw başlığında)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Konuşmadan metne (çok parçalı yükleme)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# Video oluşturma asenkrondur: POST bir job_id döndürür, ardından GET /v1/jobs/{job_id} ile sorgulayın
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### API yüzeyi

| Uç Nokta | Protokol |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (akış, araçlar, görme) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Görsel oluşturma |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Asenkron video |
| `GET /v1/models` | Model kataloğu (herkese açık) |
| `GET /v1/credits` | Bakiye |

---

## 🔌 Diğer ajanlar

Burada listelenmeyen ajanların çoğu aynı şekilde çalışır — OpenAI uyumlu temel URL'yi ayarlayın:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** ve daha fazlası.

Anthropic uyumlu `/v1/messages` üzerinden: **claude-code-router** da `ANTHROPIC_BASE_URL` ile bağlanır.

**Model kimlikleri**: bunları `GET /v1/models` adresinde veya [modeller sayfasında](https://pleum.ai/models) bulun. Cline, Continue, OpenCode ve diğerleri listeyi otomatik olarak getirir. OpenRouter biçimli kimlikler (`openai/gpt-5.5`) otomatik olarak dönüştürülür.

**LiteLLM proxy** (Aider, OpenHands, Open Interpreter, SWE-agent ve gptme LiteLLM tabanlıdır ve doğrudan bağlanır — ancak bir LiteLLM proxy'si tutuyorsanız):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # openai/ öneki → OpenAI uyumlu rota
      api_base: https://router.pleum.ai/v1           # /chat/completions EKLEMEYİN
      api_key: os.environ/PLEUM_API_KEY
```

---

## Katkıda Bulunma

PleumRouter'ı burada listelenmeyen bir araçla mı çalıştırdınız? PR'lar memnuniyetle karşılanır — **test edilmiş** bir yapılandırma kod parçasıyla (temel URL, anahtar ortam değişkeni, model kimliği biçimi ve varsa dikkat edilmesi gereken noktalar) bir bölüm ekleyin.

## Lisans

[MIT](LICENSE)
