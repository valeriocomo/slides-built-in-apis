---
class: text-center
drawings:
  persist: false
info: |
  Chrome Built‑in AI APIs On-device AI for the Web Platform
theme: apple-basic
title: Chrome Built‑in AI APIs
transition: slide-left
---

# Chrome Built‑in AI APIs

## On‑device AI for the Web

Using Gemini Nano directly in the browser

Valerio Como\
Software Engineer

------------------------------------------------------------------------

# Agenda

## 1. Introduzione alle Built‑in APIs

-   AI direttamente nel browser
-   Gemini Nano
-   Architettura client-side

## 2. Le API disponibili

-   Summarizer
-   Translator
-   Language Detector
-   Prompt API
-   Writer / Rewriter
-   Proofreader

## 3. Case studies e best practices

------------------------------------------------------------------------

# The Big Idea

## AI direttamente nel browser

Chrome introduce **Built‑in AI APIs** che permettono alle applicazioni
web di:

-   usare modelli AI locali
-   eseguire inferenza on-device
-   evitare chiamate server

------------------------------------------------------------------------

# Perché è importante

Prima:

Browser → Server → LLM → Server → Browser

Ora:

Browser → Local Model → Browser

Vantaggi:

-   privacy
-   bassa latenza
-   zero costi server

------------------------------------------------------------------------

# Architettura

1️⃣ Il sito chiama una Built‑in API\
2️⃣ Chrome comunica con il modello locale\
3️⃣ Il modello gira su CPU / GPU / NPU\
4️⃣ Il risultato torna alla pagina

------------------------------------------------------------------------

# Gemini Nano

Chrome usa **Gemini Nano** per molte API generative.

Caratteristiche:

-   modello ottimizzato per device locali
-   eseguito nel browser
-   scaricato automaticamente

------------------------------------------------------------------------

# Language Detector API

``` javascript
const detector = await LanguageDetector.create()

const result = await detector.detect("Bonjour le monde")
```

------------------------------------------------------------------------

# Translator API

``` javascript
const translator = await Translator.create({
  sourceLanguage: "fr",
  targetLanguage: "en"
})

translator.translate("Bonjour")
```

------------------------------------------------------------------------

# Summarizer API

``` javascript
const summarizer = await Summarizer.create({
  type: "key-points",
  length: "medium"
})

const summary = await summarizer.summarize(text)
```

------------------------------------------------------------------------

# Streaming summary

``` javascript
const stream = summarizer.summarizeStreaming(text)

for await (const chunk of stream) {
  console.log(chunk)
}
```

------------------------------------------------------------------------

# Prompt API

``` javascript
const session = await LanguageModel.create()

const result = await session.prompt(
  "Explain quantum computing"
)
```

------------------------------------------------------------------------

# Writer API

Generazione di testo:

-   email
-   descrizioni prodotto
-   assistenti di scrittura

------------------------------------------------------------------------

# Rewriter API

Riscrittura di testo:

-   cambiare tono
-   accorciare
-   espandere

------------------------------------------------------------------------

# Proofreader API

Correzione grammaticale automatica.

Use cases:

-   editor di testo
-   commenti
-   chat

------------------------------------------------------------------------

# Structured output

La Prompt API può restituire JSON strutturato.

``` json
{
  "title": "...",
  "summary": "...",
  "sentiment": "positive"
}
```

------------------------------------------------------------------------

# Scaling summarization

Tecnica:

doc → chunks → summaries → final summary

------------------------------------------------------------------------

# Case Study --- Product Reviews

AI locale per:

-   riassumere recensioni
-   identificare pro e contro
-   analizzare sentiment

------------------------------------------------------------------------

# Case Study --- Traduzione

Flusso:

post → language detect → translate

Tutto direttamente nel browser.

------------------------------------------------------------------------

# Hybrid AI

Strategia moderna:

Client AI + Cloud AI

-   client per task veloci
-   cloud per task complessi

------------------------------------------------------------------------

# Best Practices

✔ verificare availability API\
✔ usare streaming\
✔ informare l'utente del download modello

------------------------------------------------------------------------

# Debug

Tool utile:

chrome://on-device-internals

------------------------------------------------------------------------

# Il futuro dell'AI sul web

Trend:

-   AI client-side
-   browser come runtime AI
-   WebGPU + modelli locali

------------------------------------------------------------------------

# Conclusioni

Le Built‑in AI APIs permettono di:

-   portare l'AI nel browser
-   migliorare privacy
-   ridurre costi backend

------------------------------------------------------------------------

# Grazie

Domande?
