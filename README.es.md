<div align="center">

# Cómo usar PleumRouter

**Una clave API para más de 200 modelos de IA — compatible con OpenAI, facturado en KRW.**

[Sitio web](https://pleum.ai) · [Documentación](https://pleum.ai/docs) · [Modelos](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · Español · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter es una puerta de enlace de IA: una clave (`plm_…`), una URL base, más de 210 modelos de 18 proveedores — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE y más. Habla **OpenAI Chat Completions**, **Anthropic Messages** y **OpenAI Responses**, de modo que casi cualquier agente de codificación, plugin de IDE o SDK se conecta con un cambio de configuración de una sola línea. Texto, embeddings, imagen, voz y video funcionan todos a través de la misma clave.

Este repositorio recopila **recetas de integración verificadas**. Cada fragmento a continuación se ha probado contra la puerta de enlace en producción.

## Primeros pasos

1. [Regístrate](https://pleum.ai/signup) → Panel de control → **API Keys** → emite una clave (comienza con `plm_`).
2. Apunta tu herramienta a la URL base:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Algunos agentes (OpenCode, Crush) leen PLEUM_API_KEY — la misma clave, configura ambas.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Prueba rápida:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Recibes ₩1,000 de crédito gratis al registrarte y un bono de ₩5,000 en tu primera recarga.

## Integraciones

| Categoría | Herramientas |
|---|---|
| [⚡ Lanzador de un solo comando](#-pleum-cli--el-camino-rápido) | CLI `pleum` |
| [🤖 Agentes de codificación en terminal](#-agentes-de-terminal--cli) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 Agentes IDE / GUI](#-agentes-ide--gui) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDKs](#-sdks) | SDK de OpenAI (Python/JS), SDK de Anthropic |
| [🎨 API multimodal](#-multimodal--imagen--audio--video) | Imágenes, TTS, STT, Video, Embeddings |
| [🔌 Todo lo demás](#-más-agentes) | IDs estilo OpenRouter, proxy LiteLLM, más de 15 agentes adicionales |

---

## ⚡ pleum CLI — el camino rápido

El CLI oficial lanza tu agente favorito ya conectado a PleumRouter. Sin tocar archivos de configuración.

```bash
npm install -g pleumrouter        # o: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # inicio de sesión en el navegador, clave emitida y guardada automáticamente
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # REPL de chat en terminal
pleum models                      # lista todos los modelos con sus precios
```

Compatible con lanzamiento automático: `claude` · `aider` · `codex` · `goose` · `openhands` (además de fragmentos de configuración para `opencode` · `crush`). Las configuraciones existentes de tus herramientas nunca se modifican.

---

## 🤖 Agentes de terminal / CLI

### Claude Code (compatible con Anthropic)

Claude Code y las herramientas del Claude Agent SDK se conectan a través del endpoint compatible con Anthropic `/v1/messages`.

```bash
# ANTHROPIC_BASE_URL es la RAÍZ (sin /v1) — el CLI agrega /v1/messages por sí mismo.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# El CLI oficial prefiere ANTHROPIC_API_KEY; configura ambas por seguridad.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ **No** pongas `/v1` en `ANTHROPIC_BASE_URL` — se convierte en `/v1/v1/messages` y falla. Las llamadas a herramientas y el streaming funcionan de extremo a extremo, incluso cuando se enrutan a modelos compatibles con OpenAI.

### Codex CLI (API Responses)

Codex se conecta a través de la API OpenAI Responses (`/v1/responses`); la ruta Chat Completions se eliminó de Codex en febrero de 2026.

```toml
# ~/.codex/config.toml
# model / model_provider son claves raíz del documento (deben ir por encima de la [tabla]).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex añade /responses → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex solo admite la API Responses
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

# Goose / OpenHands: antepón openai/ al id del modelo
#   model = openai/gpt-4.1
```

### Gemini CLI

El Gemini CLI original tiene soporte débil para endpoints externos compatibles con OpenAI; es posible que necesites un wrapper o fork compatible con OpenAI.

---

## 🖥 Agentes IDE / GUI

### Cline · Roo Code · Kilo Code · Cursor

Elige **OpenAI Compatible** (o **Custom OpenAI**) como proveedor y pega:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Usa siempre el **slot OpenAI Compatible** — la entrada dedicada de OpenRouter está codificada de forma fija a openrouter.ai y fallará. **Cursor** requiere `/v1` en la URL base y un campo de clave no vacío. **Kilo Code** tiene un problema conocido (#681) donde la URL base personalizada no se pasa al listado de modelos — introduce el ID del modelo manualmente.

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

Con `model: AUTODETECT`, Continue obtiene la lista de modelos automáticamente.

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

Los nombres de los campos pueden variar según la versión de Zed — consulta la documentación de Zed.

---

## 📦 SDKs

### SDK de OpenAI (Python)

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

### SDK de OpenAI (JavaScript / TypeScript)

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

### SDK de Anthropic

```python
import anthropic

client = anthropic.Anthropic(
    base_url="https://router.pleum.ai",   # raíz, sin /v1 — el SDK añade /v1/messages
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # funciona con cualquier modelo de PleumRouter
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Multimodal — imagen · audio · video

Todas las modalidades son endpoints HTTP compatibles con OpenAI bajo la misma clave. Elige un modelo que admita la modalidad en [`GET /v1/models`](https://pleum.ai/models).

```bash
# Generación de imágenes
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Texto a voz (devuelve bytes de audio; el costo está en el encabezado X-Cost-Krw)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Voz a texto (subida multipart)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# La generación de video es asíncrona: POST devuelve un job_id, luego consulta GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### Superficie de la API

| Endpoint | Protocolo |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (streaming, herramientas, visión) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Generación de imágenes |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Video asíncrono |
| `GET /v1/models` | Catálogo de modelos (público) |
| `GET /v1/credits` | Saldo |

---

## 🔌 Más agentes

La mayoría de los agentes no listados aquí funcionan de la misma manera — configura la URL base compatible con OpenAI:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** y más.

A través de la API compatible con Anthropic `/v1/messages`: **claude-code-router** también se conecta con `ANTHROPIC_BASE_URL`.

**IDs de modelos**: encuéntralos en `GET /v1/models` o en la [página de modelos](https://pleum.ai/models). Cline, Continue, OpenCode y otros obtienen la lista automáticamente. Los IDs en formato OpenRouter (`openai/gpt-5.5`) se convierten automáticamente.

**Proxy LiteLLM** (Aider, OpenHands, Open Interpreter, SWE-agent y gptme están basados en LiteLLM y se conectan directamente — pero si mantienes un proxy LiteLLM):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # prefijo openai/ → ruta compatible con OpenAI
      api_base: https://router.pleum.ai/v1           # NO añadir /chat/completions
      api_key: os.environ/PLEUM_API_KEY
```

---

## Contribuciones

¿Conseguiste que PleumRouter funcione con una herramienta que no está en esta lista? Los PRs son bienvenidos — añade una sección con un fragmento de configuración **probado** (URL base, variable de entorno de la clave, formato del ID de modelo y cualquier detalle a tener en cuenta).

## Licencia

[MIT](LICENSE)
