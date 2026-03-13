---
layout: image
image: '/images/apis-cover.jpg'
preload: true
transition: slide-up
---

<div class="slidev-layout h-full grid section">
    <div class="my-auto">
        <h1>anatomia delle API</h1>
    </div>
</div>

---
layout: default
---

# Anatomia delle API

<!-- | API | Scopo | Documentazione |
|-----|-------|----------------|
| **Summarizer API** | Riassume testi lunghi con pochi prompt | <https://developer.chrome.com/docs/ai/summarizer-api> |
| **Translator API** | Traduzione in tempo reale | <https://developer.chrome.com/docs/ai/translator-api> |
| **Language Detection** | Rileva lingua di input | <https://developer.chrome.com/docs/ai/language-detection> |
| **Prompt API** | Invia prompt in linguaggio naturale | <https://developer.chrome.com/docs/ai/prompt-api> |
| **Writer API** | Genera testo in stile editor | <https://developer.chrome.com/docs/ai/writer-api> |
| **Rewriter API** | Rephrase e miglioramento | <https://developer.chrome.com/docs/ai/rewriter-api> |
| **Proofreader API** | Correggi grammatica e stile | <https://developer.chrome.com/docs/ai/proofreader-api> | -->

| **API** | **Scopo** | 
|-----|-------|
| **Translator API** | Traduzione in tempo reale |
| **Language Detection API** | Rileva lingua di input |
| **Summarizer API** | Riassume testi lunghi con pochi prompt |
| **Prompt API** | Invia prompt in linguaggio naturale |
| **Writer API** | Genera testo in stile editor | 
| **Rewriter API** | Rephrase e miglioramento |
| **Proofreader API** | Correggi grammatica e stile |

---
layout: image
image: 'images/built-in-ai-apis-status.png'
backgroundSize: contain
---

# Anatomia delle API
## Stato delle API

---
layout: section
---

# Requisiti

---
layout: default
---

# Anatomia delle API
## Modelli

| API                    | Model Type      | Modality    |
|------------------------|-----------------|-------------|
| Translator API         | Expert Model    | Text → Text |
| Language Detector API  | Expert Model    | Text → Text |
| Summarizer API         | Language Model  | Text → Text |
| Prompt API             | Language Model  | Multimodal  |
| Writer API             | Language Model  | Text → Text |
| Rewriter API           | Language Model  | Text → Text |
| Proofreader API        | Language Model  | Text → Text |


---
layout: default
backgroundSize: contain
---

# Anatomia delle API
## Supporto software

| API                    | Mobile          | Desktop      |
|------------------------|-----------------|--------------|
| Translator API         | ❌​              | ✅​           |
| Language Detector API  | ❌​              | ✅​           |
| Summarizer API         | ❌​              | ✅​           |
| Prompt API             | ❌​              | ✅​           |
| Writer API             | ❌​              | ✅​           |
| Rewriter API           | ❌​              | ✅​           |
| Proofreader API        | ❌​              | ✅​           |

---
layout: image-right
image: '/images/apis-hardware-req.avif'
backgroundSize: contain
---

# Anatomia delle API
## Supporto hardware

- GPU (+4GB RAM)

- CPU (+16GB RAM & 4 CPU)