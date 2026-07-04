<div align="center">

# Awesome PleumRouter

**API 키 하나로 200개+ AI 모델 — OpenAI 호환, 원화(₩) 과금.**

[웹사이트](https://pleum.ai) · [문서](https://pleum.ai/docs) · [모델](https://pleum.ai/models) · [플레이그라운드](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

한국어 | [English](README.md)

</div>

PleumRouter는 AI 게이트웨이입니다. 키 하나(`plm_…`), base URL 하나로 18개 프로바이더의 210개+ 모델을 씁니다 — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE 등. **OpenAI Chat Completions**, **Anthropic Messages**, **OpenAI Responses** 세 프로토콜을 모두 지원해 거의 모든 코딩 에이전트·IDE 플러그인·SDK가 설정 한 줄로 붙습니다. 텍스트·임베딩·이미지·음성·영상까지 같은 키로 동작합니다.

이 리포는 **검증된 통합 레시피** 모음입니다. 아래 모든 스니펫은 라이브 게이트웨이에서 테스트되었습니다.

## 시작하기

1. [가입](https://pleum.ai/signup) → 대시보드 → **API 키**에서 키 발급 (`plm_`으로 시작).
2. 도구를 base URL로 연결:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# 일부 에이전트(OpenCode, Crush)는 PLEUM_API_KEY를 읽음 — 같은 키를 둘 다 설정.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. 동작 확인:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

가입 시 ₩1,000, 첫 충전 시 ₩5,000 보너스를 드립니다.

## 통합 목록

| 분류 | 도구 |
|---|---|
| [⚡ 원커맨드 런처](#-pleum-cli--가장-빠른-길) | `pleum` CLI |
| [🤖 터미널 코딩 에이전트](#-터미널--cli-에이전트) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE / GUI 에이전트](#-ide--gui-에이전트) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK](#-sdk) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 멀티모달 API](#-멀티모달--이미지--음성--영상) | 이미지, TTS, STT, 영상, 임베딩 |
| [🔌 그 외 전부](#-더-많은-에이전트) | OpenRouter 형식 ID, LiteLLM proxy, 15개+ 에이전트 |

---

## ⚡ pleum CLI — 가장 빠른 길

공식 CLI가 쓰던 에이전트를 PleumRouter에 연결된 상태로 바로 실행합니다. 기존 설정 파일은 건드리지 않습니다.

```bash
npm install -g pleumrouter        # 또는: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # 브라우저 로그인, 키 자동 발급·저장
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # 터미널 채팅 REPL
pleum models                      # 전체 모델·가격 목록
```

자동 실행 지원: `claude` · `aider` · `codex` · `goose` · `openhands` (`opencode` · `crush`는 설정 스니펫 안내).

---

## 🤖 터미널 / CLI 에이전트

### Claude Code (Anthropic 호환)

Claude Code와 Claude Agent SDK 기반 도구는 Anthropic 호환 `/v1/messages` 엔드포인트로 붙습니다.

```bash
# ANTHROPIC_BASE_URL은 루트(/v1 없음) — CLI가 /v1/messages를 알아서 덧붙임.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# 공식 CLI는 ANTHROPIC_API_KEY를 먼저 읽으므로 둘 다 설정하는 편이 안전.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ `ANTHROPIC_BASE_URL`에 `/v1`을 넣지 마세요 — `/v1/v1/messages`가 되어 실패합니다. OpenAI 호환 모델로 라우팅해도 함수호출·스트리밍까지 동작합니다.

### Codex CLI (Responses API)

Codex는 OpenAI Responses API(`/v1/responses`)로 직접 붙습니다 (2026년 2월 Chat Completions 경로 제거).

```toml
# ~/.codex/config.toml
# model / model_provider는 문서 루트 키 ([table]보다 위에 있어야 함).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex가 /responses를 덧붙임 → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex는 Responses API만 지원
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
// opencode.json   (또는: /connect → Other)
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

# Goose / OpenHands: 모델 ID 앞에 openai/ 접두사 필요
#   model = openai/gpt-4.1
```

### Gemini CLI

순정 Gemini CLI는 외부 OpenAI 호환 엔드포인트 직결성이 낮아, OpenAI 호환 래퍼/포크를 거쳐야 할 수 있습니다.

---

## 🖥 IDE / GUI 에이전트

### Cline · Roo Code · Kilo Code · Cursor

provider로 **OpenAI Compatible**(또는 **Custom OpenAI**)을 고르고 아래 값을 입력:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ 반드시 **OpenAI Compatible 슬롯**을 쓰세요 — OpenRouter 전용 항목은 openrouter.ai로 하드코딩되어 실패합니다. **Cursor**는 base URL에 `/v1`까지 포함하고 키 칸을 비우면 안 됩니다. **Kilo Code**는 커스텀 base URL이 모델 목록 조회에 전달되지 않는 알려진 이슈(#681)가 있어 모델 ID를 직접 입력하세요.

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

`model: AUTODETECT`면 모델 목록을 자동으로 불러옵니다.

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

버전에 따라 필드명이 다를 수 있으니 Zed 문서를 확인하세요.

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
    messages=[{"role": "user", "content": "안녕!"}],
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
  messages: [{ role: "user", content: "안녕!" }],
});
console.log(resp.choices[0].message.content);
```

### Anthropic SDK

```python
import anthropic

client = anthropic.Anthropic(
    base_url="https://router.pleum.ai",   # 루트, /v1 없음 — SDK가 /v1/messages를 덧붙임
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # PleumRouter의 어떤 모델이든 동작
    max_tokens=1024,
    messages=[{"role": "user", "content": "안녕!"}],
)
print(msg.content)
```

---

## 🎨 멀티모달 — 이미지 · 음성 · 영상

모든 모달리티가 같은 키의 OpenAI 호환 HTTP 엔드포인트입니다. 모달리티를 지원하는 모델은 [`GET /v1/models`](https://pleum.ai/models)에서 확인하세요.

```bash
# 이미지 생성
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# TTS (오디오 바이트 반환; 비용은 X-Cost-Krw 헤더)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# STT (multipart 업로드)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# 영상 생성은 비동기: POST가 job_id 반환 → GET /v1/jobs/{job_id} 폴링
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### API 목록

| 엔드포인트 | 프로토콜 |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (스트리밍·도구·비전) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | 이미지 생성 |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | 비동기 영상 |
| `GET /v1/models` | 모델 카탈로그 (공개) |
| `GET /v1/credits` | 잔액 조회 |

---

## 🔌 더 많은 에이전트

여기 없는 에이전트도 대부분 같은 방식입니다 — OpenAI 호환 base URL만 설정:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby(채팅) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** 등.

Anthropic 호환(`/v1/messages`)으로는 **claude-code-router**도 `ANTHROPIC_BASE_URL`로 붙습니다.

**모델 ID**: `GET /v1/models` 또는 [모델 페이지](https://pleum.ai/models)에서 확인. Cline·Continue·OpenCode 등은 목록을 자동으로 불러옵니다. OpenRouter 형식(`openai/gpt-5.5`)으로 보내도 자동 변환됩니다.

**LiteLLM proxy** (Aider·OpenHands·Open Interpreter·SWE-agent·gptme는 LiteLLM 기반이라 base URL 직결이 되지만, 기존 LiteLLM proxy를 유지한다면):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # openai/ 접두사 → OpenAI 호환 라우트
      api_base: https://router.pleum.ai/v1           # /chat/completions를 덧붙이지 말 것
      api_key: os.environ/PLEUM_API_KEY
```

---

## 기여하기

여기 없는 도구에 PleumRouter를 연결하셨나요? PR 환영합니다 — **실제 테스트한** 설정 스니펫(base URL, 키 env, 모델 ID 형식, 함정)과 함께 섹션을 추가해 주세요.

## 라이선스

[MIT](LICENSE)
