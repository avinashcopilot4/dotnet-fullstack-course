# CSS – Responsive Design & Media Queries

---

## 📘 What is Responsive Design?

Responsive design makes web pages look and work well across **all screen sizes** — desktop, tablet, and mobile — using flexible layouts and CSS media queries.

---

## 📱 The Viewport Meta Tag

Always include this in your HTML `<head>`. Without it, mobile browsers zoom out to show desktop width.

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

---

## 🎯 Media Queries

Media queries apply CSS only when conditions are met.

### Syntax
```css
@media (condition) {
  /* CSS rules here */
}
```

### Common Breakpoints
```css
/* Mobile first: small screens get base styles */
/* Tablet */
@media (min-width: 768px) { ... }

/* Desktop */
@media (min-width: 1024px) { ... }

/* Large screens */
@media (min-width: 1280px) { ... }

/* Or, desktop first (max-width) */
@media (max-width: 767px) { ... }  /* mobile */
```

### Media Types
```css
@media screen { ... }     /* screens */
@media print  { ... }     /* printers */
@media all    { ... }     /* all (default) */
```

### Combining Conditions
```css
/* Between 600px and 1024px */
@media (min-width: 600px) and (max-width: 1024px) { ... }

/* Either condition */
@media (max-width: 600px), (orientation: landscape) { ... }

/* Orientation */
@media (orientation: portrait)  { ... }
@media (orientation: landscape) { ... }
```

---

## 📐 Responsive Layout Patterns

### Mobile-First Approach
```css
/* Base: mobile */
.nav {
  display: flex;
  flex-direction: column;
}

/* Tablet and up */
@media (min-width: 768px) {
  .nav {
    flex-direction: row;
    justify-content: space-between;
  }
}
```

### Responsive Grid
```css
.grid {
  display: grid;
  grid-template-columns: 1fr;           /* 1 column on mobile */
  gap: 16px;
}

@media (min-width: 600px) {
  .grid { grid-template-columns: 1fr 1fr; }  /* 2 cols */
}

@media (min-width: 900px) {
  .grid { grid-template-columns: repeat(3, 1fr); }  /* 3 cols */
}
```

### Auto-Responsive Grid (No Media Queries!)
```css
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
}
```

---

## 📏 Responsive Units

```css
/* Relative units — prefer these for responsiveness */
font-size: 1rem;        /* relative to root */
padding: 2em;           /* relative to element font-size */
width: 80%;             /* relative to parent */
height: 100vh;          /* 100% of viewport height */
width: 50vw;            /* 50% of viewport width */
font-size: clamp(1rem, 2.5vw, 2rem); /* min, preferred, max */
```

### `clamp()` — Fluid Typography
```css
h1 {
  font-size: clamp(1.5rem, 5vw, 3rem);
  /* Never smaller than 1.5rem, never larger than 3rem */
  /* Scales fluidly with viewport width */
}
```

---

## 🖼️ Responsive Images

```css
img {
  max-width: 100%;     /* never wider than container */
  height: auto;        /* maintain aspect ratio */
}
```

```html
<!-- Serve different images at different sizes -->
<picture>
  <source media="(min-width: 800px)" srcset="large.jpg">
  <source media="(min-width: 400px)" srcset="medium.jpg">
  <img src="small.jpg" alt="Description">
</picture>
```

---

## 📝 Interview Questions

**Q1. What is the viewport meta tag and why is it required?**
> It tells mobile browsers to use the device's actual width instead of zooming out to a desktop layout. Without it, responsive CSS has no effect on mobile devices.

**Q2. What is the difference between mobile-first and desktop-first approaches?**
> Mobile-first starts with base styles for small screens and adds complexity with `min-width` media queries as screens get larger. Desktop-first does the opposite using `max-width`. Mobile-first is generally preferred as it prioritizes performance on constrained devices.

**Q3. What are common responsive breakpoints?**
> Common ones are: mobile < 768px, tablet 768–1024px, desktop > 1024px. These vary by project — breakpoints should be based on your content, not specific devices.

**Q4. What is the difference between `min-width` and `max-width` in media queries?**
> `min-width: 768px` applies styles when the viewport is **at least** 768px (tablet and up — used in mobile-first). `max-width: 767px` applies styles when the viewport is **at most** 767px (mobile — used in desktop-first).

**Q5. What does `clamp()` do?**
> It sets a value between a minimum and maximum with a preferred fluid value in between: `clamp(min, preferred, max)`. Great for fluid typography that scales with viewport without abrupt breakpoints.

**Q6. How do you make images responsive?**
> Set `max-width: 100%; height: auto;` on the `img` element. This ensures images never exceed their container but shrink proportionally on smaller screens.

**Q7. What is the advantage of `repeat(auto-fit, minmax(250px, 1fr))` over media queries for card grids?**
> It creates a fully responsive grid that automatically adjusts the number of columns without any media queries. Columns are always at least 250px wide and fill available space — cleaner and more maintainable.

---

*Next: Transitions & Animations →*
