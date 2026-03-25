---
layout: section
---

# Proofreader API 

---
layout: default
---

# Proofreader API 
### Setup

Abilitare i seguenti flag

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