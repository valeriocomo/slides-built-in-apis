---
# theme
# https://sli.dev/themes/gallery.html

theme: apple-basic
transition: slide-left
title: npm workspaces in 15 minuti
layout: intro-image
image: '/images/cover.jpg'
---

# npm workspaces in 15 minuti
## monorepo senza tool

<div class="absolute bottom-10">
  <span class="font-700">
    Valerio Como
  </span>
</div>

<div class="abs-br m-6 text-xl">
  <a href="https://github.com/valeriocomo/slides-npm-workspaces-in-15-min" target="_blank" class="slidev-icon-btn">
    <carbon:logo-github />
  </a>
</div>

---
src: ./pages/00-about-me.md
transition: fade
---

---
layout: section
transition: slide-down
---

# monorepo

---
layout: image-right

# the image source
image: /images/what.gif
---

# monorepo
## Cos'è un monorepo

un **monorepo** è un singolo repository che contiene:

<v-clicks>

- più package / app
- versionati insieme
- con dipendenze condivise

</v-clicks>

---
layout: image-right

# the image source
image: /images/why.gif
---

# monorepo
## perché parliamo di monorepo?

<v-clicks>

- codebase sempre più grandi
- condivisione di codice tra package
- coerenza di tooling e dipendenze
- meno _copy&paste_, più riuso

</v-clicks>

---
layout: section
trasition: slide-down
---

# npm workspaces

---
layout: center
---

# npm workspaces

feature **nativa di npm**

<v-clicks>

- introdotta in npm 7+
- zero dipendenze esterne
- gestione multi-package

</v-clicks>


---

# npm workspaces
## configurazione base

<v-click>

### package.json
```json
{
  "name": "my-awesome-project",
  "private": true,
  "workspaces": [
    "packages/*",
    "apps/*"
  ]
}
```

</v-click>

<v-click>

### packages/lib/package.json

```json
{
  "name": "@my-awesome-project/lib",
  "version": "0.4.3",
  "exports": {
      ".": "./src/index.ts"
  },
  "dependencies": {
      "@my-awesome-project/config": "workspace:*",
      "@my-awesome-project/ui": "1.2.0",
  }
}
```

</v-click>


---
layout: center
---

# npm workspaces
## cosa fa

<v-clicks>

- installazione dipendenze condivisa
- linking automatico tra package locali
- hoisting delle dipendenze
- un solo `node_modules`

</v-clicks>


---

# npm workspaces
## esecuzione script

```bash
npm run build --workspace=@my-awesome-project/lib
npm run test --workspaces
```

oppure:

```bash
npm -w packages/lib run build
```

---
layout: center
---

# npm workspaces
## dependency graph (semplice)

- _npm_ risolve le dipendenze
- collega i package locali
- **nessuna orchestrazione avanzata**

> npm non decide *ordine*, *cache* o *parallelismo*

---
layout: section
transition: slide-down
---

# quando usare npm workspace

---
layout: two-cols-header
---

# quando usare npm workspace

::left::

<v-click>

## quando è ok

- librerie condivise
- design system
- piccoli / medi monorepo
- team ridotti

</v-click>

::right::

<v-click>

## quando NON basta

- build complesse
- pipeline ottimizzate
- task dipendenti
- scaling team e repo

</v-click>

---

# quando usare npm workspace
## npm vs Turborepo vs Nx

| Feature | npm workspaces | Turborepo | Nx |
|------|---------------|-----------|----|
| Built-in | ✅ | ❌ | ❌ |
| Task orchestration | ❌ | ✅ | ✅ |
| Cache build | ❌ | ✅ | ✅ |
| Dependency graph | ❌ | ⚠️ | ✅ |
| Learning curve | 🟢 Bassa | 🟡 Media | 🔴 Alta |
| Opinionated | ❌ | 🟡 | ✅ |

---
layout: section
transition: slide-down
---

# PROs & CONs

---
layout: two-cols-header
---

# PROs & CONs

::left::

<v-click>

## PROs

- zero setup extra
- standard npm
- trasparente
- nessun lock-in
- facile da spiegare

</v-click>


::right::

<v-click>

## CONs

- niente caching
- niente parallelismo intelligente
- niente affected commands
- scaling limitato

</v-click>

---
layout: section
transition: slide-down
---

# processo decisionale

---

# processo decisionale
## strategia consigliata

<v-clicks>

- parti con npm workspaces
 
- valuta complessità reale

- introduci Turborepo o Nx **solo se serve**

</v-clicks>

<v-click>

> "Start simple, scale when needed"

</v-click>

---

# processo decisionale
## messaggio chiave

👉 npm workspaces **non è un sostituto** di Nx o Turborepo

👉 è una **base solida** per monorepo moderni

---
src: ./pages/01-qa.md
transition: slide-down
---