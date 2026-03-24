---
layout: image
image: '/images/built-in-apis-cover.png'
preload: true
transition: slide-up
---

<div class="slidev-layout h-full grid section">
    <div class="my-auto">
        <h1>Casi di studio</h1>
    </div>
</div>

---
layout: section
---

# Editoria

---
layout: image
image: "/images/uc-summarize.gif"
---

---
layout: default
---

# Editoria
### Generare sintesi

- genera un riassunto tramite Summarize API

- possibilità di generare *key-points* o *tldr* 


---
layout: image
image: "/images/uc-summarize-terra.gif"
---

---
layout: default
---

# Editoria
### Modificare contenuti

- genera un riassunto in una lingua non supportata

- uso combinato di Translation API e Summarize API


---
layout: section
---

# Recensioni

---
layout: image
image: "/images/uc-summarize-reviews.gif"
---

---
layout: two-cols-header
---

# Recensioni
### Riassumere recensioni

::left::

- riassumere le review usando Summarize API

- context-driven summarization

::right::

<v-click>

```javascript
 const promptContext =
      'Summarize the following reviews in 30 words or less.' +
      'Focus on key positives and negatives, such as comfort, maintenance,' +
      'pricing, and cleanliness. Reviews are separated by {end}.' +
      'Give the summary in just one paragraph.';

const reviewSummary = await summarizer.summarize(reviews, {
    context: promptContext
});
```

</v-click>
