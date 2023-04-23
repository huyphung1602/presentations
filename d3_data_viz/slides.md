---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://source.unsplash.com/collection/94734566/1920x1080
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
</div> -->

<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:edit />
  </button>
  <a href="http://localhost:3030/presenter" target="_blank" alt="GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:presentation-file />
  </a>
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
layout: default
hideInToc: true
transition: fade-out
---

# Table of contents

<Toc max-depth="1"></Toc>

---
layout: section
transition: fade-out
---

# Introduction

---
transition: slide-up
level: 2
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
---

# What is D3.js?
##

- D3.js is a JavaScript library for manipulating documents based on data
- Allows you to bind data to a Document Object Model (DOM), and then apply transformations to the document
- Uses web standards: HTML, SVG and CSS
- Open source, maintained by Mike Bostock

---
transition: slide-up
level: 2
---

# Compare D3.js to other chart libraries
##

<table>
  <tr>
    <th></th>
    <th>D3.js</th>
    <th>Highcharts</th>
    <th>Vega</th>
    <th>Vega Lite</th>
  </tr>
  <tr>
    <td>Type</td>
    <td>Library</td>
    <td>Charting library</td>
    <td>Visualization grammar</td>
    <td>High-level visualization grammar</td>
  </tr>
  <tr>
    <td>Language</td>
    <td>JavaScript</td>
    <td>JavaScript</td>
    <td>JSON</td>
    <td>JSON</td>
  </tr>
  <tr>
    <td>Learning curve</td>
    <td>Steep</td>
    <td>Low</td>
    <td>Moderate</td>
    <td>Low</td>
  </tr>
   <tr>
    <td>Customization</td>
    <td>High</td>
    <td>Medium</td>
    <td>High</td>
    <td>Low</td>
  </tr>
  <tr>
    <td>Main purpose</td>
    <td>DOM manipulation for visualization</td>
    <td>Interactive charts and plots</td>
    <td>Create custom visualizations </td>
    <td>Rapid visualization creation</td>
  </tr>
</table>

---
transition: slide-up
level: 2
---

# Compare D3.js to other chart libraries
##

Some key differences:
- D3.js has a steep learning curve as a low-level library, while the others are higher level (especially Vega Lite)
- D3.js and Vega offer high customization, while Highcharts and Vega Lite are more limited
- Highcharts is focused specifically on charting, while D3.js and Vega are more general purpose
- Vega and Vega Lite use a JSON grammar, while D3.js and Highcharts use JavaScript
- D3.js manipulates the DOM directly, while the others have abstraction layers
Overall, the choice depends on your needs for customization vs. ease of use, purpose of visualization, and tech stack. Let me know if you would like me to clarify or expand the table further. I aimed for a high-level comparison, but can add more nuanced detail if needed.

---
layout: section
transition: fade-out
---

# Basic concepts

---
transition: slide-up
level: 2
---
# Basic Concepts
The core concepts to create charts using D3.js

There are some core concepts we need to know before creating our first chart using D3.js:
- Selections
- Scales
- Axes
- Transitions
- Data Binding

---
transition: slide-up
level: 2
---
# Selections
Selections are the basic unit of interaction in D3.js. They allow you to query and traverse the DOM.

**Making a selection**
- Use d3.select() to select one element:
```js
d3.select("div")  // Selects first div
```

- d3.select() uses querySelector() under the hood to find the first matching element.
- Use d3.selectAll() to select multiple elements:

```js
d3.selectAll("div") // Selects all divs
```
- d3.selectAll() uses querySelectorAll() under the hood to find all matching elements.

---
transition: slide-up
level: 2
---
# Selections
Selections are the basic unit of interaction in D3.js. They allow you to query and traverse the DOM.

- Select by ID (#), class (.), tag name, attribute, or node:
```js
d3.select("#id");   // Uses getElementById()
d3.select(".class");   // Uses getElementsByClassName()
d3.select("div");      // Uses querySelector()
d3.select("[attr]");  // Uses querySelector()
d3.select(node);      // Just passes through node
```

---
transition: slide-up
level: 2
---
# Selections
Selections are the basic unit of interaction in D3.js. They allow you to query and traverse the DOM.

**Selecting and chaining**
- Store selection in a variable to operate on later
- Use method chaining to apply multiple operations to a selection sequentially:
```js
let divSelection = d3.selectAll("div")
                     .attr("class", "bar")     // Set attribute
                     .style("color", "blue")   // Set style
```

- Each method call returns the selection, allowing the next method to be called on the same selection.

---
transition: slide-up
level: 2
---
# Selections
Selections are the basic unit of interaction in D3.js. They allow you to query and traverse the DOM.

**Appending elements**
- Use .append() to add an element to each node in the selection:
```js
divSelection.append("p")   // Add <p> to each div
```

- .append() uses element.appendChild() to append a child element to each node in the selection.

---
transition: slide-up
level: 2
---
# Selections
Selections are the basic unit of interaction in D3.js. They allow you to query and traverse the DOM.

**Other selection methods**
- .attr() - Get or set attributes
- .text() - Get or set text content
- .html() - Get or set inner HTML
- .style() - Get or set styles
- .on() - Add event listeners
- .data() - Bind data (covered in Data Binding slides)
- .enter() - Get "enter" selection (covered in Data Binding slides)
- .exit() - Get "exit" selection  (covered in Data Binding slides)
- .remove() - Remove elements from document
- And many more! Selections are a core part of D3.

---
transition: slide-up
level: 2
---
# Scales
Scales map a dimension of data to a visual representation. They are a core part of D3.js.

**Why use scales?**
- Map a continuous input domain (data) to a continuous or discrete output range (visual)
- Make visual encodings of data easier by handling interpolation and normalization
- Many types for different types of data (linear, ordinal, time, quantize, etc.)

---
transition: slide-up
level: 2
---
# Scales
Scales map a dimension of data to a visual representation. They are a core part of D3.js.

**Creating a scale**
- Use .scaleLinear() for a continuous linear scale:
```js
let scale = d3.scaleLinear()
             .domain([0, 100])     // Data domain
             .range([0, 500])      // Visual range
```

- Use .scaleOrdinal() for a discrete ordinal scale:
```js
let scale = d3.scaleOrdinal()
             .domain(["a", "b", "c"])
             .range(["red", "blue", "green"])
```
- Other scale types: time scale for dates, quantize scale for quantizing a continuous range into discrete values, threshold scale for a two-color range, etc.

---
transition: slide-up
level: 2
---
# Scales
Scales map a dimension of data to a visual representation. They are a core part of D3.js.

**Scale functions**
- scale(x) - Get corresponding y value for x
- For example:

```js
scale(25)     // Returns 250
scale("b")   // Returns "blue"
```
- invert(y) - Get x value for corresponding y value
- domain() - Get or set input domain
- range() - Get or set output range
- ticks() - Get tick values for axis
- tickFormat() - Format ticks appropriately (currency, percentage, time, etc.)

---
transition: slide-up
level: 2
---
# Scales
Scales map a dimension of data to a visual representation. They are a core part of D3.js.

**Uses of scales**
- Position and size elements based on data
- Color elements
- Create axes to map positions visually
- Encode other visual properties like opacity, font size, etc.

---
transition: slide-up
level: 2
---
# Axes
Axes are visual representations of scales. They provide reference marks for values along a scale's domain.

**Why use axes?**
- Give viewers a reference to position, value, and units along a dimension
- Automate the generation of axes based on scales
- Control axis appearance by setting properties


---
transition: slide-up
level: 2
---
# Axes
Axes are visual representations of scales. They provide reference marks for values along a scale's domain.

**Creating an axis**
- Call .axisBottom() (or .axisTop(), .axisLeft(), .axisRight()) and pass in a scale:

```js
let scale = d3.scaleLinear()
             .domain([0, 100])
             .range([0, 500]);

let axis = d3.axisBottom(scale);
```

---
transition: slide-up
level: 2
---
# Axes
Axes are visual representations of scales. They provide reference marks for values along a scale's domain.

**Appending the axis to the DOM**
- Create a g (group) element
- Apply a transform to position the axis
- Append the g to your SVG or grouping element

```js
svg.append("g")
   .attr("transform", "translate(0,500)")
   .call(axis);
```

---
transition: slide-up
level: 2
---
# Axes
Axes are visual representations of scales. They provide reference marks for values along a scale's domain.

**Axis properties**
Some properties to customize your axis:
- ticks: Number of ticks (and labels)
- tickSize: Length of ticks
- tickPadding: Padding between tick and label
- tickFormat: Format tick labels ($, %, time, SI prefix, etc.)
- orient: Orientation (top, bottom, left, right)
- tickValues: Specific tick values to use instead of D3's default
** Uses of axes **
- x-axis along the bottom of a chart
- y-axis along the left side of a chart
- Color bar axes
- Size axes
- And more! Any visual encoding of data along a dimension.

---
transition: slide-up
level: 2
---
# Transitions
Transitions animate and interpolate between states in D3.js visualizations.

**Why use transitions?**
- Create engaging data visualizations
- Help the viewer understand changes between states
- Guide the viewer's attention to important changes

---
transition: slide-up
level: 2
---
# Transitions
Transitions animate and interpolate between states in D3.js visualizations.

**How do they work?**
- D3 interpolates values and styles over the duration of the transition
- During a transition, D3 will calculate the state between the starting and ending values
  - For numeric values, it calculates the range between start and end
  - For colors, it interpolates RGB values
  - For positions, it calculates the intermediate x and y coordinates
- This gives the smooth animated transition effect

---
transition: slide-up
level: 2
---
# Transitions
Transitions animate and interpolate between states in D3.js visualizations.

**Adding a transition**
To a selection, call .transition() and chain a duration()method:
```js
selection
  .transition()
  .duration(500) // Transition lasts 500ms
  .attr("width", 200) // End value
```

This will animate the width of elements in the selection from their current width to 200px over 500ms.

---
transition: slide-up
level: 2
---
# Transitions
Transitions animate and interpolate between states in D3.js visualizations.

**Other methods**
- delay() - Delay transition start
- ease() - Set easing function for different effects (bounce, elastic, etc.)
- Can call same methods as on regular selections:
  - attr() - Animate attribute changes
  - style() - Animate style changes
  - text() - Transition text content
  - remove() - Transition elements out of the document

---
transition: slide-up
level: 2
---
# Transitions
Transitions animate and interpolate between states in D3.js visualizations.

**Common uses**
- Change bar heights on updating data
- Zoom in/out of a map or scatterplot
- Fade elements in/out
- Move elements positions
- And much more! Transitions greatly enhance data visualizations.

---
transition: slide-up
level: 2
---
# Data Binding
Data binding links input data to elements in the document.

**Why data binding?**
- Dynamically create elements based on data
- Update, remove or modify elements based on updated data
- The foundation for interactive, data-driven visualizations in D3

---
transition: slide-up
level: 2
---
# Data Binding
Data binding links input data to elements in the document.

**How does it work?**
- Use .data() to bind data to a selection of elements
- There are three selections made:
  - Update selection: Existing elements with bound data
  - Enter selection: New elements bound to new data
  - Exit selection: Existing elements with no bound data
- Apply operations to each selection independently

---
transition: slide-up
level: 2
---
# Data Binding
Data binding links input data to elements in the document.

**Update selection**
```js
selection
  .data(data)  // Binds data to selection
  .text(d => d.value)  // Updates text content to match bound data
```

**Enter selection**
To append new elements for data not bound to an element yet:
```js
selection
  .data(data)
  .enter()    // Selects enter selection
  .append("div")   // Append div for each enter selection
  .text(d => d.value) // Set text content with bound data
```

---
transition: slide-up
level: 2
---
# Data Binding
Data binding links input data to elements in the document.

**Exit selection**
To remove elements no longer bound to data:
```js
selection
  .data(data)
  .exit()     // Selects exit selection
  .remove()   // Remove exit selection
```

**Key functions**
For stable data bindings, define a key function to uniquely identify elements:
```js
selection
  .data(data, d => d.id)   // d.id is the key function
  // ...
```

---
transition: slide-up
level: 2
---
# Data Binding
Data binding links input data to elements in the document.

**Chaining**
Selections can be chained so you can bind data, update, add enter selections and remove exit selections sequentially.

---
layout: section
level: 2
transition: fade-out
---

# Demo 1
## Basic Concepts


---
layout: section
transition: fade-out
---
# Working with Data

---
transition: slide-up
level: 2
layout: image
image: ./images/the_d3_data_flow.svg
---
# The d3 data flow

---
transition: slide-up
level: 2
---
# Find the data
Data Types

When building data visualizations, we work with two main data types: quantitative and qualitative. Quantitative data is numerical information like time, weight, or countries' GDP. Quantitative data can be discrete or continuous.

Discrete data consists of whole numbers, also called integers, that cannot be subdivided.

Qualitative data is made of non-numerical information like text. It can be nominal or ordinal. Nominal values don't have a specific order, for instance, gender identity labels or city names. Ordinal values, on the other hand, can be classified by order of magnitude. If we take t-shirt sizes as an example, we usually list them in ascending size order (XS, S, M, L, XL).

---
transition: slide-up
level: 2
layout: image
image: ./images/data_types.svg
---

---
transition: slide-up
level: 2
---
# Find the data
Data Formats and Structures

Data comes in many formats for different needs. Some common ones are: 
- Tabular data: represent in columns and rows.
- JSON objects.
- Nested data.
- Networks.
- Geographic data.
- Raw data.

In this talk, we'll use the tabluar data from CSV file.

---
transition: slide-up
level: 2
---
# Load the data
##

We load the data into the project using the `d3-fetch` module.

```js
d3.csv('src/data/1.csv', d => {
  console.log(d);
});
```

---
transition: slide-up
level: 2
---
# Format the Data
##

Note how the values from the count column have been fetched as strings instead of numbers. This is a common issue when importing data and is due to the type conversion of the dataset from CSV to JSON. Since the callback function of d3.csv() gives us access to the data one row at a time, it is a great place to convert the counts back into numbers. Doing so will ensure that the count values are ready to be used to generate our visualization later.

```js
d3.csv('src/data/1.csv', d => {
  console.log(d);
  return {
    technology: d.technology,
    count: +d.count,
  }; 
}).then(d => {
  console.log(d);
});
```

---
transition: slide-up
level: 2
---
# Measure the Data
##

In step 3.a of our data workflow, we have completed the data formatting part but we can still explore and measure our data using D3. Measuring specific aspects of the data can help to get situated before diving into the actual crafting of a data visualization.

```js
d3.csv('src/data/1.csv', d => {
  return {
    technology: d.technology,
    count: +d.count,
  }; 
}).then(d => {
  console.log(d.length);
});
```

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