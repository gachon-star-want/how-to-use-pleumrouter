<div align="center">

# Comment utiliser PleumRouter

**Une seule clé API pour plus de 200 modèles d'IA — compatible OpenAI, facturé en KRW.**

[Site web](https://pleum.ai) · [Docs](https://pleum.ai/docs) · [Modèles](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · Français · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · [Suomi](README.fi.md) · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter est une passerelle IA (gateway) : une seule clé (`plm_…`), une seule URL de base, plus de 210 modèles provenant de 18 fournisseurs — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE et bien d'autres. Elle prend en charge **OpenAI Chat Completions**, **Anthropic Messages** et **OpenAI Responses**, si bien que la quasi-totalité des agents de codage, plugins d'IDE et SDK s'y connectent avec un simple changement de configuration en une ligne. Texte, embeddings, image, audio et vidéo passent tous par la même clé.

Ce dépôt rassemble des **recettes d'intégration vérifiées**. Chaque extrait ci-dessous est testé sur la passerelle en production.

## Pour commencer

1. [Inscrivez-vous](https://pleum.ai/signup) → Tableau de bord → **API Keys** → générez une clé (commence par `plm_`).
2. Pointez votre outil vers l'URL de base :

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Certains agents (OpenCode, Crush) lisent PLEUM_API_KEY — même clé, définissez les deux.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Test de bon fonctionnement :

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Vous recevez ₩1 000 de crédit gratuit à l'inscription et un bonus de ₩5 000 lors de votre première recharge.

## Intégrations

| Catégorie | Outils |
|---|---|
| [⚡ Lanceur en une commande](#-pleum-cli--le-chemin-le-plus-rapide) | CLI `pleum` |
| [🤖 Agents de codage en terminal](#-agents-terminal--cli) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 Agents IDE / GUI](#-agents-ide--gui) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDKs](#-sdks) | SDK OpenAI (Python/JS), SDK Anthropic |
| [🎨 API multimodale](#-multimodal--image--audio--vidéo) | Images, TTS, STT, Vidéo, Embeddings |
| [🔌 Tout le reste](#-plus-dagents) | IDs façon OpenRouter, proxy LiteLLM, 15+ autres agents |

---

## ⚡ pleum CLI — le chemin le plus rapide

Le CLI officiel lance votre agent préféré déjà configuré pour PleumRouter. Aucun fichier de configuration n'est modifié.

```bash
npm install -g pleumrouter        # ou : curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # connexion via navigateur, clé générée & enregistrée automatiquement
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # REPL de chat en terminal
pleum models                      # liste tous les modèles avec leurs tarifs
```

Lancement automatique pris en charge pour : `claude` · `aider` · `codex` · `goose` · `openhands` (plus des extraits de configuration pour `opencode` · `crush`). Les configurations existantes de vos outils ne sont jamais modifiées.

---

## 🤖 Agents terminal / CLI

### Claude Code (compatible Anthropic)

Claude Code et les outils du Claude Agent SDK se connectent via le point de terminaison compatible Anthropic `/v1/messages`.

```bash
# ANTHROPIC_BASE_URL est la RACINE (sans /v1) — le CLI ajoute lui-même /v1/messages.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# Le CLI officiel privilégie ANTHROPIC_API_KEY ; définissez les deux par sécurité.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ Ne mettez **surtout pas** `/v1` dans `ANTHROPIC_BASE_URL` — cela donnerait `/v1/v1/messages` et échouerait. Les appels d'outils (tool calls) et le streaming fonctionnent de bout en bout, même lorsqu'ils sont routés vers des modèles compatibles OpenAI.

### Codex CLI (API Responses)

Codex se connecte via l'API OpenAI Responses (`/v1/responses`) ; la voie Chat Completions a été retirée de Codex en février 2026.

```toml
# ~/.codex/config.toml
# model / model_provider sont des clés à la racine du document (doivent être au-dessus de la [table]).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex ajoute /responses → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex ne prend en charge que l'API Responses
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
// opencode.json   (ou : /connect → Other)
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

# Goose / OpenHands : préfixez l'id du modèle par openai/
#   model = openai/gpt-4.1
```

### Gemini CLI

Le Gemini CLI officiel prend mal en charge les points de terminaison externes compatibles OpenAI ; un wrapper ou un fork compatible OpenAI peut être nécessaire.

---

## 🖥 Agents IDE / GUI

### Cline · Roo Code · Kilo Code · Cursor

Choisissez **OpenAI Compatible** (ou **Custom OpenAI**) comme fournisseur et collez :

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Utilisez toujours l'**emplacement OpenAI Compatible** — l'entrée dédiée OpenRouter est codée en dur vers openrouter.ai et échouera. **Cursor** exige `/v1` dans l'URL de base et un champ de clé non vide. **Kilo Code** a un problème connu (#681) où l'URL de base personnalisée n'est pas transmise à la liste des modèles — saisissez l'id du modèle manuellement.

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

Avec `model: AUTODETECT`, Continue récupère automatiquement la liste des modèles.

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

Les noms de champs peuvent varier selon la version de Zed — consultez la documentation de Zed.

---

## 📦 SDKs

### SDK OpenAI (Python)

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

### SDK OpenAI (JavaScript / TypeScript)

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

### SDK Anthropic

```python
import anthropic

client = anthropic.Anthropic(
    base_url="https://router.pleum.ai",   # racine, sans /v1 — le SDK ajoute /v1/messages
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # n'importe quel modèle PleumRouter fonctionne
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Multimodal — image · audio · vidéo

Toutes les modalités sont des points de terminaison HTTP compatibles OpenAI, sous la même clé. Choisissez un modèle qui prend en charge la modalité via [`GET /v1/models`](https://pleum.ai/models).

```bash
# Génération d'image
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Synthèse vocale / text-to-speech (renvoie des octets audio ; coût dans l'en-tête X-Cost-Krw)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Reconnaissance vocale / speech-to-text (upload multipart)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# La génération vidéo est asynchrone : le POST renvoie un job_id, puis interrogez GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### Surface de l'API

| Point de terminaison | Protocole |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (streaming, outils, vision) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Génération d'images |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Vidéo asynchrone |
| `GET /v1/models` | Catalogue de modèles (public) |
| `GET /v1/credits` | Solde |

---

## 🔌 Plus d'agents

La plupart des agents non listés ici fonctionnent de la même manière — définissez l'URL de base compatible OpenAI :

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** et d'autres encore.

Via le point de terminaison compatible Anthropic `/v1/messages` : **claude-code-router** se connecte lui aussi avec `ANTHROPIC_BASE_URL`.

**IDs de modèles** : trouvez-les via `GET /v1/models` ou sur la [page des modèles](https://pleum.ai/models). Cline, Continue, OpenCode et d'autres récupèrent la liste automatiquement. Les IDs au format OpenRouter (`openai/gpt-5.5`) sont convertis automatiquement.

**Proxy LiteLLM** (Aider, OpenHands, Open Interpreter, SWE-agent et gptme reposent sur LiteLLM et se connectent directement — mais si vous maintenez un proxy LiteLLM) :

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # préfixe openai/ → route compatible OpenAI
      api_base: https://router.pleum.ai/v1           # NE PAS ajouter /chat/completions
      api_key: os.environ/PLEUM_API_KEY
```

---

## Contribuer

Vous avez réussi à faire fonctionner PleumRouter avec un outil qui ne figure pas ici ? Les PR sont les bienvenues — ajoutez une section avec un extrait de configuration **testé** (URL de base, variable d'environnement de la clé, format de l'id du modèle, et les éventuels pièges).

## Licence

[MIT](LICENSE)
