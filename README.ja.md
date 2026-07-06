<div align="center">

# PleumRouterの使い方

**200以上のAIモデルを1つのAPIキーで — OpenAI互換、KRW建て請求。**

[Website](https://pleum.ai) · [Docs](https://pleum.ai/docs) · [Models](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · 日本語 · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouterはAIゲートウェイです。1つのキー（`plm_…`）、1つのベースURL、18のプロバイダーから210以上のモデル — GPT、Claude、Gemini、DeepSeek、Qwen、EXAONEなど。**OpenAI Chat Completions**、**Anthropic Messages**、**OpenAI Responses**に対応しているため、ほぼすべてのコーディングエージェント、IDEプラグイン、SDKが1行の設定変更だけで接続できます。テキスト、埋め込み、画像、音声、動画もすべて同じキーで利用できます。

このリポジトリは**検証済みの統合レシピ**を集めたものです。以下のスニペットはすべて実際のゲートウェイに対してテスト済みです。

## はじめに

1. [サインアップ](https://pleum.ai/signup) → ダッシュボード → **API Keys** → キーを発行（`plm_`で始まります）。
2. ツールのベースURLを設定します。

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# 一部のエージェント（OpenCode、Crush）はPLEUM_API_KEYを読み取ります — 同じキーを両方に設定してください。
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. 動作確認：

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

サインアップで₩1,000の無料クレジット、初回チャージで₩5,000のボーナスがもらえます。

## 連携

| カテゴリー | ツール |
|---|---|
| [⚡ ワンコマンドランチャー](#-pleum-cli--高速な近道) | `pleum` CLI |
| [🤖 ターミナルコーディングエージェント](#-ターミナル--cliエージェント) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE / GUIエージェント](#-ide--guiエージェント) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK](#-sdk) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 マルチモーダルAPI](#-マルチモーダル--画像--音声--動画) | Images, TTS, STT, Video, Embeddings |
| [🔌 その他すべて](#-その他のエージェント) | OpenRouter形式のID、LiteLLMプロキシ、その他15以上のエージェント |

---

## ⚡ pleum CLI — 高速な近道

公式CLIは、お気に入りのエージェントをPleumRouterに接続済みの状態で起動します。設定ファイルには一切触れません。

```bash
npm install -g pleumrouter        # または: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # ブラウザでログイン、キーは自動発行・自動保存
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # ターミナルチャットREPL
pleum models                      # 全モデルと価格の一覧表示
```

自動起動に対応：`claude` · `aider` · `codex` · `goose` · `openhands`（加えて`opencode` · `crush`向けの設定スニペットあり）。既存のツール設定が変更されることは一切ありません。

---

## 🤖 ターミナル / CLIエージェント

### Claude Code（Anthropic互換）

Claude CodeおよびClaude Agent SDK系のツールは、Anthropic互換の`/v1/messages`エンドポイント経由で接続します。

```bash
# ANTHROPIC_BASE_URLはルート（/v1なし）— CLI側が自動的に/v1/messagesを付加します。
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# 公式CLIはANTHROPIC_API_KEYを優先します。念のため両方設定してください。
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ `ANTHROPIC_BASE_URL`に`/v1`を含め**ない**でください — `/v1/v1/messages`になってしまい失敗します。ツール呼び出しやストリーミングは、OpenAI互換モデルにルーティングされた場合でも最初から最後まで正常に動作します。

### Codex CLI（Responses API）

Codexは OpenAI Responses API（`/v1/responses`）経由で接続します。Chat Completionsのパスは2026年2月にCodexから削除されました。

```toml
# ~/.codex/config.toml
# model / model_provider はドキュメントルート直下のキーです（[table]より上に置く必要があります）。
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codexが/responsesを付加 → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # CodexはResponses APIのみサポート
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
// opencode.json   (または: /connect → Other)
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

# Goose / OpenHands: モデルIDの先頭にopenai/を付けてください
#   model = openai/gpt-4.1
```

### Gemini CLI

アップストリームのGemini CLIは、外部のOpenAI互換エンドポイントへの対応が弱いため、OpenAI互換ラッパーやフォーク版が必要になる場合があります。

---

## 🖥 IDE / GUIエージェント

### Cline · Roo Code · Kilo Code · Cursor

プロバイダーとして**OpenAI Compatible**（または**Custom OpenAI**）を選択し、以下を貼り付けます。

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ 必ず**OpenAI Compatibleスロット**を使用してください — 専用のOpenRouter欄はopenrouter.aiにハードコードされているため失敗します。**Cursor**はベースURLに`/v1`を含めることと、キー欄を空にしないことが必要です。**Kilo Code**には既知の不具合（#681）があり、カスタムベースURLがモデル一覧取得に渡されません — モデルIDは手動で入力してください。

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

`model: AUTODETECT`にしておくと、Continueが自動的にモデル一覧を取得します。

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

フィールド名はZedのバージョンによって異なる場合があります — Zedの公式ドキュメントを確認してください。

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
    base_url="https://router.pleum.ai",   # ルートのみ、/v1なし — SDKが/v1/messagesを付加
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # PleumRouterのどのモデルでも動作します
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 マルチモーダル — 画像・音声・動画

すべてのモダリティは、同じキーで使えるOpenAI互換のHTTPエンドポイントです。[`GET /v1/models`](https://pleum.ai/models)から該当モダリティに対応するモデルを選んでください。

```bash
# 画像生成
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# テキスト読み上げ（音声バイトを返却。コストはX-Cost-Krwヘッダーに記載）
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# 音声認識（マルチパートアップロード）
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# 動画生成は非同期です。POSTがjob_idを返し、その後GET /v1/jobs/{job_id}でポーリングします
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### APIサーフェス

| エンドポイント | プロトコル |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions（ストリーミング、ツール、vision対応） |
| `POST /v1/messages` | Anthropic Messages（Claude Code、Agent SDK） |
| `POST /v1/responses` | OpenAI Responses（Codex CLI） |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | 画像生成 |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS・STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | 非同期動画生成 |
| `GET /v1/models` | モデルカタログ（公開） |
| `GET /v1/credits` | 残高 |

---

## 🔌 その他のエージェント

ここに掲載されていないほとんどのエージェントも同じ方法で動作します — OpenAI互換のベースURLを設定してください。

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** など。

Anthropic互換の`/v1/messages`経由：**claude-code-router**も`ANTHROPIC_BASE_URL`で接続できます。

**モデルID**：`GET /v1/models`または[モデルページ](https://pleum.ai/models)で確認できます。Cline、Continue、OpenCodeなどは自動的に一覧を取得します。OpenRouter形式のID（`openai/gpt-5.5`）は自動的に変換されます。

**LiteLLMプロキシ**（Aider、OpenHands、Open Interpreter、SWE-agent、gptmeはLiteLLMベースで直接接続しますが、もしLiteLLMプロキシを利用している場合）：

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # openai/プレフィックス → OpenAI互換ルート
      api_base: https://router.pleum.ai/v1           # /chat/completionsは付加しないでください
      api_key: os.environ/PLEUM_API_KEY
```

---

## コントリビュート

ここに載っていないツールでPleumRouterを動かせましたか？PR歓迎です — **動作確認済み**の設定スニペット（ベースURL、キーの環境変数、モデルIDの形式、注意点）を添えたセクションを追加してください。

## ライセンス

[MIT](LICENSE)
