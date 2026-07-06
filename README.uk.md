<div align="center">

# Як користуватися PleumRouter

**Один API-ключ для 200+ моделей ШІ — сумісний з OpenAI, оплата в KRW.**

[Вебсайт](https://pleum.ai) · [Документація](https://pleum.ai/docs) · [Моделі](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · Українська · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter — це шлюз ШІ: один ключ (`plm_…`), одна базова URL-адреса, 210+ моделей від 18 провайдерів — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE та інші. Він підтримує протоколи **OpenAI Chat Completions**, **Anthropic Messages** і **OpenAI Responses**, тож майже будь-який агент для кодування, плагін IDE чи SDK підключається після зміни одного рядка конфігурації. Текст, ембеддинги, зображення, мовлення та відео — все працює через один і той самий ключ.

Цей репозиторій збирає **перевірені рецепти інтеграції**. Кожен фрагмент коду нижче протестований на робочому шлюзі.

## Початок роботи

1. [Зареєструйтеся](https://pleum.ai/signup) → Панель керування → **API Keys** → випустіть ключ (починається з `plm_`).
2. Спрямуйте свій інструмент на базову URL-адресу:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Деякі агенти (OpenCode, Crush) читають PLEUM_API_KEY — той самий ключ, встановіть обидва.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Тест на працездатність:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Ви отримуєте ₩1,000 безкоштовного кредиту при реєстрації та бонус ₩5,000 при першому поповненні.

## Інтеграції

| Категорія | Інструменти |
|---|---|
| [⚡ Лаунчер в одну команду](#-pleum-cli--швидкий-шлях) | CLI `pleum` |
| [🤖 Термінальні агенти для кодування](#-термінальні--cli-агенти) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE / GUI агенти](#-ide--gui-агенти) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK](#-sdk) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 Мультимодальний API](#-мультимодальність--зображення--аудіо--відео) | Зображення, TTS, STT, Відео, Embeddings |
| [🔌 Все інше](#-інші-агенти) | Ідентифікатори у стилі OpenRouter, проксі LiteLLM, 15+ інших агентів |

---

## ⚡ pleum CLI — швидкий шлях

Офіційний CLI запускає вашого улюбленого агента, уже налаштованого на PleumRouter. Жодні конфігураційні файли не змінюються.

```bash
npm install -g pleumrouter        # або: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # вхід через браузер, ключ видається та зберігається автоматично
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # термінальний чат-REPL
pleum models                      # список усіх моделей з цінами
```

Підтримується автозапуск для: `claude` · `aider` · `codex` · `goose` · `openhands` (плюс фрагменти конфігурації для `opencode` · `crush`). Ваші наявні конфігурації інструментів ніколи не змінюються.

---

## 🤖 Термінальні / CLI агенти

### Claude Code (сумісний з Anthropic)

Claude Code та інструменти Claude Agent SDK підключаються через сумісний з Anthropic ендпоінт `/v1/messages`.

```bash
# ANTHROPIC_BASE_URL — це КОРІНЬ (без /v1) — сам CLI додає /v1/messages.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# Офіційний CLI віддає перевагу ANTHROPIC_API_KEY; встановіть обидва про всяк випадок.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ **Не** додавайте `/v1` до `ANTHROPIC_BASE_URL` — вийде `/v1/v1/messages`, і запит не спрацює. Виклики інструментів та потокова передача працюють наскрізно, навіть коли маршрутизація йде на сумісні з OpenAI моделі.

### Codex CLI (Responses API)

Codex підключається через OpenAI Responses API (`/v1/responses`); шлях Chat Completions було видалено з Codex у лютому 2026 року.

```toml
# ~/.codex/config.toml
# model / model_provider — ключі кореня документа (мають бути вище за [table]).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex додає /responses → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex підтримує лише Responses API
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
// opencode.json   (або: /connect → Other)
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

# Goose / OpenHands: додайте префікс openai/ до ідентифікатора моделі
#   model = openai/gpt-4.1
```

### Gemini CLI

Офіційний Gemini CLI має слабку підтримку зовнішніх сумісних з OpenAI ендпоінтів; можливо, вам знадобиться сумісна з OpenAI обгортка або форк.

---

## 🖥 IDE / GUI агенти

### Cline · Roo Code · Kilo Code · Cursor

Виберіть **OpenAI Compatible** (або **Custom OpenAI**) як провайдера та вставте:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Завжди використовуйте **слот OpenAI Compatible** — виділений запис OpenRouter жорстко прив'язаний до openrouter.ai і не спрацює. **Cursor** вимагає `/v1` у базовій URL-адресі та непорожнє поле ключа. **Kilo Code** має відому проблему (#681), коли користувацька базова URL-адреса не передається до списку моделей — введіть ідентифікатор моделі вручну.

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

З `model: AUTODETECT` Continue автоматично завантажує список моделей.

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

Назви полів можуть відрізнятися залежно від версії Zed — перевірте документацію Zed.

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
    base_url="https://router.pleum.ai",   # корінь, без /v1 — SDK додає /v1/messages
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # працює будь-яка модель PleumRouter
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Мультимодальність — зображення · аудіо · відео

Усі модальності — це сумісні з OpenAI HTTP-ендпоінти під тим самим ключем. Виберіть модель, яка підтримує потрібну модальність, на [`GET /v1/models`](https://pleum.ai/models).

```bash
# Генерація зображень
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Синтез мовлення (повертає аудіобайти; вартість у заголовку X-Cost-Krw)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Розпізнавання мовлення (multipart-завантаження)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# Генерація відео є асинхронною: POST повертає job_id, потім опитуйте GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### Поверхня API

| Ендпоінт | Протокол |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (потокова передача, інструменти, зір) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Генерація зображень |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Асинхронне відео |
| `GET /v1/models` | Каталог моделей (публічний) |
| `GET /v1/credits` | Баланс |

---

## 🔌 Інші агенти

Більшість агентів, не перелічених тут, працюють так само — встановіть сумісну з OpenAI базову URL-адресу:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** та інші.

Через сумісний з Anthropic `/v1/messages`: **claude-code-router** також підключається за допомогою `ANTHROPIC_BASE_URL`.

**Ідентифікатори моделей**: знайдіть їх на `GET /v1/models` або на [сторінці моделей](https://pleum.ai/models). Cline, Continue, OpenCode та інші отримують список автоматично. Ідентифікатори у форматі OpenRouter (`openai/gpt-5.5`) конвертуються автоматично.

**Проксі LiteLLM** (Aider, OpenHands, Open Interpreter, SWE-agent та gptme базуються на LiteLLM і підключаються напряму — але якщо ви використовуєте проксі LiteLLM):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # префікс openai/ → маршрут, сумісний з OpenAI
      api_base: https://router.pleum.ai/v1           # НЕ додавайте /chat/completions
      api_key: os.environ/PLEUM_API_KEY
```

---

## Внесок

Вдалося запустити PleumRouter з інструментом, якого немає в цьому списку? PR вітаються — додайте розділ із **перевіреним** фрагментом конфігурації (базова URL-адреса, змінна середовища для ключа, формат ідентифікатора моделі та будь-які підводні камені).

## Ліцензія

[MIT](LICENSE)
