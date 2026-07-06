<div align="center">

# Como usar o PleumRouter

**Uma única chave de API para mais de 200 modelos de IA — compatível com OpenAI, cobrado em KRW.**

[Site](https://pleum.ai) · [Documentação](https://pleum.ai/docs) · [Modelos](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · Português · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

O PleumRouter é um gateway de IA: uma chave (`plm_…`), uma URL base, mais de 210 modelos de 18 provedores — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE e outros. Ele fala **OpenAI Chat Completions**, **Anthropic Messages** e **OpenAI Responses**, então praticamente todo agente de codificação, plugin de IDE e SDK se conecta com uma mudança de configuração de uma linha. Texto, embeddings, imagem, fala e vídeo passam todos pela mesma chave.

Este repositório reúne **receitas de integração verificadas**. Cada trecho abaixo é testado contra o gateway em produção.

## Primeiros passos

1. [Cadastre-se](https://pleum.ai/signup) → Painel → **API Keys** → emita uma chave (começa com `plm_`).
2. Aponte sua ferramenta para a URL base:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Alguns agentes (OpenCode, Crush) leem PLEUM_API_KEY — mesma chave, defina ambas.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Teste rápido:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Você recebe ₩1.000 de crédito grátis ao se cadastrar e um bônus de ₩5.000 na sua primeira recarga.

## Integrações

| Categoria | Ferramentas |
|---|---|
| [⚡ Lançador em um comando](#-pleum-cli--o-caminho-mais-rápido) | CLI `pleum` |
| [🤖 Agentes de codificação de terminal](#-agentes-de-terminal--cli) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 Agentes de IDE / GUI](#-agentes-de-ide--gui) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDKs](#-sdks) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 API multimodal](#-multimodal--imagem--áudio--vídeo) | Imagens, TTS, STT, Vídeo, Embeddings |
| [🔌 Tudo mais](#-mais-agentes) | IDs no estilo OpenRouter, proxy LiteLLM, mais de 15 outros agentes |

---

## ⚡ pleum CLI — o caminho mais rápido

A CLI oficial inicia seu agente favorito já conectado ao PleumRouter. Nenhum arquivo de configuração é alterado.

```bash
npm install -g pleumrouter        # ou: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # login pelo navegador, chave emitida e salva automaticamente
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # REPL de chat no terminal
pleum models                      # lista todos os modelos com preços
```

Suportado para lançamento automático: `claude` · `aider` · `codex` · `goose` · `openhands` (além de trechos de configuração para `opencode` · `crush`). As configurações das suas ferramentas existentes nunca são modificadas.

---

## 🤖 Agentes de terminal / CLI

### Claude Code (compatível com Anthropic)

O Claude Code e as ferramentas do Claude Agent SDK se conectam via o endpoint compatível com Anthropic `/v1/messages`.

```bash
# ANTHROPIC_BASE_URL é a RAIZ (sem /v1) — a própria CLI adiciona /v1/messages.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# A CLI oficial prefere ANTHROPIC_API_KEY; defina ambas por segurança.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ **Não** coloque `/v1` em `ANTHROPIC_BASE_URL` — isso vira `/v1/v1/messages` e falha. Chamadas de ferramentas e streaming funcionam de ponta a ponta, mesmo quando roteados para modelos compatíveis com OpenAI.

### Codex CLI (API Responses)

O Codex se conecta via a API OpenAI Responses (`/v1/responses`); o caminho Chat Completions foi removido do Codex em fevereiro de 2026.

```toml
# ~/.codex/config.toml
# model / model_provider são chaves na raiz do documento (devem ficar acima da [tabela]).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex adiciona /responses → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex suporta apenas a API Responses
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
// opencode.json   (ou: /connect → Other)
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

# Goose / OpenHands: prefixe o id do modelo com openai/
#   model = openai/gpt-4.1
```

### Gemini CLI

O Gemini CLI original tem suporte fraco a endpoints externos compatíveis com OpenAI; talvez seja necessário um wrapper ou fork compatível com OpenAI.

---

## 🖥 Agentes de IDE / GUI

### Cline · Roo Code · Kilo Code · Cursor

Escolha **OpenAI Compatible** (ou **Custom OpenAI**) como provedor e cole:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Sempre use o **slot OpenAI Compatible** — a entrada dedicada do OpenRouter é fixada em openrouter.ai e vai falhar. O **Cursor** exige `/v1` na URL base e um campo de chave não vazio. O **Kilo Code** tem um problema conhecido (#681) em que a URL base personalizada não é passada para a listagem de modelos — digite o ID do modelo manualmente.

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

Com `model: AUTODETECT`, o Continue busca a lista de modelos automaticamente.

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

Os nomes dos campos podem variar conforme a versão do Zed — consulte a documentação do Zed.

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
    base_url="https://router.pleum.ai",   # raiz, sem /v1 — o SDK adiciona /v1/messages
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # qualquer modelo do PleumRouter funciona
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Multimodal — imagem · áudio · vídeo

Todas as modalidades são endpoints HTTP compatíveis com OpenAI na mesma chave. Escolha um modelo que suporte a modalidade em [`GET /v1/models`](https://pleum.ai/models).

```bash
# Geração de imagem
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Texto para fala (retorna bytes de áudio; custo no cabeçalho X-Cost-Krw)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Fala para texto (upload multipart)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# A geração de vídeo é assíncrona: o POST retorna um job_id, depois faça polling em GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### Superfície da API

| Endpoint | Protocolo |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (streaming, ferramentas, visão) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Geração de imagem |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Vídeo assíncrono |
| `GET /v1/models` | Catálogo de modelos (público) |
| `GET /v1/credits` | Saldo |

---

## 🔌 Mais agentes

A maioria dos agentes não listados aqui funciona da mesma forma — defina a URL base compatível com OpenAI:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** e outros.

Via o endpoint compatível com Anthropic `/v1/messages`: o **claude-code-router** também se conecta com `ANTHROPIC_BASE_URL`.

**IDs de modelo**: encontre-os em `GET /v1/models` ou na [página de modelos](https://pleum.ai/models). Cline, Continue, OpenCode e outros buscam a lista automaticamente. IDs no formato OpenRouter (`openai/gpt-5.5`) são convertidos automaticamente.

**Proxy LiteLLM** (Aider, OpenHands, Open Interpreter, SWE-agent e gptme são baseados em LiteLLM e se conectam diretamente — mas se você mantém um proxy LiteLLM):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # prefixo openai/ → rota compatível com OpenAI
      api_base: https://router.pleum.ai/v1           # NÃO adicione /chat/completions
      api_key: os.environ/PLEUM_API_KEY
```

---

## Contribuindo

Conseguiu fazer o PleumRouter funcionar com uma ferramenta que não está listada aqui? PRs são bem-vindos — adicione uma seção com um trecho de configuração **testado** (URL base, variável de ambiente da chave, formato do ID do modelo e quaisquer detalhes importantes).

## Licença

[MIT](LICENSE)
