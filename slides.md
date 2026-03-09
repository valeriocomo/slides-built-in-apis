---
theme: apple-basic
title: Chrome Built-in AI APIs
info: |
  Chrome Built-in AI APIs
  On-device AI for the Web Platform
drawings:
  persist: false
transition: slide-left
layout: intro-image
image: '/images/cover.jpg'
---

# Introduzione alle Built‑in APIs

<div class="absolute bottom-10">
  <span class="font-700">
    Valerio Como
  </span>
</div>

<div class="abs-br m-6 text-xl">
  <a href="https://github.com/valeriocomo/slides-built-in-apis" target="_blank" class="slidev-icon-btn">
    <carbon:logo-github />
  </a>
</div>

---
src: ./pages/00-about-me.md
transition: fade
---

---
src: ./pages/01-agenda.md
transition: fade
---

---

## 1.1 Che cosa sono le Built‑in APIs?

- **Definizione**: API AI pre‑installate in Chrome che permettono di eseguire modelli di linguaggio, traduzione, riassunto e altro direttamente nel browser, senza bisogno di backend o network.
- **Obiettivi**:
  - Rendere l’IA più veloce, privata e accessibile.
  - Offrire un set di funzionalità di LLM che funzionano offline o con download on‑device.
- **Documentazione**: <https://developer.chrome.com/docs/ai/built-in>.

---

## 1.2 Come iniziare

- **Requisiti**: Chrome 110+ (stable) e flag di developer mode abilitati.
- **Setup rapido**:
  1. Attiva l’API **Prompt** nella console Chrome.
  2. Usa l’API JavaScript `chrome.ai` per fare chiamate immediate.
- **Guide introduttive**:
  - <https://developer.chrome.com/docs/ai/get-started>
  - <https://developer.chrome.com/docs/ai/client-side>

---

## 1.3 Client‑side vs Server‑side

- **Client‑side**: Modelli piccoli (es. Gemini Nano) sono scaricati sul dispositivo; garantisce privacy e latenza ridotta.
- **Server‑side**: Modelli più grandi, come Gemini Ultra, eseguiti sul server; usati per compiti complessi.
- **Mix**: L’API **Prompt** gestisce sessioni e può delegare a modelli più potenti in background.
- **Riferimento**: <https://developer.chrome.com/docs/ai/client-side>

---

# Descrizione delle API

---

## 2.1 API di riassunto

| API | Scopo | Documentazione |
|-----|-------|----------------|
| **Summarizer API** | Riassume testi lunghi con pochi prompt | <https://developer.chrome.com/docs/ai/summarizer-api> |
| **Scale Summarization** | Massimizza throughput con batch | <https://developer.chrome.com/docs/ai/scale-summarization> |

- **Esempio rapido**:
  ```js
  const result = await chrome.ai.summarizer.summarize({
    text: "Long article..."
  });
  console.log(result.summary);
  ```

---

## 2.2 API di traduzione e linguaggio

| API | Funzione | Documentazione |
|-----|----------|----------------|
| **Translator API** | Traduzione in tempo reale | <https://developer.chrome.com/docs/ai/translator-api> |
| **Language Detection** | Rileva lingua di input | <https://developer.chrome.com/docs/ai/language-detection> |

- **Uso**:
  ```js
  const lang = await chrome.ai.languageDetection.detect({
    text: "Bonjour"
  });
  const translation = await chrome.ai.translator.translate({
    sourceLanguage: lang,
    targetLanguage: "en",
    text: "Bonjour"
  });
  ```

---

## 2.3 Prompt‑based APIs

- **Prompt API**: Invia prompt multi‑pass con strutture complesse.
- **Structured Output**: Ottieni JSON ben formattato da Gemini.
- **Session Management**: Mantieni stato di conversazione.

```js
const session = chrome.ai.sessionManagement.create({
  model: "gemini-1.5-flash",
  cache: true
});
const response = await session.prompt({
  prompt: "Explain quantum entanglement in simple terms."
});
```

---

## 2.4 Writer‑like APIs

| API | Scopo | Documentazione |
|-----|-------|----------------|
| **Writer API** | Genera testo in stile editor | <https://developer.chrome.com/docs/ai/writer-api> |
| **Rewriter API** | Rephrase e miglioramento | <https://developer.chrome.com/docs/ai/rewriter-api> |
| **Proofreader API** | Correggi grammatica e stile | <https://developer.chrome.com/docs/ai/proofreader-api> |

- **Esempio**:
  ```js
  const rewritten = await chrome.ai.rewriter.rewrite({
    original: "Hello, world!",
    style: "formal"
  });
  ```

---

# Case Study & Best Practices

---

## 3.1 Case Studies

| Azienda | Uso | Riferimento |
|---------|-----|-------------|
| CyberAgent | Prompt API per UI | <https://developer.chrome.com/blog/prompt-api-blog-cyberagent> |
| Jio Hotstar | Traduzione on‑device | <https://developer.chrome.com/blog/pb-jiohotstar-translation-ai> |
| Terra BrightSites | Sommario per contenuti | <https://developer.chrome.com/blog/summarizer-terra-brightsites> |
| RedBus Miravia | Riassunto per app | <https://developer.chrome.com/blog/summarizer-redbus-miravia> |
| Firebase AI Logic | Logica AI serverless | <https://developer.chrome.com/docs/ai/firebase-ai-logic> |
| Product Reviews | Valutazione recensioni on‑device | <https://developer.chrome.com/docs/ai/product-reviews-on-device> |

- **Key takeaways**: riduzione latenza, privacy, scalabilità.

---

## 3.2 Best Practices

| Tema | Esempio | Documentazione |
|------|---------|----------------|
| **Cache dei modelli** | Salva modelli su disco per usi futuri | <https://developer.chrome.com/docs/ai/cache-models> |
| **Streaming** | Visualizza risposte in tempo reale | <https://developer.chrome.com/docs/ai/streaming> |
| **Debug** | Utilizza `debug-gemini-nano` | <https://developer.chrome.com/docs/ai/debug-gemini-nano> |
| **Gestione modelli** | Monitora versioni e download | <https://developer.chrome.com/docs/ai/understand-built-in-model-management> |

- **Time‑box**: 30 min di talk con 15 slide (≈ 2 min ciascuna).

---

# Conclusioni

- Le Built‑in APIs di Chrome offrono un ecosistema rapido e privato per LLM.
- La combinazione di **Prompt API**, **Summarizer**, **Translator**, e altre rende semplice aggiungere AI a web‑app.
- Le best practices garantiscono performance e sicurezza.
