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

| **API** | **Scopo** | **Spec** | 
|---------|-----------|----------|
| **Translator API** | Traduzione in tempo reale | Translation API |
| **Language Detection API** | Rileva lingua di input | Translation API |
| **Summarizer API** | Riassume testi lunghi con pochi prompt | Writing Assistance API |
| **Writer API** | Genera testo in stile editor | Writing Assistance API |
| **Rewriter API** | Rephrase e miglioramento | Writing Assistance API |
| **Prompt API** | Invia prompt in linguaggio naturale | Prompt API |
| **Proofreader API** | Correggi grammatica e stile | Proofreader API |

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
| Writer API             | Language Model  | Text → Text |
| Rewriter API           | Language Model  | Text → Text |
| Prompt API             | Language Model  | Multimodal  |
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
| Writer API             | ❌​              | ✅​           |
| Rewriter API           | ❌​              | ✅​           |
| Prompt API             | ❌​              | ✅​           |
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

---
layout: section
---

# Translation API 

---
layout: default
---

# Translation API 
## Translator API
### Esempio

````md magic-move

```javascript
'Translator' in self
// true
```

```javascript
const translatorCapabilities = await Translator.availability({
  sourceLanguage: 'it',
  targetLanguage: 'es',
});
// 'available'
// 'unavailable'
// 'downloadable'
// 'downloading'
```

```javascript
const translator = await Translator.create({
  sourceLanguage: 'it'
  targetLanguage: 'es',
});
```

```javascript
await translator.translate('Saluti da Corralejo');
// "Saludos desde Corralejo"
```

```javascript
const translatorCapabilities = await Translator.availability({
  sourceLanguage: 'it'
  targetLanguage: 'es',
});

const translator = await Translator.create({
  sourceLanguage: 'it'
  targetLanguage: 'es',
});

await translator.translate('Saluti da Corralejo');
// "Saludos desde Corralejo"
```

````

---
layout: default
---

# Translation API 
## Translator API
### Esempio con Stream

```javascript
const stream = translator.translateStreaming(longText);
for await (const chunk of stream) {
  console.log(chunk);
}
```

---
layout: default
---

# Translation API 
## Translator API
### Pro tip

Mostra sempre un loader nella UI quando usi chiami il metodo ```.translate```


---
layout: default
---

# Translation API 
## Language Detector API
### Esempio

````md magic-move

```javascript
'LanguageDetector' in self
// true
```

```javascript
const detector = await LanguageDetector.create();
```

```javascript
const detector = await LanguageDetector.create({
  monitor(m) {
    m.addEventListener('downloadprogress', (e) => {
      console.log(`Downloaded ${e.loaded * 100}%`);
    });
  },
});
```

```javascript
const text = 'Saludos desde Corralejo';
const results = await detector.detect(text);

for (const result of results) {
  console.log(result.detectedLanguage, result.confidence);
}
// Output:
// es 0.9882242679595947
// gl 0.00650646910071373
// und 0.000003673242190416204
```

```javascript
const detector = await LanguageDetector.create({
  monitor(m) {
    m.addEventListener('downloadprogress', (e) => {
      console.log(`Downloaded ${e.loaded * 100}%`);
    });
  },
});

const text = 'Saludos desde Corralejo';
const results = await detector.detect(text);

for (const result of results) {
  console.log(result.detectedLanguage, result.confidence);
}
// Output:
// es 0.9882242679595947
// gl 0.00650646910071373
// und 0.000003673242190416204
```

````

---
layout: default
---

# Translation API
## Language Detector API
### Security & Policy

<v-clicks>

- Non è supportato nei Service Worker

- top-level window (no cross-origin)

- configurazione permessi per iframe (cross-origin)

</v-clicks>

<v-after>

```html
<iframe src="https://cross-origin.example.com/" allow="language-detector"></iframe>
```

</v-after>

---
layout: section
---

# Writing Assistance API 

---
layout: default
---

# Writing Assistance API 
## Summarizer API
### Esempio

````md magic-move

```javascript
'Summarizer' in self
// true
```

```javascript
const availability = await Summarizer.availability();
// 'available'
// 'unavailable'
// 'downloadable'
// 'downloading'
```

```javascript
const summarizer = await Summarizer.create();
```

```javascript
const summarizer = await Summarizer.create({
  type: 'key-points', // key-points | tldr | teaser | headline
  format: 'markdown', // markdown | plainText
  length: 'medium', // short | medium | long
  sharedContext: 'This is article about american pro basketball. The users expect to a response in Spanish',
});
```

```javascript
const summarizer = await Summarizer.create({
  type: 'key-points', // key-points | tldr | teaser | headline
  format: 'markdown', // markdown | plainText
  length: 'medium', // short | medium | long
  sharedContext: 'This is article about american pro basketball. The users expect to a response in Spanish',
  expectedInputLanguages: ['en', 'ja', 'es'],
  outputLanguage: 'es',
  expectedContextLanguages: ['en'],
});
```

```javascript
const longText = document.querySelector('article').innerHTML;
const summary = await summarizer.summarize(longText, {
  context: 'This article is intended for readers who are familiar with American professional basketball',
});
```

```javascript
const longText = document.querySelector('article').innerHTML;
const stream = await summarizer.summarizeStream(longText, {
  context: 'This article is intended for readers who are familiar with American professional basketball',
});

for await (const chunk of stream) {
  console.log(chunk);
}
```

````