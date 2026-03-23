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
---

# Anatomia delle API
## Security & Policy

<v-clicks>

- Non è supportate nei Web Worker

- top-level window (no cross-origin)

- configurazione permessi per iframe (cross-origin)

</v-clicks>

<v-after>

```html
<iframe src="https://cross-origin.valeriocomo.dev/" 
  allow="summarizer,language-model,language-detector,writer,rewriter,proofreader">
</iframe>
```

</v-after>

---
layout: image-right
image: '/images/apis-hardware-req.avif'
backgroundSize: contain
---

# Anatomia delle API
## Requisiti hardware & software

- GPU (+4GB RAM)

- CPU (+16GB RAM & 4 CPU)

- Linux,Windows,MacOS,ChromeOS

- No Android & iOS

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
<iframe src="https://cross-origin.valeriocomo.dev/" allow="language-detector"></iframe>
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
const summary = await summarizer.summarize(longText);
```

```javascript
const longText = document.querySelector('article').innerHTML;
const summary = await summarizer.summarize(longText, {
  context: 'This article is intended for readers who are familiar with American professional basketball',
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

const longText = document.querySelector('article').innerHTML;
const summary = await summarizer.summarize(longText, {
  context: 'This article is intended for readers who are familiar with American professional basketball',
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

const longText = document.querySelector('article').innerHTML;
const stream = await summarizer.summarizeStream(longText, {
  context: 'This article is intended for readers who are familiar with American professional basketball',
});

for await (const chunk of stream) {
  console.log(chunk);
}
```

````
---
layout: default
---

# Writing Assistance API 
## Summarizer API
### Configurazione - type

| Type        | Significato                                                                                                              |
|-------------|--------------------------------------------------------------------------------------------------------------------------|
| tldr        | Riepilogo breve e diretto, fornisce una rapida panoramica dell'input |
| teaser      | Riepilogo delle parti più interessanti o intriganti dell'input, progettato per invogliare il lettore a continuare la lettura. |
| key points. | Riepilogo dei punti più importanti dall'input, presentandoli come elenco puntato.                   |
| headline    | Riepilogo che contiene il punto principale dell'input in una singola frase, nel formato di un titolo di articolo. |

---
layout: default
---

# Writing Assistance API 
## Summarizer API
### Configurazione - type & length

| Type        | Length     | Output             |
|-------------|------------|--------------------|
| tldr        |  short     | 1 frase            |
| tldr        |  medium    | 3 frasi            |
| tldr        |  long      | 5 frasi            |
| teaser      |  short     | 1 frase            |
| teaser      |  medium    | 3 frasi            |
| teaser      |  long      | 5 frasi            |

---
layout: default
---

# Writing Assistance API 
## Summarizer API
### Configurazione - type & length

| Type        | Lunghezza  | Output             |
|-------------|------------|--------------------|
| key-points  |  short     | 3 punti elenco     |
| key-points  |  medium    | 5 punti elenco     |
| key-points  |  long      | 7 punti elenco     |
| headline    |  short     | 12 parole          |
| headline    |  medium    | 17 parole          |
| headline    |  long      | 22 parole          |

---
layout: default
---

# Translation API
## Summarizer API
### Security & Policy

<v-clicks>

- Non è supportato nei Web Worker

- top-level window (no cross-origin)

- configurazione permessi per iframe (cross-origin)

</v-clicks>

<v-after>

```html
<iframe src="https://cross-origin.valeriocomo.dev/" allow="summarizer"></iframe>
```

</v-after>

---
layout: default
---

# Translation API 
## Summarizer API
### Pro tip

<v-clicks>

- context window limitata

- summary of summaries

</v-clicks>

<v-click>

```javascript
// numero di token dell'input
await summarizer.measureInputUsage('your long text here')
// numero di token della context window
await summarizer.inputQuota
```

</v-click>

---
layout: default
---

# Writing Assistance API 
## Writer API
### Setup

Abilitare i seguenti flag

```text
chrome://flags/#optimization-guide-on-device-model
```
```text
chrome://flags/#prompt-api-for-gemini-nano-multimodal-input
```
```text
chrome://flags/#writer-api-for-gemini-nano
```


---
layout: default
---

# Writing Assistance API 
## Writer API
### Esempio

````md magic-move

```javascript
'Writer' in self
```

```javascript
const availability = await Writer.availability();
```

```javascript
const writer = await Writer.create();
```

```javascript
const writer = await Writer.create({
  sharedContext: 'This is an email asking about the price of a car.',
  tone: 'casual', // neutral | formal | casual
  format: 'plain-text',  // plain-text | markdown
  length: 'medium', // short | medium | long
});
```

```javascript
const writer = await Writer.create({
  sharedContext: 'This is an email asking about the price of a car.',
  tone: 'casual', // neutral | formal | casual
  format: 'plain-text',  // plain-text | markdown
  length: 'medium', // short | medium | long
  expectedInputLanguages: ["en", "ja", "es"],
  expectedContextLanguages: ["en", "ja", "es"],
  outputLanguage: "en",
});
```

```javascript
const result = await writer.write(
  "An inquiry to a car dealer about the price of a car in stock.",
  {
    context: "I'm a new customer",
  },
);
/*
Subject: Inquiry Regarding Vehicle Price

Dear [Dealership Name],

I am interested in the [Year] [Make] [Model] currently listed on your website. 
Could you please provide the price for this vehicle, including any applicable taxes and fees? 
Thank you for your time and assistance.

Sincerely,

[Your Name]
[Your Phone Number]
*/
```

```javascript
const availability = await Writer.availability();

const writer = await Writer.create({
  sharedContext: 'This is an email asking about the price of a car.',
  tone: 'casual', // neutral | formal | casual
  format: 'plain-text',  // plain-text | markdown
  length: 'medium', // short | medium | long
  expectedInputLanguages: ["en", "ja", "es"],
  expectedContextLanguages: ["en", "ja", "es"],
  outputLanguage: "en",
});

const result = await writer.write(
  "An inquiry to a car dealer about the price of a car in stock.",
  {
    context: "I'm a new customer",
  },
);
```

```javascript
const availability = await Writer.availability();

const writer = await Writer.create({
  sharedContext: 'This is an email asking about the price of a car.',
  tone: 'casual', // neutral | formal | casual
  format: 'plain-text',  // plain-text | markdown
  length: 'medium', // short | medium | long
  expectedInputLanguages: ["en", "ja", "es"],
  expectedContextLanguages: ["en", "ja", "es"],
  outputLanguage: "en",
});

const stream = await writer.writeStreaming(
  "An inquiry to a car dealer about the price of a car in stock.",
  {
    context: "I'm a new customer",
  },
);

for await (const chunk of stream) {
  console.log(chunk)
}
```

````
---
layout: default
---

# Writing Assistance API 
## Writer API
### Pro tip

<v-clicks>

- Non è supportato nei Web Worker

- top-level window (no cross-origin)

- configurazione permessi per iframe (cross-origin)

</v-clicks>

<v-after>

```html
<iframe src="https://cross-origin.valeriocomo.dev/" allow="writer"></iframe>
```

</v-after>

---
layout: default
---

# Writing Assistance API 
## Rewriter API
### Setup

Abilitare i seguenti flag

```text
chrome://flags/#optimization-guide-on-device-model
```
```text
chrome://flags/#prompt-api-for-gemini-nano-multimodal-input
```
```text
chrome://flags/#writer-api-for-gemini-nano
```

---
layout: default
---

# Writing Assistance API 
## Rewriter API
### Esempio

````md magic-move

```javascript
'Rewriter' in self
```

```javascript
const availability = await Rewriter.availability();
```

```javascript
const rewriter = await Rewriter.create();
```

```javascript
const rewriter = await Rewriter.create({
  sharedContext: 'These are request of rephrasing a sentence.',
  tone: 'casual', // neutral | formal | casual
  format: 'plain-text',  // plain-text | markdown
  length: 'medium', // short | medium | long
});
```

```javascript
const rewriter = await Rewriter.create({
  sharedContext: 'These are request of rephrasing a sentence.',
  tone: 'casual', // neutral | formal | casual
  format: 'plain-text',  // plain-text | markdown
  length: 'medium', // short | medium | long
  expectedInputLanguages: ["en", "ja", "es"],
  expectedContextLanguages: ["en", "ja", "es"],
  outputLanguage: "en",
});
```

```javascript
const result = await rewriter.rewrite(
  text,
  {
    context: "Use a polite tone",
  },
);
```

```javascript
const availability = await Rewriter.availability();

const rewriter = await Rewriter.create({
  sharedContext: 'These are request of rephrasing a sentence.',
  tone: 'casual', // neutral | formal | casual
  format: 'plain-text',  // plain-text | markdown
  length: 'medium', // short | medium | long
  expectedInputLanguages: ["en", "ja", "es"],
  expectedContextLanguages: ["en", "ja", "es"],
  outputLanguage: "en",
});

const result = await rewriter.rewrite(
  text,
  {
    context: "Use a polite tone",
  },
);
```

```javascript
const availability = await Rewriter.availability();

const rewriter = await Rewriter.create({
  sharedContext: 'These are request of rephrasing a sentence.',
  tone: 'casual', // neutral | formal | casual
  format: 'plain-text',  // plain-text | markdown
  length: 'medium', // short | medium | long
  expectedInputLanguages: ["en", "ja", "es"],
  expectedContextLanguages: ["en", "ja", "es"],
  outputLanguage: "en",
});

const stream = await rewriter.rewriteStreaming(
  text,
  {
    context: "Use a polite tone",
  },
);

for await (const chunk of stream) {
  console.log(chunk)
}
```

````
---
layout: default
---

# Writing Assistance API 
## Rewriter API
### Pro tip

<v-clicks>

- Non è supportato nei Web Worker

- top-level window (no cross-origin)

- configurazione permessi per iframe (cross-origin)

</v-clicks>

<v-after>

```html
<iframe src="https://cross-origin.valeriocomo.dev/" allow="rewriter"></iframe>
```

</v-after>

<!-- 

layout: iframe
url: https://chrome.dev/web-ai-demos/writer-rewriter-api-playground/
allow: "writer,rewriter"

-->

---
layout: section
---

# Prompt API 

---
layout: default
---

# Prompt API 
### Setup

```text
chrome://flags/#optimization-guide-on-device-model
```

```text
chrome://flags/#prompt-api-for-gemini-nano-multimodal-input
```


---
layout: default
---

# Prompt API 
### Esempio

````md magic-move

```javascript
const available = await LanguageModel.availability({
  expectedInputs: [{type: 'text', languages: ['en']}],
  expectedOutputs: [{type: 'text', languages: ['en']}],
});

const session = await LanguageModel.create();

// Prompt the model and wait for the whole result to come back.
const result = await session.prompt('Write me a short poem!');
console.log(result);

/*
A single raindrop, cool and clear,
Reflects the sky, dispelling fear.
A tiny jewel, a fleeting grace,
Washing worries from time and space. 

Then slips away, a silent fall,
Joining the stream, answering the call.
*/
```

```javascript
const available = await LanguageModel.availability({
  expectedInputs: [{type: 'text', languages: ['en']}],
  expectedOutputs: [{type: 'text', languages: ['en']}],
});

const session = await LanguageModel.create();

// Prompt the model and wait for the whole result to come back.
const result = await session.prompt('Write me a short poem!');
console.log(result);
```


```javascript
const available = await LanguageModel.availability({
  expectedInputs: [
    {type: 'text', languages: ['en', 'ja', 'es']},
    {type: 'image'},
    {type: 'audio'},
  ],
  expectedOutputs: [{type: 'text', languages: ['en']}],
});

const session = await LanguageModel.create();

// Prompt the model and wait for the whole result to come back.
const result = await session.prompt('Write me a short poem!');
console.log(result);
```

```javascript
const options = {
  expectedInputs: [
    {type: 'text', languages: ['en', 'ja', 'es']},
    {type: 'image'},
    {type: 'audio'},
  ],
  expectedOutputs: [{type: 'text', languages: ['en']}],
};

const available = await LanguageModel.availability(options);

const session = await LanguageModel.create(options);
```

```javascript
const options = {
  expectedInputs: [
    {type: 'text', languages: ['en', 'ja', 'es']},
    {type: 'image'},
    {type: 'audio'},
  ],
  expectedOutputs: [{type: 'text', languages: ['en']}],
};

const available = await LanguageModel.availability(options);

const session = await LanguageModel.create(options);
```

```javascript
const options = {
  expectedInputs: [
    {type: 'text', languages: ['en', 'ja', 'es']},
    {type: 'image'},
    {type: 'audio'},
  ],
  expectedOutputs: [{type: 'text', languages: ['en']}],
};

const available = await LanguageModel.availability(options);

const session = await LanguageModel.create({
  ...options,
   initialPrompts: [
    { role: 'system', content: 'You are a fine-art critique' }
  ]
});
```

```javascript
const options = {
  expectedInputs: [
    {type: 'text', languages: ['en', 'ja', 'es']},
    {type: 'image'},
    {type: 'audio'},
  ],
  expectedOutputs: [{type: 'text', languages: ['en']}],
};

const available = await LanguageModel.availability(options);

const session = await LanguageModel.create({
  ...options,
   initialPrompts: [
    { role: 'system', content: 'You are a fine-art critique' },
    { role: 'user', content: 'Is impressionism the best movement ever? Answer just yes or no' },
    { role: 'assistant', content: 'No.'}
  ]
});

const response = await session.prompt('Is Monet an impressionist artist? Answer just yes or no')
//yes
```

```javascript
const session = await LanguageModel.create({
  ...options,
   initialPrompts: [
    { role: 'system', content: 'You are a fine-art critique' },
    { role: 'user', content: 'Is impressionism the best movement ever? Answer just yes or no' },
    { role: 'assistant', content: 'No.'}
  ]
});

const response = await session.prompt([{
  role: 'user'
  content: [
    {
      type: 'text',
      value: `Express a fine-art critique about this image`,
    },
    { type: 'image', value: fileUpload.files[0] },
  ],
}])
```

```javascript
const session = await LanguageModel.create({
  ...options,
   initialPrompts: [
    { role: 'system', content: 'You are a fine-art critique' },
    { role: 'user', content: 'Is impressionism the best movement ever? Answer just yes or no' },
    { role: 'assistant', content: 'No.'}
  ]
});

const canvas = document.querySelector("canvas");

const response = await session.prompt([{
  role: 'user'
  content: [
    {
      type: 'text',
      value: `Express a fine-art critique about this image`,
    },
    { type: 'image', value: canvas },
  ],
}])
```

```javascript
const session = await LanguageModel.create({
  ...options,
   initialPrompts: [
    { role: 'system', content: 'You are a fine-art critique' },
    { role: 'user', content: 'Is impressionism the best movement ever? Answer just yes or no' },
    { role: 'assistant', content: 'No.'}
  ]
});

const image = await (await fetch("impressionism-sol-levant.jpeg")).blob();

const response = await session.prompt([{
  role: 'user'
  content: [
    {
      type: 'text',
      value: `Express a fine-art critique about this image`,
    },
    { type: 'image', value: image },
  ],
}])
```

```javascript
const image = await (await fetch("impressionism-sol-levant.jpeg")).blob();
const response = await session.prompt([{
  role: 'user'
  content: [
    {
      type: 'text',
      value: `Express a fine-art critique about this image`,
    },
    { type: 'image', value: image },
  ],
}])
console.log(response)

const audioBuffer = functionThatGetAudioFromMic()
const userResponse = await session.prompt([
  {
    role: "user",
    content: [
      { type: "text", value: "My response to your critique:" },
      { type: "audio", value: audioBuffer },
    ],
  }
]);
```

````

---
layout: default
---

# Prompt API
### Session Mgmt


````md magic-move

```javascript
const languageModel = await LanguageModel.create({
  initialPrompts: [{
    role: 'system',
    content: 'You are a helpful personal-finance assistant.'
  }]
});
```

```javascript
const languageModel = await LanguageModel.create({
  initialPrompts: [{
    role: 'system',
    content: 'You are a helpful personal-finance assistant.'
  }]
});
// clone a session
const s1 = await languageModel.clone();
const s2 = await languageModel.clone();
```

```javascript
const languageModel = await LanguageModel.create({
  initialPrompts: [{
    role: 'system',
    content: 'You are a helpful personal-finance assistant.'
  }]
});
// clone a session
const s1 = await languageModel.clone();
const s2 = await languageModel.clone();

const r1 = s1.prompt('Is 1-ETF strategy a good strategy?')
const r2 = s2.prompt('Talk me about the all-weather portfolio')
```

```javascript
const languageModel = await LanguageModel.create({
  initialPrompts: [{
    role: 'system',
    content: 'You are a helpful personal-finance assistant.'
  }]
});
// clone a session
const s1 = await languageModel.clone();
const s2 = await languageModel.clone();

const r1 = s1.prompt('Is 1-ETF strategy a good strategy?')
const r2 = s2.prompt('Talk me about the all-weather portfolio')
// contextWindow - contextUsage
s1.contextUsage // 2471
s2.contextUsage // 1484
```

```javascript
const languageModel = await LanguageModel.create({
  initialPrompts: [{
    role: 'system',
    content: 'You are a helpful personal-finance assistant.'
  }]
});
// clone a session
const s1 = await languageModel.clone();
const s2 = await languageModel.clone();

const r1 = s1.prompt('Is 1-ETF strategy a good strategy?')
const r2 = s2.prompt('Talk me about the all-weather portfolio')
// contextWindow - contextUsage
s1.contextUsage // 2471
s2.contextUsage // 1484

s1.destroy();
s2.destroy();
```

````

---
layout: default
---

# Prompt API
### Structured Output

````md magic-move

```javascript
const session = await LanguageModel.create({
  ...options,
   initialPrompts: [
    { role: 'system', content: 'You are a fine-art critique. Answer just yes or no to my prompt' }
  ]
});
```

```javascript
const session = await LanguageModel.create({
  ...options,
   initialPrompts: [
    { role: 'system', content: 'You are a fine-art critique. Answer just yes or no to my prompt' }
  ]
});

const result = await session.prompt('Is Monet an impressionist artist ever?')
// "Yes."
```

```javascript
const schema = {
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "title": "YesNoResponse",
  "description": "An object that contains a yes/no answer",
  "type": "object",
  "properties": {
    "answer": {
      "type": "string",
      "enum": ["yes", "no"],
      "description": "Answer: yes or no"
    }
  },
  "required": ["answer"],
  "additionalProperties": false
}

const result = await session.prompt('Is Monet an impressionist artist ever?', { responseConstraint: schema })
// '{"answer": "yes"}'
```

````

---
layout: default
---

# Prompt API 
### Pro tip

<v-clicks>

- Non è supportato nei Web Worker

- top-level window (no cross-origin)

- configurazione permessi per iframe (cross-origin)

</v-clicks>

<v-after>

```html
<iframe src="https://cross-origin.valeriocomo.dev/" allow="language-model"></iframe>
```

</v-after>

<!-- 

layout: iframe
url: https://chrome.dev/web-ai-demos/writer-rewriter-api-playground/
allow: "writer,rewriter"

-->

---
layout: section
---

# Proofreader API 

---
layout: default
---

# Proofreader API 
### Setup

```text
chrome://flags/#optimization-guide-on-device-model
```

```text
chrome://flags/#prompt-api-for-gemini-nano-multimodal-input
```

```text
chrome://flags/#proofreader-api-for-gemini-nano
```

---
layout: default
---

# Proofreader API 
### Esempio

````md magic-move

```javascript
const available = await Proofreader.availability();
```

```javascript
const available = await Proofreader.availability();

const proofreader = await Proofreader.create();
```

```javascript
const available = await Proofreader.availability();

const proofreader = await Proofreader.create({
  expectedInputLanguages: ["en"]
});
```

```javascript
const available = await Proofreader.availability();

const proofreader = await Proofreader.create({
  expectedInputLanguages: ["en"]
});

const correction = await proofreader.proofread(
  'I gone to the bookstore yesterday and I bought two book of English grammar.',
);
```

```javascript
const correction = await proofreader.proofread(
  'I gone to the bookstore yesterday and I bought two book of English grammar.',
);

{
   "correctedInput":"I went to the bookstore yesterday and bought two books of English grammar.",
   "corrections": [
    ...
   ]
}
```

```javascript
const correction = await proofreader.proofread(
  'I gone to the bookstore yesterday and I bought two book of English grammar.',
);

{
   "correctedInput":"I went to the bookstore yesterday and bought two books of English grammar.",
   "corrections": [
      {
         "correction":"went",
         "endIndex":6,
         "startIndex":2,
         "types":[
            "grammar"
         ]
      },
      ...
   ]
}
```

```javascript
const correction = await proofreader.proofread(
  'I gone to the bookstore yesterday and I bought two book of English grammar.',
);

{
   "correctedInput":"I went to the bookstore yesterday and bought two books of English grammar.",
   "corrections": [
      ...
      {
         "correction":"",
         "endIndex":40,
         "startIndex":38,
         "types":[
            "grammar"
         ]
      },
      ...
   ]
}
```

```javascript
const correction = await proofreader.proofread(
  'I gone to the bookstore yesterday and I bought two book of English grammar.',
);

{
   "correctedInput":"I went to the bookstore yesterday and bought two books of English grammar.",
   "corrections": [
      ...
      {
         "correction":"books",
         "endIndex":55,
         "startIndex":51,
         "types":[
            "grammar"
         ]
      }
   ]
}
```

````

---
layout: default
---

# Proofreader API 
### Pro tip

<v-clicks>

- Non è supportato nei Web Worker

- top-level window (no cross-origin)

- configurazione permessi per iframe (cross-origin)

</v-clicks>


<v-after>

```html
<iframe src="https://cross-origin.valeriocomo.dev/" allow="proofreader"></iframe>
```

</v-after>