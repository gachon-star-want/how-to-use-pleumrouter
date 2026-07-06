<div align="center">

# 如何使用 PleumRouter

**一組 API 金鑰，暢用 200 多個 AI 模型 — 相容 OpenAI 介面，以韓元計費。**

[官方網站](https://pleum.ai) · [文件](https://pleum.ai/docs) · [模型列表](https://pleum.ai/models) · [線上試用](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · 繁體中文 · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter 是一個 AI 閘道器：只需一組金鑰（`plm_…`）、一個基底網址，即可存取來自 18 家供應商的 210 多個模型 — GPT、Claude、Gemini、DeepSeek、Qwen、EXAONE 等等。它支援 **OpenAI Chat Completions**、**Anthropic Messages** 以及 **OpenAI Responses** 三種介面協定，因此幾乎所有的程式碼助理、IDE 外掛與 SDK，只要改一行設定就能連上。文字、嵌入向量、圖像、語音與影片，全部共用同一組金鑰即可運作。

本專案彙整了**經過驗證的串接範例**。以下每一段程式碼都已在正式運行的閘道器上測試過。

## 快速上手

1. [註冊帳號](https://pleum.ai/signup) → 進入儀表板 → **API Keys** → 發行一組金鑰（以 `plm_` 開頭）。
2. 將你的工具指向此基底網址：

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# 部分代理程式（OpenCode、Crush）會讀取 PLEUM_API_KEY —— 同一組金鑰，兩個都要設定。
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. 連線測試：

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

註冊即可獲得 ₩1,000 免費點數，首次儲值再送 ₩5,000 獎勵金。

## 整合列表

| 分類 | 工具 |
|---|---|
| [⚡ 一鍵啟動器](#-pleum-cli-—-最快的方式) | `pleum` CLI |
| [🤖 終端機程式碼助理](#-終端機-cli-代理) | Claude Code、Codex CLI、Aider、OpenCode、Crush、Goose、OpenHands |
| [🖥 IDE / GUI 代理](#-ide--gui-代理) | Cline、Roo Code、Kilo Code、Cursor、Continue.dev、Zed |
| [📦 SDK](#-sdk) | OpenAI SDK（Python/JS）、Anthropic SDK |
| [🎨 多模態 API](#-多模態--圖像--語音--影片) | 圖像、TTS、STT、影片、嵌入向量 |
| [🔌 其他一切](#-其他代理) | OpenRouter 風格的模型 ID、LiteLLM 代理、15 種以上其他代理 |

---

## ⚡ pleum CLI — 最快的方式

官方 CLI 能直接啟動你偏好的代理程式，並自動接上 PleumRouter，完全不需要動到任何設定檔。

```bash
npm install -g pleumrouter        # 或：curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # 瀏覽器登入，金鑰自動發行並儲存
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # 終端機聊天 REPL
pleum models                      # 列出所有模型及其價格
```

支援自動啟動的工具：`claude` · `aider` · `codex` · `goose` · `openhands`（另提供 `opencode` · `crush` 的設定範例）。你原有的工具設定檔絕不會被修改。

---

## 🤖 終端機 / CLI 代理

### Claude Code（相容 Anthropic）

Claude Code 與 Claude Agent SDK 工具是透過相容 Anthropic 介面的 `/v1/messages` 端點連線。

```bash
# ANTHROPIC_BASE_URL 要填根網址（不含 /v1）—— CLI 自己會補上 /v1/messages。
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# 官方 CLI 優先讀取 ANTHROPIC_API_KEY；保險起見兩個都設定。
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ **切勿**在 `ANTHROPIC_BASE_URL` 中加入 `/v1` —— 這會變成 `/v1/v1/messages` 導致失敗。即使路由到相容 OpenAI 介面的模型，工具呼叫與串流輸出仍能完整運作。

### Codex CLI（Responses API）

Codex 是透過 OpenAI Responses API（`/v1/responses`）連線；Chat Completions 路徑已於 2026 年 2 月從 Codex 中移除。

```toml
# ~/.codex/config.toml
# model / model_provider 是文件根層級的鍵值（必須放在 [table] 之上）。
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex 會自動補上 /responses → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex 僅支援 Responses API
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
// opencode.json   (或：/connect → Other)
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

# Goose / OpenHands：模型 ID 前面要加上 openai/ 前綴
#   model = openai/gpt-4.1
```

### Gemini CLI

官方 Gemini CLI 對外部相容 OpenAI 端點的支援較弱；你可能需要一個相容 OpenAI 的封裝層或改用分支版本。

---

## 🖥 IDE / GUI 代理

### Cline · Roo Code · Kilo Code · Cursor

選擇 **OpenAI Compatible**（或 **Custom OpenAI**）作為供應商，並貼上以下設定：

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ 務必使用 **OpenAI Compatible 選項** —— 專屬的 OpenRouter 項目已寫死指向 openrouter.ai，無法使用。**Cursor** 要求基底網址必須包含 `/v1`，且金鑰欄位不可留空。**Kilo Code** 有一個已知問題（#681），自訂基底網址不會傳入模型列表功能 —— 請手動輸入模型 ID。

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

設定 `model: AUTODETECT` 後，Continue 會自動抓取模型列表。

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

欄位名稱可能因 Zed 版本而異 —— 請以 Zed 官方文件為準。

---

## 📦 SDK

### OpenAI SDK（Python）

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

### OpenAI SDK（JavaScript / TypeScript）

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
    base_url="https://router.pleum.ai",   # 根網址，不含 /v1 —— SDK 會自行補上 /v1/messages
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # PleumRouter 上的任何模型都可以使用
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 多模態 — 圖像 · 語音 · 影片

所有模態都是相容 OpenAI 介面的 HTTP 端點，共用同一組金鑰。請從 [`GET /v1/models`](https://pleum.ai/models) 挑選支援該模態的模型。

```bash
# 圖像生成
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# 文字轉語音（回傳音訊位元組；費用記載於 X-Cost-Krw 標頭）
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# 語音轉文字（multipart 上傳）
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# 影片生成為非同步作業：POST 會回傳 job_id，接著輪詢 GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### API 介面總覽

| 端點 | 協定 |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions（串流、工具呼叫、視覺辨識） |
| `POST /v1/messages` | Anthropic Messages（Claude Code、Agent SDK） |
| `POST /v1/responses` | OpenAI Responses（Codex CLI） |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | 圖像生成 |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | 非同步影片生成 |
| `GET /v1/models` | 模型目錄（公開） |
| `GET /v1/credits` | 餘額查詢 |

---

## 🔌 其他代理

大多數未列於此處的代理都採用相同方式運作 —— 只需設定相容 OpenAI 的基底網址即可：

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** 等等。

透過相容 Anthropic 的 `/v1/messages`：**claude-code-router** 也可以用 `ANTHROPIC_BASE_URL` 連線。

**模型 ID**：可在 `GET /v1/models` 或[模型頁面](https://pleum.ai/models)查詢。Cline、Continue、OpenCode 等工具會自動抓取列表。OpenRouter 格式的 ID（`openai/gpt-5.5`）會自動轉換。

**LiteLLM 代理**（Aider、OpenHands、Open Interpreter、SWE-agent 與 gptme 都是基於 LiteLLM 並可直接連線 —— 但若你仍在使用 LiteLLM 代理伺服器）：

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # openai/ 前綴 → 路由至相容 OpenAI 介面
      api_base: https://router.pleum.ai/v1           # 請勿再加上 /chat/completions
      api_key: os.environ/PLEUM_API_KEY
```

---

## 貢獻方式

已經成功把 PleumRouter 接上這裡沒列出的工具了嗎？歡迎提交 PR —— 附上一段**經過測試**的設定範例（基底網址、金鑰環境變數、模型 ID 格式，以及任何需要注意的坑）。

## 授權條款

[MIT](LICENSE)
