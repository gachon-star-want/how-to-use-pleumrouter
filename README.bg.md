<div align="center">

# Как да използвате PleumRouter

**Един API ключ за над 200 AI модела — съвместим с OpenAI, таксуван в KRW.**

[Уебсайт](https://pleum.ai) · [Документация](https://pleum.ai/docs) · [Модели](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · Български · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter е AI шлюз: един ключ (`plm_…`), един базов URL адрес, над 210 модела от 18 доставчика — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE и други. Той поддържа **OpenAI Chat Completions**, **Anthropic Messages** и **OpenAI Responses**, така че почти всеки агент за кодиране, IDE плъгин и SDK се свързва само с една промяна в конфигурацията. Текст, ембединги, изображения, реч и видео — всичко минава през един и същ ключ.

Това хранилище събира **проверени рецепти за интеграция**. Всеки фрагмент по-долу е тестван срещу живия шлюз.

## Първи стъпки

1. [Регистрирайте се](https://pleum.ai/signup) → Табло → **API Keys** → издайте ключ (започва с `plm_`).
2. Насочете инструмента си към базовия URL адрес:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Някои агенти (OpenCode, Crush) четат PLEUM_API_KEY — същият ключ, задайте и двете.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Бърз тест:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Получавате безплатен кредит от ₩1,000 при регистрация и бонус от ₩5,000 при първото зареждане.

## Интеграции

| Категория | Инструменти |
|---|---|
| [⚡ Лансиране с една команда](#-pleum-cli--бързият-път) | CLI `pleum` |
| [🤖 Терминални агенти за кодиране](#-терминални--cli-агенти) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE / GUI агенти](#-ide--gui-агенти) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK-та](#-sdk-та) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 Мултимодален API](#-мултимодален--изображения--аудио--видео) | Изображения, TTS, STT, видео, ембединги |
| [🔌 Всичко останало](#-още-агенти) | ID-та във формат OpenRouter, LiteLLM прокси, над 15 други агенти |

---

## ⚡ pleum CLI — бързият път

Официалният CLI стартира любимия ви агент, вече свързан с PleumRouter. Никакви конфигурационни файлове не се докосват.

```bash
npm install -g pleumrouter        # или: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # вход през браузър, ключът се издава и запазва автоматично
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # терминален чат REPL
pleum models                      # изброява всички модели с цените им
```

Поддържа се автоматично лансиране за: `claude` · `aider` · `codex` · `goose` · `openhands` (плюс конфигурационни фрагменти за `opencode` · `crush`). Съществуващите ви конфигурации на инструменти никога не се променят.

---

## 🤖 Терминални / CLI агенти

### Claude Code (съвместим с Anthropic)

Claude Code и инструментите на Claude Agent SDK се свързват чрез съвместимата с Anthropic крайна точка `/v1/messages`.

```bash
# ANTHROPIC_BASE_URL е КОРЕНЪТ (без /v1) — самият CLI добавя /v1/messages.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# Официалният CLI предпочита ANTHROPIC_API_KEY; задайте и двете за сигурност.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ **Не** поставяйте `/v1` в `ANTHROPIC_BASE_URL` — превръща се в `/v1/v1/messages` и се проваля. Извикванията на инструменти и стрийминга работят изцяло, дори когато се насочват към съвместими с OpenAI модели.

### Codex CLI (Responses API)

Codex се свързва чрез OpenAI Responses API (`/v1/responses`); пътят Chat Completions беше премахнат от Codex през февруари 2026 г.

```toml
# ~/.codex/config.toml
# model / model_provider са ключове от кореновия документ (трябва да са над [table]).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex добавя /responses → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex поддържа само Responses API
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

# Goose / OpenHands: добавете префикс openai/ пред ID-то на модела
#   model = openai/gpt-4.1
```

### Gemini CLI

Официалният Gemini CLI има слаба поддръжка за външни съвместими с OpenAI крайни точки; може да ви е необходима съвместима с OpenAI обвивка (wrapper) или форк.

---

## 🖥 IDE / GUI агенти

### Cline · Roo Code · Kilo Code · Cursor

Изберете **OpenAI Compatible** (или **Custom OpenAI**) като доставчик и поставете:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Винаги използвайте слота **OpenAI Compatible** — специализираният запис за OpenRouter е твърдо кодиран към openrouter.ai и ще се провали. **Cursor** изисква `/v1` в базовия URL адрес и непразно поле за ключ. **Kilo Code** има известен проблем (#681), при който персонализираният базов URL адрес не се предава при извеждането на списъка с модели — въведете ID-то на модела ръчно.

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

С `model: AUTODETECT` Continue извлича списъка с модели автоматично.

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

Имената на полетата може да варират в зависимост от версията на Zed — проверете документацията на Zed.

---

## 📦 SDK-та

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
    base_url="https://router.pleum.ai",   # корен, без /v1 — SDK-то добавя /v1/messages
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # работи с всеки модел на PleumRouter
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Мултимодален — изображения · аудио · видео

Всички модалности са HTTP крайни точки, съвместими с OpenAI, на един и същ ключ. Изберете модел, който поддържа съответната модалност, от [`GET /v1/models`](https://pleum.ai/models).

```bash
# Генериране на изображение
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Текст в реч (връща аудио байтове; цената е в хедъра X-Cost-Krw)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Реч в текст (качване multipart)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# Генерирането на видео е асинхронно: POST връща job_id, след което следи GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### API повърхност

| Крайна точка | Протокол |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (стрийминг, инструменти, зрение) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Генериране на изображения |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Асинхронно видео |
| `GET /v1/models` | Каталог с модели (публичен) |
| `GET /v1/credits` | Баланс |

---

## 🔌 Още агенти

Повечето агенти, които не са изброени тук, работят по същия начин — задайте съвместимия с OpenAI базов URL адрес:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** и други.

Чрез съвместимата с Anthropic крайна точка `/v1/messages`: **claude-code-router** също се свързва с `ANTHROPIC_BASE_URL`.

**ID-та на моделите**: намерете ги чрез `GET /v1/models` или на [страницата с модели](https://pleum.ai/models). Cline, Continue, OpenCode и други извличат списъка автоматично. ID-та във формат OpenRouter (`openai/gpt-5.5`) се преобразуват автоматично.

**LiteLLM прокси** (Aider, OpenHands, Open Interpreter, SWE-agent и gptme са базирани на LiteLLM и се свързват директно — но ако поддържате LiteLLM прокси):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # префикс openai/ → маршрут за съвместимост с OpenAI
      api_base: https://router.pleum.ai/v1           # НЕ добавяйте /chat/completions
      api_key: os.environ/PLEUM_API_KEY
```

---

## Принос

Успяхте да накарате PleumRouter да работи с инструмент, който не е изброен тук? PR-овете са добре дошли — добавете раздел с **тестван** конфигурационен фрагмент (базов URL адрес, environment променлива за ключа, формат на ID-то на модела и всякакви особености).

## Лиценз

[MIT](LICENSE)
