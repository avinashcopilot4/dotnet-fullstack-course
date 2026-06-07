# 01 — HTML Tags & Document Structure

> **Interview Tip:** "HTML stands for HyperText Markup Language. It gives structure and meaning to web content using elements (tags)."

---

## What is an HTML Tag?

A **tag** is a keyword wrapped in angle brackets. Most tags come in pairs — an opening tag and a closing tag.

```html
<tagname> content </tagname>
```

A **self-closing tag** has no content and no closing pair:

```html
<img src="photo.jpg" alt="photo" />
<br />
<hr />
<input type="text" />
```

---

## Anatomy of an HTML Document

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Page Title</title>
    <link rel="stylesheet" href="style.css" />
  </head>
  <body>
    <!-- Visible content goes here -->
    <h1>Hello World</h1>
  </body>
</html>
```

| Part | Purpose |
|---|---|
| `<!DOCTYPE html>` | Tells the browser to use HTML5 |
| `<html lang="en">` | Root element; `lang` helps screen readers |
| `<head>` | Metadata — not visible on the page |
| `<meta charset="UTF-8">` | Character encoding (supports all languages) |
| `<meta name="viewport">` | Makes the page responsive on mobile |
| `<title>` | Text shown in browser tab |
| `<link>` | Links external CSS file |
| `<body>` | Everything the user sees |

---

## Heading Tags

```html
<h1>Main Title (only ONE per page)</h1>
<h2>Section Heading</h2>
<h3>Sub-section</h3>
<h4>Sub-sub-section</h4>
<h5>Rarely used</h5>
<h6>Smallest heading</h6>
```

> **Interview Q:** Why only one `<h1>` per page? — SEO and accessibility; it defines the main topic.

---

## Text Content Tags

```html
<p>This is a paragraph.</p>

<strong>Bold & important</strong>   <!-- semantic weight -->
<b>Just visually bold</b>           <!-- no semantic meaning -->

<em>Italic & emphasized</em>        <!-- semantic emphasis -->
<i>Just visually italic</i>         <!-- no semantic meaning -->

<u>Underlined</u>
<s>Strikethrough</s>

<small>Fine print / legal text</small>
<mark>Highlighted text</mark>
<sup>Superscript</sup> and <sub>Subscript</sub>

<br />   <!-- Line break (use sparingly) -->
<hr />   <!-- Horizontal rule / thematic break -->
```

---

## Container / Layout Tags

### Block-level vs Inline elements

| Block-level | Inline |
|---|---|
| Takes full width, starts on new line | Only as wide as content |
| `<div>`, `<p>`, `<h1>`–`<h6>`, `<section>` | `<span>`, `<a>`, `<strong>`, `<img>` |

```html
<!-- div: generic block container, used for layout -->
<div class="card">
  <h2>Title</h2>
  <p>Content here</p>
</div>

<!-- span: generic inline container, used for styling a word/phrase -->
<p>The price is <span class="price">₹999</span> only.</p>
```

---

## Semantic HTML5 Tags

Semantic tags describe **meaning**, not just appearance. Always prefer them over `<div>` where appropriate.

```html
<header>   <!-- Site or section header, logo, nav -->
<nav>      <!-- Navigation links -->
<main>     <!-- Primary unique content (ONE per page) -->
<section>  <!-- Thematic grouping with a heading -->
<article>  <!-- Self-contained piece (blog post, news item) -->
<aside>    <!-- Sidebar / related content -->
<footer>   <!-- Bottom of page or section -->
```

**Example page structure:**

```html
<body>
  <header>
    <h1>My Blog</h1>
    <nav>
      <a href="/">Home</a>
      <a href="/about">About</a>
    </nav>
  </header>

  <main>
    <article>
      <h2>Post Title</h2>
      <p>Post content...</p>
    </article>
    <aside>
      <h3>Related Posts</h3>
    </aside>
  </main>

  <footer>
    <p>© 2024 My Blog</p>
  </footer>
</body>
```

> **Interview Q:** What are semantic tags and why use them?
> — They give meaning to structure, improve SEO, and make pages accessible to screen readers.

---

## Links

```html
<!-- External link -->
<a href="https://google.com" target="_blank" rel="noopener noreferrer">
  Visit Google
</a>

<!-- Internal link -->
<a href="/about.html">About Us</a>

<!-- Jump to section on same page (anchor) -->
<a href="#contact">Go to Contact</a>
<section id="contact">...</section>

<!-- Email link -->
<a href="mailto:hello@example.com">Email Us</a>

<!-- Phone link -->
<a href="tel:+919876543210">Call Us</a>
```

> **Interview Q:** What does `target="_blank"` do and why add `rel="noopener"`?
> — Opens in a new tab. `noopener` prevents the new page from accessing `window.opener`, a security measure.

---

## Images

```html
<img
  src="photo.jpg"          <!-- file path or URL -->
  alt="A smiling person"   <!-- REQUIRED for accessibility & SEO -->
  width="400"
  height="300"
  loading="lazy"           <!-- defer offscreen images -->
/>
```

> **Interview Q:** Why is `alt` important? — Screen readers use it; also shown when image fails to load.

---

## Lists

```html
<!-- Unordered (bullets) -->
<ul>
  <li>HTML</li>
  <li>CSS</li>
  <li>JavaScript</li>
</ul>

<!-- Ordered (numbers) -->
<ol>
  <li>Wake up</li>
  <li>Code</li>
  <li>Sleep</li>
</ol>

<!-- Description list -->
<dl>
  <dt>HTML</dt>
  <dd>Hyper Text Markup Language</dd>
  <dt>CSS</dt>
  <dd>Cascading Style Sheets</dd>
</dl>
```

---

## Tables

```html
<table border="1">
  <caption>Student Marks</caption>
  <thead>
    <tr>
      <th>Name</th>
      <th>Marks</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Rahul</td>
      <td>85</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td>Average</td>
      <td>85</td>
    </tr>
  </tfoot>
</table>
```

Attributes: `colspan="2"` (span columns), `rowspan="2"` (span rows)

---

## Meta Tags (Important for SEO & Social)

```html
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Learn HTML basics for freshers">
  <meta name="keywords" content="HTML, web development, tutorial">
  <meta name="author" content="Your Name">

  <!-- Open Graph (for sharing on WhatsApp, LinkedIn, etc.) -->
  <meta property="og:title" content="My Page Title">
  <meta property="og:image" content="thumbnail.jpg">
</head>
```

---

## Script & Style Tags

```html
<!-- Internal CSS -->
<style>
  body { background: #f0f0f0; }
</style>

<!-- External CSS (in <head>) -->
<link rel="stylesheet" href="style.css">

<!-- Internal JS (before </body> is best practice) -->
<script>
  console.log("Hello!");
</script>

<!-- External JS -->
<script src="app.js" defer></script>
```

> `defer` — script loads in background, runs after HTML is parsed. Always use for external scripts.

---

## Quick-Reference Cheatsheet

| Tag | Use |
|---|---|
| `<h1>–<h6>` | Headings |
| `<p>` | Paragraph |
| `<a>` | Hyperlink |
| `<img>` | Image |
| `<ul>` / `<ol>` / `<li>` | Lists |
| `<table>`, `<tr>`, `<td>`, `<th>` | Tables |
| `<div>` | Block container |
| `<span>` | Inline container |
| `<header>`, `<nav>`, `<main>`, `<footer>` | Semantic layout |
| `<strong>`, `<em>` | Bold / italic with meaning |
| `<br>`, `<hr>` | Line break / horizontal rule |

---

## Common Interview Questions

1. What is the difference between `<div>` and `<span>`?
2. What are semantic HTML tags? Give examples.
3. What is the difference between `<strong>` and `<b>`?
4. What does `<!DOCTYPE html>` do?
5. Why is `alt` attribute important on `<img>`?
6. What is the difference between block and inline elements?
