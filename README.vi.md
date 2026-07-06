<div align="center">

# Cách sử dụng PleumRouter

**Một API key cho hơn 200 mô hình AI — tương thích OpenAI, thanh toán bằng KRW.**

[Trang chủ](https://pleum.ai) · [Tài liệu](https://pleum.ai/docs) · [Mô hình](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · Tiếng Việt · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter là một cổng AI (AI gateway): một key duy nhất (`plm_…`), một base URL duy nhất, hơn 210 mô hình từ 18 nhà cung cấp — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE và nhiều hơn nữa. Nó hỗ trợ **OpenAI Chat Completions**, **Anthropic Messages**, và **OpenAI Responses**, vì vậy hầu như mọi coding agent, plugin IDE, và SDK đều có thể kết nối chỉ với một dòng cấu hình thay đổi. Văn bản, embeddings, hình ảnh, giọng nói và video đều chạy qua cùng một key.

Repo này tổng hợp các **công thức tích hợp đã được xác minh**. Mọi đoạn mã bên dưới đều đã được kiểm thử trên gateway thực tế (live gateway).

## Bắt đầu

1. [Đăng ký](https://pleum.ai/signup) → Dashboard → **API Keys** → cấp một key (bắt đầu bằng `plm_`).
2. Trỏ công cụ của bạn đến base URL:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Một số agent (OpenCode, Crush) đọc PLEUM_API_KEY — cùng một key, đặt cả hai.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Kiểm tra nhanh (smoke test):

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Bạn nhận được ₩1.000 tín dụng miễn phí khi đăng ký và ₩5.000 tiền thưởng cho lần nạp tiền đầu tiên.

## Tích hợp

| Danh mục | Công cụ |
|---|---|
| [⚡ Trình khởi chạy một lệnh](#-pleum-cli--con-đường-nhanh-nhất) | CLI `pleum` |
| [🤖 Coding agent chạy trên terminal](#-agent-terminal--cli) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 Agent IDE / GUI](#-agent-ide--gui) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK](#-sdk) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 API đa phương thức](#-đa-phương-thức--hình-ảnh--âm-thanh--video) | Hình ảnh, TTS, STT, Video, Embeddings |
| [🔌 Tất cả các agent khác](#-các-agent-khác) | ID theo kiểu OpenRouter, proxy LiteLLM, hơn 15 agent khác |

---

## ⚡ pleum CLI — con đường nhanh nhất

CLI chính thức khởi chạy agent yêu thích của bạn đã được kết nối sẵn với PleumRouter. Không cần chạm vào bất kỳ file cấu hình nào.

```bash
npm install -g pleumrouter        # hoặc: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # đăng nhập qua trình duyệt, key được tự động cấp & lưu
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # REPL chat trên terminal
pleum models                      # liệt kê tất cả mô hình kèm giá
```

Hỗ trợ tự động khởi chạy: `claude` · `aider` · `codex` · `goose` · `openhands` (cùng với các đoạn cấu hình cho `opencode` · `crush`). Cấu hình công cụ hiện có của bạn sẽ không bao giờ bị thay đổi.

---

## 🤖 Agent Terminal / CLI

### Claude Code (tương thích Anthropic)

Claude Code và các công cụ Claude Agent SDK kết nối qua endpoint `/v1/messages` tương thích Anthropic.

```bash
# ANTHROPIC_BASE_URL là ROOT (không có /v1) — CLI sẽ tự thêm /v1/messages.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# CLI chính thức ưu tiên ANTHROPIC_API_KEY; đặt cả hai để chắc chắn.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ **Không** đặt `/v1` trong `ANTHROPIC_BASE_URL` — nó sẽ trở thành `/v1/v1/messages` và thất bại. Tool calls và streaming hoạt động xuyên suốt, ngay cả khi được định tuyến đến các mô hình tương thích OpenAI.

### Codex CLI (Responses API)

Codex kết nối qua OpenAI Responses API (`/v1/responses`); đường dẫn Chat Completions đã bị loại bỏ khỏi Codex vào tháng 2 năm 2026.

```toml
# ~/.codex/config.toml
# model / model_provider là các khóa ở gốc tài liệu (phải nằm phía trên [table]).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex tự thêm /responses → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex chỉ hỗ trợ Responses API
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
// opencode.json   (hoặc: /connect → Other)
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

# Goose / OpenHands: thêm tiền tố openai/ vào model id
#   model = openai/gpt-4.1
```

### Gemini CLI

Gemini CLI gốc có hỗ trợ yếu đối với các endpoint tương thích OpenAI bên ngoài; bạn có thể cần một wrapper hoặc bản fork tương thích OpenAI.

---

## 🖥 Agent IDE / GUI

### Cline · Roo Code · Kilo Code · Cursor

Chọn **OpenAI Compatible** (hoặc **Custom OpenAI**) làm provider và dán:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Luôn sử dụng **ô OpenAI Compatible** — mục nhập OpenRouter chuyên dụng được hardcode đến openrouter.ai và sẽ thất bại. **Cursor** yêu cầu `/v1` trong base URL và trường key không được để trống. **Kilo Code** có một lỗi đã biết (#681) khiến base URL tùy chỉnh không được truyền vào khi liệt kê mô hình — hãy nhập model ID theo cách thủ công.

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

Với `model: AUTODETECT`, Continue sẽ tự động lấy danh sách mô hình.

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

Tên trường có thể khác nhau tùy phiên bản Zed — hãy kiểm tra tài liệu của Zed.

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
    base_url="https://router.pleum.ai",   # root, không có /v1 — SDK tự thêm /v1/messages
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # bất kỳ mô hình PleumRouter nào cũng hoạt động
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Đa phương thức — hình ảnh · âm thanh · video

Tất cả các phương thức đều là endpoint HTTP tương thích OpenAI trên cùng một key. Chọn một mô hình hỗ trợ phương thức đó từ [`GET /v1/models`](https://pleum.ai/models).

```bash
# Tạo hình ảnh
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Chuyển văn bản thành giọng nói (trả về dữ liệu audio; chi phí trong header X-Cost-Krw)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Chuyển giọng nói thành văn bản (tải lên dạng multipart)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# Tạo video là bất đồng bộ: POST trả về job_id, sau đó poll GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### Bề mặt API

| Endpoint | Giao thức |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (streaming, tools, vision) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Tạo hình ảnh |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Video bất đồng bộ |
| `GET /v1/models` | Danh mục mô hình (công khai) |
| `GET /v1/credits` | Số dư |

---

## 🔌 Các agent khác

Hầu hết các agent không được liệt kê ở đây đều hoạt động theo cùng một cách — chỉ cần đặt base URL tương thích OpenAI:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** và nhiều hơn nữa.

Qua giao thức tương thích Anthropic `/v1/messages`: **claude-code-router** cũng kết nối được bằng `ANTHROPIC_BASE_URL`.

**ID mô hình**: tìm chúng tại `GET /v1/models` hoặc trên [trang mô hình](https://pleum.ai/models). Cline, Continue, OpenCode và các công cụ khác sẽ tự động lấy danh sách. ID theo định dạng OpenRouter (`openai/gpt-5.5`) được tự động chuyển đổi.

**Proxy LiteLLM** (Aider, OpenHands, Open Interpreter, SWE-agent và gptme đều dựa trên LiteLLM và kết nối trực tiếp — nhưng nếu bạn vẫn dùng một proxy LiteLLM):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # tiền tố openai/ → tuyến tương thích OpenAI
      api_base: https://router.pleum.ai/v1           # KHÔNG thêm /chat/completions
      api_key: os.environ/PLEUM_API_KEY
```

---

## Đóng góp

Bạn đã dùng PleumRouter thành công với một công cụ chưa được liệt kê ở đây? Rất hoan nghênh PR — hãy thêm một mục với đoạn cấu hình đã **được kiểm thử** (base URL, biến môi trường key, định dạng model ID, và bất kỳ lưu ý nào cần biết).

## Giấy phép

[MIT](LICENSE)
