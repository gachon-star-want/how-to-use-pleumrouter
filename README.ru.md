<div align="center">

# Как использовать PleumRouter

**Один API-ключ для 200+ моделей ИИ — совместимость с OpenAI, оплата в KRW.**

[Сайт](https://pleum.ai) · [Документация](https://pleum.ai/docs) · [Модели](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · Русский · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter — это шлюз ИИ: один ключ (`plm_…`), один базовый URL, 210+ моделей от 18 провайдеров — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE и другие. Он поддерживает **OpenAI Chat Completions**, **Anthropic Messages** и **OpenAI Responses**, поэтому почти любой агент для программирования, плагин для IDE или SDK подключается всего одним изменением конфигурации. Текст, эмбеддинги, изображения, речь и видео — всё работает через один и тот же ключ.

Этот репозиторий собирает **проверенные рецепты интеграции**. Каждый фрагмент кода ниже протестирован на реальном шлюзе.

## Начало работы

1. [Зарегистрируйтесь](https://pleum.ai/signup) → Панель управления → **API Keys** → выпустите ключ (начинается с `plm_`).
2. Направьте свой инструмент на базовый URL:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Некоторые агенты (OpenCode, Crush) читают PLEUM_API_KEY — тот же ключ, задайте обе переменные.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Тестовый запрос:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

При регистрации вы получаете ₩1,000 бесплатных кредитов, а при первом пополнении — бонус ₩5,000.

## Интеграции

| Категория | Инструменты |
|---|---|
| [⚡ Запуск одной командой](#-pleum-cli--быстрый-путь) | CLI `pleum` |
| [🤖 Терминальные агенты для программирования](#-терминальные--cli-агенты) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE / GUI-агенты](#-ide--gui-агенты) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK](#-sdk) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 Мультимодальный API](#-мультимодальность--изображения--аудио--видео) | Изображения, TTS, STT, видео, эмбеддинги |
| [🔌 Всё остальное](#-другие-агенты) | ID в стиле OpenRouter, прокси LiteLLM, 15+ других агентов |

---

## ⚡ pleum CLI — быстрый путь

Официальный CLI запускает вашего любимого агента, уже настроенного на работу с PleumRouter. Никакие конфигурационные файлы не затрагиваются.

```bash
npm install -g pleumrouter        # или: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # вход через браузер, ключ выпускается и сохраняется автоматически
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # чат-REPL в терминале
pleum models                      # список всех моделей с ценами
```

Автозапуск поддерживается для: `claude` · `aider` · `codex` · `goose` · `openhands` (плюс фрагменты конфигурации для `opencode` · `crush`). Существующие конфигурации ваших инструментов никогда не изменяются.

---

## 🤖 Терминальные / CLI-агенты

### Claude Code (совместимость с Anthropic)

Claude Code и инструменты Claude Agent SDK подключаются через совместимый с Anthropic эндпоинт `/v1/messages`.

```bash
# ANTHROPIC_BASE_URL — это КОРНЕВОЙ URL (без /v1) — сам CLI добавляет /v1/messages.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# Официальный CLI предпочитает ANTHROPIC_API_KEY; задайте обе переменные для надёжности.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ **Не** добавляйте `/v1` в `ANTHROPIC_BASE_URL` — получится `/v1/v1/messages`, и запрос не пройдёт. Вызовы инструментов и потоковая передача работают полностью, даже при маршрутизации на модели, совместимые с OpenAI.

### Codex CLI (Responses API)

Codex подключается через OpenAI Responses API (`/v1/responses`); путь Chat Completions был удалён из Codex в феврале 2026 года.

```toml
# ~/.codex/config.toml
# model / model_provider — это ключи корня документа (должны быть выше [table]).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex добавляет /responses → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex поддерживает только Responses API
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
// opencode.json   (или: /connect → Other)
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

# Goose / OpenHands: добавьте к id модели префикс openai/
#   model = openai/gpt-4.1
```

### Gemini CLI

У исходного Gemini CLI слабая поддержка внешних совместимых с OpenAI эндпоинтов; может потребоваться обёртка или форк, совместимые с OpenAI.

---

## 🖥 IDE / GUI-агенты

### Cline · Roo Code · Kilo Code · Cursor

Выберите **OpenAI Compatible** (или **Custom OpenAI**) в качестве провайдера и вставьте:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Всегда используйте слот **OpenAI Compatible** — выделенный пункт OpenRouter жёстко привязан к openrouter.ai и работать не будет. **Cursor** требует `/v1` в базовом URL и непустое поле ключа. У **Kilo Code** есть известная проблема (#681), из-за которой пользовательский базовый URL не передаётся в список моделей — вводите ID модели вручную.

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

При `model: AUTODETECT` Continue автоматически получает список моделей.

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

Названия полей могут отличаться в зависимости от версии Zed — сверьтесь с документацией Zed.

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
    base_url="https://router.pleum.ai",   # корневой URL, без /v1 — SDK сам добавляет /v1/messages
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # подойдёт любая модель PleumRouter
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Мультимодальность — изображения · аудио · видео

Все модальности — это совместимые с OpenAI HTTP-эндпоинты на одном и том же ключе. Выберите модель, поддерживающую нужную модальность, через [`GET /v1/models`](https://pleum.ai/models).

```bash
# Генерация изображений
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Синтез речи (возвращает аудиобайты; стоимость в заголовке X-Cost-Krw)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Распознавание речи (multipart-загрузка)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# Генерация видео асинхронна: POST возвращает job_id, затем опрашивайте GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### Поверхность API

| Эндпоинт | Протокол |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (потоковая передача, инструменты, зрение) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Генерация изображений |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Асинхронное видео |
| `GET /v1/models` | Каталог моделей (публичный) |
| `GET /v1/credits` | Баланс |

---

## 🔌 Другие агенты

Большинство агентов, не перечисленных здесь, работают так же — задайте совместимый с OpenAI базовый URL:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** и другие.

Через совместимый с Anthropic `/v1/messages`: **claude-code-router** также подключается с помощью `ANTHROPIC_BASE_URL`.

**ID моделей**: найдите их через `GET /v1/models` или на [странице моделей](https://pleum.ai/models). Cline, Continue, OpenCode и другие получают список автоматически. ID в формате OpenRouter (`openai/gpt-5.5`) конвертируются автоматически.

**Прокси LiteLLM** (Aider, OpenHands, Open Interpreter, SWE-agent и gptme основаны на LiteLLM и подключаются напрямую — но если вы используете прокси LiteLLM):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # префикс openai/ → маршрут, совместимый с OpenAI
      api_base: https://router.pleum.ai/v1           # НЕ добавляйте /chat/completions
      api_key: os.environ/PLEUM_API_KEY
```

---

## Вклад в проект

Заставили PleumRouter работать с инструментом, которого здесь нет в списке? Мы будем рады PR — добавьте раздел с **протестированным** фрагментом конфигурации (базовый URL, переменная окружения для ключа, формат ID модели и любые подводные камни).

## Лицензия

[MIT](LICENSE)
