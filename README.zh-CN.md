<div align="center">

# 如何使用 PleumRouter

**一个 API 密钥，畅享 200+ AI 模型 — 兼容 OpenAI，以韩元（KRW）计费。**

[官网](https://pleum.ai) · [文档](https://pleum.ai/docs) · [模型](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · 简体中文 · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter 是一个 AI 网关：一个密钥（`plm_…`）、一个基础 URL，即可调用来自 18 家提供商的 210+ 模型 — GPT、Claude、Gemini、DeepSeek、Qwen、EXAONE 等等。它兼容 **OpenAI Chat Completions**、**Anthropic Messages** 和 **OpenAI Responses** 协议，因此几乎所有编程智能体、IDE 插件和 SDK 只需修改一行配置即可接入。文本、向量嵌入（embeddings）、图像、语音和视频，全部通过同一个密钥运行。

本仓库收录了**经过验证的集成方案**。以下每个代码片段都在真实网关环境中测试通过。

## 快速开始

1. [注册](https://pleum.ai/signup) → 进入控制台 → **API Keys** → 签发一个密钥（以 `plm_` 开头）。
2. 将你的工具指向该基础 URL：

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# 部分智能体（OpenCode、Crush）读取 PLEUM_API_KEY —— 是同一个密钥，两者都要设置。
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. 冒烟测试（Smoke test）：

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

注册即可获得 ₩1,000 免费额度，首次充值再送 ₩5,000 奖励。

## 集成方案

| 分类 | 工具 |
|---|---|
| [⚡ 一键启动器](#-pleum-cli--最快路径) | `pleum` CLI |
| [🤖 终端编程智能体](#-终端--cli-智能体) | Claude Code、Codex CLI、Aider、OpenCode、Crush、Goose、OpenHands |
| [🖥 IDE / 图形界面智能体](#-ide--图形界面智能体) | Cline、Roo Code、Kilo Code、Cursor、Continue.dev、Zed |
| [📦 SDK](#-sdk) | OpenAI SDK（Python/JS）、Anthropic SDK |
| [🎨 多模态 API](#-多模态--图像--音频--视频) | 图像、TTS、STT、视频、向量嵌入 |
| [🔌 其他](#-更多智能体) | OpenRouter 风格 ID、LiteLLM 代理、15+ 其他智能体 |

---

## ⚡ pleum CLI — 最快路径

官方 CLI 可直接启动你常用的智能体，并自动完成与 PleumRouter 的对接，无需改动任何配置文件。

```bash
npm install -g pleumrouter        # 或者：curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # 浏览器登录，密钥自动签发并保存
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # 终端聊天 REPL
pleum models                      # 列出所有模型及价格
```

支持自动启动的工具：`claude` · `aider` · `codex` · `goose` · `openhands`（另外还为 `opencode` · `crush` 提供配置片段）。你现有的工具配置永远不会被修改。

---

## 🤖 终端 / CLI 智能体

### Claude Code（兼容 Anthropic）

Claude Code 与 Claude Agent SDK 工具通过兼容 Anthropic 的 `/v1/messages` 端点连接。

```bash
# ANTHROPIC_BASE_URL 是根路径（不带 /v1）—— CLI 会自行追加 /v1/messages。
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# 官方 CLI 优先读取 ANTHROPIC_API_KEY；两者都设置以确保安全。
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ **不要**在 `ANTHROPIC_BASE_URL` 中包含 `/v1` —— 否则会变成 `/v1/v1/messages` 并导致失败。工具调用（tool calls）与流式响应（streaming）均可全流程正常工作，即使路由到兼容 OpenAI 的模型也是如此。

### Codex CLI（Responses API）

Codex 通过 OpenAI Responses API（`/v1/responses`）连接；Chat Completions 路径已于 2026 年 2 月从 Codex 中移除。

```toml
# ~/.codex/config.toml
# model / model_provider 是文档根级键（必须位于 [table] 之上）。
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex 会追加 /responses → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex 仅支持 Responses API
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
// opencode.json   （或者：/connect → Other）
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

# Goose / OpenHands：在模型 ID 前加上 openai/ 前缀
#   model = openai/gpt-4.1
```

### Gemini CLI

上游 Gemini CLI 对外部兼容 OpenAI 的端点支持较弱；你可能需要一个兼容 OpenAI 的封装器（wrapper）或分支版本（fork）。

---

## 🖥 IDE / 图形界面智能体

### Cline · Roo Code · Kilo Code · Cursor

选择 **OpenAI Compatible**（或 **Custom OpenAI**）作为提供商，然后填入：

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ 务必使用 **OpenAI Compatible 插槽** —— 专用的 OpenRouter 入口被硬编码为 openrouter.ai，无法正常工作。**Cursor** 要求基础 URL 中必须包含 `/v1`，且密钥字段不能为空。**Kilo Code** 存在一个已知问题（#681）：自定义基础 URL 不会被传递给模型列表拉取逻辑 —— 请手动输入模型 ID。

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

设置 `model: AUTODETECT` 后，Continue 会自动拉取模型列表。

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

字段名称可能因 Zed 版本而异 —— 请查阅 Zed 官方文档确认。

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
    base_url="https://router.pleum.ai",   # 根路径，不带 /v1 —— SDK 会自行追加 /v1/messages
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # 任意 PleumRouter 模型均可使用
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 多模态 — 图像 · 音频 · 视频

所有模态均为兼容 OpenAI 的 HTTP 端点，共用同一个密钥。请从 [`GET /v1/models`](https://pleum.ai/models) 中选择支持对应模态的模型。

```bash
# 图像生成
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# 文字转语音（返回音频字节数据；费用记录在 X-Cost-Krw 响应头中）
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# 语音转文字（multipart 文件上传）
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# 视频生成为异步接口：POST 请求返回 job_id，随后轮询 GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### API 接口一览

| 端点 | 协议 |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions（流式响应、工具调用、视觉能力） |
| `POST /v1/messages` | Anthropic Messages（Claude Code、Agent SDK） |
| `POST /v1/responses` | OpenAI Responses（Codex CLI） |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | 图像生成 |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | 异步视频生成 |
| `GET /v1/models` | 模型目录（公开） |
| `GET /v1/credits` | 余额查询 |

---

## 🔌 更多智能体

大多数未在此列出的智能体，接入方式相同 —— 设置兼容 OpenAI 的基础 URL 即可：

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby（对话模式）· Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** 及更多。

通过兼容 Anthropic 的 `/v1/messages`：**claude-code-router** 同样可以用 `ANTHROPIC_BASE_URL` 连接。

**模型 ID**：可在 `GET /v1/models` 或[模型页面](https://pleum.ai/models)查询。Cline、Continue、OpenCode 等工具会自动拉取列表。OpenRouter 格式的 ID（如 `openai/gpt-5.5`）会被自动转换。

**LiteLLM 代理**（Aider、OpenHands、Open Interpreter、SWE-agent 和 gptme 均基于 LiteLLM，可直接连接 —— 但如果你自行维护 LiteLLM 代理）：

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # openai/ 前缀 → 兼容 OpenAI 的路由
      api_base: https://router.pleum.ai/v1           # 请勿追加 /chat/completions
      api_key: os.environ/PLEUM_API_KEY
```

---

## 贡献指南

已经把 PleumRouter 接入了此处未列出的工具？欢迎提交 PR —— 附上一份**经过测试**的配置片段（基础 URL、密钥环境变量、模型 ID 格式，以及任何注意事项）即可。

## 许可证

[MIT](LICENSE)
