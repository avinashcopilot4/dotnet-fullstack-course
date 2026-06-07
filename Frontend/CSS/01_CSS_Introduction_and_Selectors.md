# CSS – Introduction & Selectors

---

## 📘 What is CSS?

CSS (Cascading Style Sheets) is used to control the **visual presentation** of HTML elements — layout, colors, fonts, spacing, and more.

### Three Ways to Apply CSS

| Method | Example | Use Case |
|--------|---------|----------|
| **Inline** | `<p style="color:red;">` | Quick one-off overrides |
| **Internal** | `<style>` inside `<head>` | Single-page styles |
| **External** | `<link rel="stylesheet" href="style.css">` | Best practice for projects |

---

## 🎯 CSS Selectors

### Basic Selectors

```css
/* Element selector */
p { color: blue; }

/* Class selector */
.card { background: white; }

/* ID selector */
#header { font-size: 24px; }

/* Universal selector */
* { box-sizing: border-box; }
```

### Combinator Selectors

```css
/* Descendant (any level inside) */
div p { color: gray; }

/* Child (direct children only) */
div > p { color: red; }

/* Adjacent sibling (immediately after) */
h1 + p { font-weight: bold; }

/* General sibling (all after) */
h1 ~ p { color: green; }
```

### Attribute Selectors

```css
input[type="text"] { border: 1px solid #ccc; }
a[href^="https"] { color: green; }   /* starts with */
a[href$=".pdf"] { color: red; }      /* ends with */
a[href*="google"] { color: blue; }   /* contains */
```

### Pseudo-classes

```css
a:hover    { color: orange; }
a:visited  { color: purple; }
li:first-child  { font-weight: bold; }
li:last-child   { border: none; }
li:nth-child(2) { background: #f0f0f0; }
input:focus { outline: 2px solid blue; }
button:disabled { opacity: 0.5; }
```

### Pseudo-elements

```css
p::first-line   { font-weight: bold; }
p::first-letter { font-size: 2em; }
div::before     { content: "★ "; }
div::after      { content: " ✓"; }
::selection     { background: yellow; }
```

---

## 🏆 Specificity

Specificity determines which CSS rule wins when multiple rules target the same element.

```
Inline styles    → 1,0,0,0  (highest)
ID selectors     → 0,1,0,0
Class/pseudo     → 0,0,1,0
Element/pseudo   → 0,0,0,1  (lowest)
```

```css
/* Specificity: 0,0,0,1 */
p { color: black; }

/* Specificity: 0,0,1,0 — wins! */
.intro { color: blue; }

/* Specificity: 0,1,0,0 — wins over class! */
#main { color: red; }
```

> `!important` overrides all specificity — use sparingly.

---

## 📝 Interview Questions

**Q1. What is the difference between `id` and `class` selectors?**
> `id` is unique per page (use `#`) and has higher specificity. `class` can be reused on multiple elements (use `.`).

**Q2. What is specificity and how is it calculated?**
> Specificity is the priority system CSS uses to decide which rule applies. It's calculated as (inline, id, class, element). Higher numbers win.

**Q3. What does the cascade mean in CSS?**
> It means styles flow from multiple sources (browser defaults, external files, inline). When conflicts arise, specificity and order of declaration determine which wins.

**Q4. What is the difference between `>` and a space in CSS selectors?**
> `div > p` selects only *direct children*. `div p` selects *all descendants* at any nesting level.

**Q5. What are pseudo-elements vs pseudo-classes?**
> Pseudo-classes (`:hover`, `:focus`) target states of elements. Pseudo-elements (`::before`, `::after`) target specific parts of an element or create virtual elements.

**Q6. How does `!important` affect specificity?**
> It overrides all other declarations regardless of specificity. It should be avoided unless absolutely necessary as it breaks the natural cascade.

**Q7. What will be the color of the paragraph?**
```html
<p id="title" class="intro">Hello</p>
```
```css
p       { color: black; }
.intro  { color: blue; }
#title  { color: red; }
```
> **Red** — because `#id` has the highest specificity (0,1,0,0).

---

*Next: Box Model →*
