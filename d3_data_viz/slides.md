---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
# background: https://source.unsplash.com/collection/94734566/1920x1080
background: https://w.wallhaven.cc/full/7p/wallhaven-7p12xv.jpg
# apply any windi css classes to the current slide
class: 'text-center text-white'
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
# some information about the slides, markdown enabled
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# persist drawings in exports and build
drawings:
  persist: false
# page transition
transition: slide-left
# use UnoCSS
css: unocss
# Hide in Table of Content
hideInToc: true
---

# Basic Data Visualization with D3.js
*Visualize data dynamically*

<!-- <div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Press Space for next page <carbon:arrow-right class="inline"/>
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:edit />
  </button>
  <a href="https://github.com/slidevjs/slidev" target="_blank" alt="GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div> -->

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
layout: default
hideInToc: true
transition: fade-out
---

# Table of contents

<Toc></Toc>

---
layout: section
transition: fade-out
---

# Introduction

---
transition: slide-up
level: 2
hideInToc: true
---

# Meet John
##

John had CSV data tracking key metrics for his company that he wanted to visualize. Simply sharing the raw data wouldn't convey the insights effectively. He needed an interactive visualization solution.

John found D3.js, a JavaScript library to bind data to HTML/SVG and create visualizations. Using D3.js, John built line charts, bar charts and pie charts to represent his data.

John loaded his data into D3.js and created his first visualization in a few lines of code. He built more visualizations and dashboards, bringing his data to life with responsive and animated charts.

Stakeholders seeing John's dashboards instantly grasped insights that were hard to see in the CSVs. John's project succeeded, and he plans to use D3.js again. D3.js proved a simple yet powerful tool to gain valuable insights into complex data.

Overall, the core message and sequence of events remains the same as the original story, just in a more concise summarization.

---
transition: slide-up
level: 2
hideInToc: true
---

# What is D3.js?
##

D3.js is a JavaScript library for manipulating documents based on data. It uses HTML, CSS, and SVG to create interactive data visualizations that update automatically when your data changes. With over 100 built-in charts and maps, D3.js is a popular choice for building dynamic dashboards, reports, and data exploration tools.

---
transition: slide-up
level: 2
hideInToc: true
---

# Compare D3.js to other chart libraries
##

| Library | Highcharts.js | D3.js | Vega | Vega Lite|
|:-:|:-:|:-:|:-:|:-:|
| Pros | Easy to use<br>Many chart types<br>Good documentation<br>Simple styling<br>Commercial support | Customizable<br>Handles big data<br>Open source<br>Smooth animations<br> Free| Declarative<br>Efficient with big data<br>Open source <br>Embeddable<br>Enables interaction|Easier to learn than Vega <br>Also handles big data <br>Open source<br>Good documentation   |
| Cons | Limited customization<br>Inefficient for big data<br>Paid license for commercial use|Steep learning curve<br>Coding-intensive<br>No default styling |   Steep learning curve<br>Abstracted from HTML<br>Limited docs/support|Less flexible than Vega<br>Still requires Vega knowledge<br>Limited styling|

---
layout: section
transition: fade-out
---

# Basic selection and manipulation

---
transition: slide-up
level: 2
hideInToc: true
---
# Selection
##

- **d3.select()** - Selects the first element that matches the selector
- **d3.selectAll()** - Selects all elements that match the selector
- selection.select() - Selects descendants of the current selection 
- selection.selectAll() - Selects all descendants of the current selection
- selection.filter() - Filters the selection to only keep elements that match the selector
- selection.data() - Binds data to the selected elements  

---
transition: slide-up
level: 2
hideInToc: true
---
# Manipulation
## 

- **selection.append()** - Appends a new element to each selected node
- selection.insert() - Inserts a new element before each selected node   
- selection.html() - Sets the inner HTML of each selected node
- **selection.attr()** - Sets the given attribute on each selected node
- **selection.style()** - Sets the given style property on each selected node 
- selection.on() - Attaches an event listener to each selected node
- selection.remove() - Removes each selected node
- selection.sort() - Sorts the selected nodes stably
- selection.raise() - Re-inserts each selected node as the last child of its parent 
- selection.lower() - Re-inserts each selected node as the first child of its parent

---
transition: slide-up
level: 2
hideInToc: true
---
# Select and Append flow
##

Here is the flow of operations when D3 selects and appends an element:
1. Use `d3.select()` to find an element:

```js
d3.select("#container")
```

This uses `document.querySelector()` to find the element with id="container"

2. Call `.append()` on the selection to append a new element:

```js
d3.select("#container").append("p")
```

This uses `element.appendChild(document.createElement("p"))` to:
- Create a new `<p>` element with `document.createElement("p")`.
- Append it as a child of `#container` with `appendChild()`.

---
transition: slide-up
level: 2
hideInToc: true
---
# Select and Append flow
##

3. The new `<p>` element is now part of the selection and can be manipulated:

```js 
d3.select("#container")
  .append("p")
  .text("Hello")   // Sets text content with element.textContent
  .style("color", "blue") // Sets style with element.style.color 
```

4. We can traverse to the parent or children of the selection:

```js
const parent = d3.select("#container").select("p").parent() 
// Uses element.parentElement to select #container parent

const children = parent.children()
// Uses element.children to select #container descendants, including the <p>
```

5. D3 returns a new selection at each step, allowing us to chain multiple methods:

```js
d3.select("#container")
  .append("p")
  .text("Hello")
  .style("color", "blue") 
  .on("click", () => {...}) // Attaches an event with element.addEventListener()
```

---
layout: section
level: 2
hideInToc: true
---

# Demo 1
## Basic selection and manipulation


---
layout: section
---
# The Basic Shape

---
layout: section
---
# Creating bar chart using D3.js

---
image: https://source.unsplash.com/collection/94734566/1920x1080
hideInToc: true
---

# Code

Use code snippets and get the highlighting directly![^1]

```ts {all|2|1-6|9|all}
interface User {
  id: number
  firstName: string
  lastName: string
  role: string
}

function updateUser(id: number, update: User) {
  const user = getUser(id)
  const newUser = { ...user, ...update }
  saveUser(id, newUser)
}
```

<arrow v-click="3" x1="400" y1="420" x2="230" y2="330" color="#564" width="3" arrowSize="1" />

[^1]: [Learn More](https://sli.dev/guide/syntax.html#line-highlighting)

<style>
.footnotes-sep {
  @apply mt-20 opacity-10;
}
.footnotes {
  @apply text-sm opacity-75;
}
.footnote-backref {
  display: none;
}
</style>

---