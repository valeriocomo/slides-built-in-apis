---
layout: section
---

# Translation API 

---
layout: center
---

# Translation API 

- Translator API

- Language Detector API

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
  sourceLanguage: 'it',
  targetLanguage: 'es',
});
```

```javascript
await translator.translate('Saluti da Corralejo');
// "Saludos desde Corralejo"
```

```javascript
const translatorCapabilities = await Translator.availability({
  sourceLanguage: 'it',
  targetLanguage: 'es',
});

const translator = await Translator.create({
  sourceLanguage: 'it',
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

Mostra sempre un loader nella UI quando usi il metodo ```.translate```


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