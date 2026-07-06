<div align="center">

# Kuinka käyttää PleumRouteria

**Yksi API-avain 200+ tekoälymallille — OpenAI-yhteensopiva, laskutus KRW:ssä.**

[Verkkosivusto](https://pleum.ai) · [Dokumentaatio](https://pleum.ai/docs) · [Mallit](https://pleum.ai/models) · [Playground](https://pleum.ai/playground)

[![npm](https://img.shields.io/npm/v/pleumrouter?label=pleum%20CLI)](https://www.npmjs.com/package/pleumrouter)
[![models](https://img.shields.io/badge/models-210%2B-8A2BE2)](https://pleum.ai/models)
[![providers](https://img.shields.io/badge/providers-18-blue)](https://pleum.ai/models)

[English](README.md) · [한국어](README.ko.md) · [日本語](README.ja.md) · [简体中文](README.zh-CN.md) · [繁體中文](README.zh-TW.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt-BR.md) · [Русский](README.ru.md) · [Italiano](README.it.md) · [Nederlands](README.nl.md) · [Polski](README.pl.md) · [Türkçe](README.tr.md) · [Tiếng Việt](README.vi.md) · [ไทย](README.th.md) · [Bahasa Indonesia](README.id.md) · [Bahasa Melayu](README.ms.md) · [हिन्दी](README.hi.md) · [বাংলা](README.bn.md) · [اردو](README.ur.md) · [العربية](README.ar.md) · [فارسی](README.fa.md) · [עברית](README.he.md) · [Ελληνικά](README.el.md) · [Українська](README.uk.md) · [Čeština](README.cs.md) · [Slovenčina](README.sk.md) · [Română](README.ro.md) · [Magyar](README.hu.md) · [Svenska](README.sv.md) · [Dansk](README.da.md) · [Norsk](README.nb.md) · Suomi · [Български](README.bg.md) · [Hrvatski](README.hr.md) · [Српски](README.sr.md) · [Slovenščina](README.sl.md) · [Lietuvių](README.lt.md) · [Latviešu](README.lv.md) · [Eesti](README.et.md) · [Kiswahili](README.sw.md) · [தமிழ்](README.ta.md) · [తెలుగు](README.te.md) · [ខ្មែរ](README.km.md) · [မြန်မာ](README.my.md) · [नेपाली](README.ne.md) · [Монгол](README.mn.md) · [ქართული](README.ka.md) · [Հայերեն](README.hy.md) · [አማርኛ](README.am.md) · [Filipino](README.tl.md) · [Català](README.ca.md) · [Íslenska](README.is.md)

</div>

PleumRouter on tekoälyn yhdyskäytävä: yksi avain (`plm_…`), yksi perus-URL, yli 210 mallia 18 palveluntarjoajalta — GPT, Claude, Gemini, DeepSeek, Qwen, EXAONE ja muita. Se puhuu **OpenAI Chat Completions** -, **Anthropic Messages** - ja **OpenAI Responses** -rajapintoja, joten lähes jokainen koodausagentti, IDE-laajennus ja SDK yhdistyy yhden rivin asetusmuutoksella. Teksti, upotukset, kuvat, puhe ja video kulkevat kaikki saman avaimen kautta.

Tämä repositorio kokoaa **vahvistettuja integraatioreseptejä**. Jokainen alla oleva koodinpätkä on testattu live-yhdyskäytävää vasten.

## Aloittaminen

1. [Rekisteröidy](https://pleum.ai/signup) → Dashboard → **API Keys** → luo avain (alkaa merkinnällä `plm_`).
2. Osoita työkalusi perus-URL:ään:

```bash
export OPENAI_API_BASE=https://router.pleum.ai/v1
export OPENAI_API_KEY=plm_xxxxxxxxxxxxxxxx
# Jotkin agentit (OpenCode, Crush) lukevat PLEUM_API_KEY — sama avain, aseta molemmat.
export PLEUM_API_KEY=plm_xxxxxxxxxxxxxxxx
```

3. Savutesti:

```bash
curl https://router.pleum.ai/v1/models \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx"
```

Saat ₩1 000 ilmaista krediittiä rekisteröitymisen yhteydessä ja ₩5 000 bonuksen ensimmäisestä lataamisesta.

## Integraatiot

| Kategoria | Työkalut |
|---|---|
| [⚡ Yhden komennon käynnistin](#-pleum-cli--nopea-tie) | `pleum` CLI |
| [🤖 Pääteikkunan koodausagentit](#-pääteikkunan--cli-agentit) | Claude Code, Codex CLI, Aider, OpenCode, Crush, Goose, OpenHands |
| [🖥 IDE- / graafiset agentit](#-ide--graafiset-agentit) | Cline, Roo Code, Kilo Code, Cursor, Continue.dev, Zed |
| [📦 SDK:t](#-sdkt) | OpenAI SDK (Python/JS), Anthropic SDK |
| [🎨 Multimodaali-API](#-multimodaali--kuva--ääni--video) | Kuvat, TTS, STT, video, upotukset |
| [🔌 Kaikki muu](#-muut-agentit) | OpenRouter-tyyliset tunnisteet, LiteLLM-välityspalvelin, 15+ muuta agenttia |

---

## ⚡ pleum CLI — nopea tie

Virallinen CLI käynnistää suosikkiagenttisi valmiiksi kytkettynä PleumRouteriin. Asetustiedostoihin ei kosketa.

```bash
npm install -g pleumrouter        # tai: curl -fsSL https://router.pleum.ai/install | sh

pleum login                       # kirjautuminen selaimessa, avain luodaan & tallennetaan automaattisesti
pleum launch claude --model claude-sonnet-4
pleum launch codex  --model gpt-4.1
pleum run gpt-4.1                 # pääteikkunan chat-REPL
pleum models                      # listaa kaikki mallit hinnoitteluineen
```

Automaattikäynnistys tuettu: `claude` · `aider` · `codex` · `goose` · `openhands` (lisäksi asetuspätkät työkaluille `opencode` · `crush`). Olemassa olevia työkaluasetuksiasi ei koskaan muokata.

---

## 🤖 Pääteikkunan / CLI-agentit

### Claude Code (Anthropic-yhteensopiva)

Claude Code ja Claude Agent SDK -työkalut yhdistyvät Anthropic-yhteensopivan `/v1/messages`-päätepisteen kautta.

```bash
# ANTHROPIC_BASE_URL on JUURI (ei /v1) — CLI lisää /v1/messages itse.
export ANTHROPIC_BASE_URL=https://router.pleum.ai
# Virallinen CLI suosii muuttujaa ANTHROPIC_API_KEY; aseta molemmat varmuuden vuoksi.
export ANTHROPIC_API_KEY=plm_xxxxxxxxxxxxxxxx
export ANTHROPIC_AUTH_TOKEN=plm_xxxxxxxxxxxxxxxx

claude --model anthropic/gpt-4.1
```

> ⚠️ Älä laita `/v1`-merkintää muuttujaan `ANTHROPIC_BASE_URL` — siitä tulee `/v1/v1/messages`, ja se epäonnistuu. Työkalukutsut ja striimaus toimivat päästä päähän, vaikka reititys tapahtuisi OpenAI-yhteensopiviin malleihin.

### Codex CLI (Responses API)

Codex yhdistyy OpenAI Responses -rajapinnan (`/v1/responses`) kautta; Chat Completions -polku poistettiin Codexista helmikuussa 2026.

```toml
# ~/.codex/config.toml
# model / model_provider ovat dokumentin juuriavaimia (oltava [table]-taulukon yläpuolella).
model = "gpt-4.1"
model_provider = "pleum"

[model_providers.pleum]
name = "PleumRouter"
base_url = "https://router.pleum.ai/v1"   # Codex lisää /responses → /v1/responses
env_key = "PLEUM_API_KEY"
wire_api = "responses"                      # Codex tukee vain Responses-rajapintaa
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
// opencode.json   (tai: /connect → Other)
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

# Goose / OpenHands: lisää mallitunnisteen eteen etuliite openai/
#   model = openai/gpt-4.1
```

### Gemini CLI

Ylävirran Gemini CLI:llä on heikko tuki ulkoisille OpenAI-yhteensopiville päätepisteille; saatat tarvita OpenAI-yhteensopivan kääreen tai haarautuman.

---

## 🖥 IDE- / graafiset agentit

### Cline · Roo Code · Kilo Code · Cursor

Valitse palveluntarjoajaksi **OpenAI Compatible** (tai **Custom OpenAI**) ja liitä:

```text
API Provider   →  OpenAI Compatible
Base URL       →  https://router.pleum.ai/v1
API Key        →  plm_xxxxxxxxxxxxxxxx
Model ID       →  gpt-4.1
```

> ⚠️ Käytä aina **OpenAI Compatible -paikkaa** — omistettu OpenRouter-kohta on kovakoodattu osoitteeseen openrouter.ai ja epäonnistuu. **Cursor** vaatii merkinnän `/v1` perus-URL:ssä ja ei-tyhjän avainkentän. **Kilo Codella** on tunnettu ongelma (#681), jossa mukautettua perus-URL:ää ei välitetä mallilistaukseen — syötä mallitunniste käsin.

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

Kun `model: AUTODETECT` on asetettu, Continue hakee mallilistan automaattisesti.

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

Kenttänimet voivat vaihdella Zed-version mukaan — tarkista Zedin dokumentaatiosta.

---

## 📦 SDK:t

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
    base_url="https://router.pleum.ai",   # juuri, ei /v1 — SDK lisää /v1/messages
    api_key="plm_xxxxxxxxxxxxxxxx",
)

msg = client.messages.create(
    model="gpt-4.1",                      # mikä tahansa PleumRouter-malli toimii
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello!"}],
)
print(msg.content)
```

---

## 🎨 Multimodaali — kuva · ääni · video

Kaikki modaliteetit ovat OpenAI-yhteensopivia HTTP-päätepisteitä saman avaimen alla. Valitse modaliteettia tukeva malli osoitteesta [`GET /v1/models`](https://pleum.ai/models).

```bash
# Kuvan generointi
curl https://router.pleum.ai/v1/images/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a red bicycle", "n": 1, "size": "1024x1024" }'

# Tekstistä puheeksi (palauttaa äänitavuja; kustannus X-Cost-Krw-otsikossa)
curl https://router.pleum.ai/v1/audio/speech \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "input": "Hello there", "voice": "alloy" }' --output speech.mp3

# Puheesta tekstiksi (multipart-lataus)
curl https://router.pleum.ai/v1/audio/transcriptions \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -F model=MODEL_ID -F file=@audio.mp3

# Videon generointi on asynkroninen: POST palauttaa job_id:n, sitten pollaa GET /v1/jobs/{job_id}
curl https://router.pleum.ai/v1/video/generations \
  -H "Authorization: Bearer plm_xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{ "model": "MODEL_ID", "prompt": "a drone shot over a forest" }'
```

### API-pinta

| Päätepiste | Protokolla |
|---|---|
| `POST /v1/chat/completions` | OpenAI Chat Completions (striimaus, työkalut, näkö) |
| `POST /v1/messages` | Anthropic Messages (Claude Code, Agent SDK) |
| `POST /v1/responses` | OpenAI Responses (Codex CLI) |
| `POST /v1/embeddings` | OpenAI Embeddings |
| `POST /v1/images/generations` | Kuvan generointi |
| `POST /v1/audio/speech` · `POST /v1/audio/transcriptions` | TTS · STT |
| `POST /v1/video/generations` → `GET /v1/jobs/{id}` | Asynkroninen video |
| `GET /v1/models` | Mallikatalogi (julkinen) |
| `GET /v1/credits` | Saldo |

---

## 🔌 Muut agentit

Useimmat tähän listaamattomat agentit toimivat samalla tavalla — aseta OpenAI-yhteensopiva perus-URL:

**OpenHands · Open Interpreter · SWE-agent · Qwen Code · MetaGPT · GPT-Pilot · ChatDev · Tabby (chat) · Dyad · Plandex · bolt.diy · Forge · Kimi CLI · gptme · Letta** ja muita.

Anthropic-yhteensopivan `/v1/messages`-rajapinnan kautta: myös **claude-code-router** yhdistyy muuttujalla `ANTHROPIC_BASE_URL`.

**Mallitunnisteet**: löydät ne osoitteesta `GET /v1/models` tai [mallisivulta](https://pleum.ai/models). Cline, Continue, OpenCode ja muut hakevat listan automaattisesti. OpenRouter-muotoiset tunnisteet (`openai/gpt-5.5`) muunnetaan automaattisesti.

**LiteLLM-välityspalvelin** (Aider, OpenHands, Open Interpreter, SWE-agent ja gptme perustuvat LiteLLM:ään ja yhdistyvät suoraan — mutta jos ylläpidät LiteLLM-välityspalvelinta):

```yaml
# litellm config.yaml
model_list:
  - model_name: pleum-gpt-4.1
    litellm_params:
      model: openai/gpt-4.1                          # openai/-etuliite → OpenAI-yhteensopiva reitti
      api_base: https://router.pleum.ai/v1           # ÄLÄ lisää perään /chat/completions
      api_key: os.environ/PLEUM_API_KEY
```

---

## Osallistuminen

Saitko PleumRouterin toimimaan työkalulla, jota ei ole listattu tässä? PR:t ovat tervetulleita — lisää osio **testatulla** asetuspätkällä (perus-URL, avaimen ympäristömuuttuja, mallitunnisteen muoto ja mahdolliset sudenkuopat).

## Lisenssi

[MIT](LICENSE)
