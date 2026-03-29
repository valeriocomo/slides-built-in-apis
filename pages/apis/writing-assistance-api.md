---
layout: section
---

# Writing Assistance API 

---
layout: center
---

# Writing Assistance API 

- Summarizer API

- Writer API

- Rewriter API

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
const stream = await summarizer.summarizeStreaming(longText, {
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
| key points  | Riepilogo dei punti più importanti dall'input, presentandoli come elenco puntato.                   |
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

# Writing Assistance API 
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

<!-- ```javascript
const writer = await Writer.create();
```

```javascript
const writer = await Writer.create({
  sharedContext: 'This is an email asking about the price of a car.',
  tone: 'casual', // neutral | formal | casual
  format: 'plain-text',  // plain-text | markdown
  length: 'medium', // short | medium | long
});
``` -->

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
## Rewriter API
### Esempio

````md magic-move

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