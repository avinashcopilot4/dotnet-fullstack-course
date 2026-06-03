# CSS – Grid Layout

---

## 📘 What is CSS Grid?

CSS Grid is a **two-dimensional** layout system — it handles both rows AND columns simultaneously. Perfect for complex page layouts.

```css
.container {
  display: grid;
}
```

---

## 🗂️ Grid Container Properties

### Defining Columns & Rows

```css
.container {
  display: grid;

  /* Define 3 columns */
  grid-template-columns: 200px 200px 200px;
  grid-template-columns: 1fr 1fr 1fr;      /* equal fractions */
  grid-template-columns: 2fr 1fr 1fr;      /* 2:1:1 ratio */
  grid-template-columns: 200px 1fr;        /* fixed + flexible */
  grid-template-columns: repeat(3, 1fr);   /* shorthand for 3 equal */
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); /* responsive */

  /* Define 2 rows */
  grid-template-rows: 100px auto;
}
```

### Gap Between Cells
```css
gap: 20px;               /* row + column gap */
row-gap: 10px;
column-gap: 20px;
gap: 10px 20px;          /* row-gap column-gap */
```

### Alignment
```css
/* Align all cells inside their area */
justify-items: start | end | center | stretch;  /* horizontal */
align-items:   start | end | center | stretch;  /* vertical */

/* Align the entire grid inside the container */
justify-content: start | end | center | space-between | space-around;
align-content:   start | end | center | space-between | space-around;
```

### Grid Template Areas
```css
.container {
  display: grid;
  grid-template-columns: 200px 1fr;
  grid-template-rows: auto 1fr auto;
  grid-template-areas:
    "header  header"
    "sidebar main"
    "footer  footer";
}

header  { grid-area: header; }
sidebar { grid-area: sidebar; }
main    { grid-area: main; }
footer  { grid-area: footer; }
```

---

## 🧩 Grid Item Properties

### Placement by Line Numbers
```css
/* Lines start at 1 */
.item {
  grid-column: 1 / 3;   /* from line 1 to line 3 (spans 2 cols) */
  grid-row: 1 / 2;      /* row 1 only */
}

/* span keyword */
.item {
  grid-column: 1 / span 2;  /* start at 1, span 2 columns */
  grid-row: span 3;          /* span 3 rows wherever it lands */
}
```

### Shorthand
```css
/* grid-area: row-start / col-start / row-end / col-end */
.item {
  grid-area: 1 / 1 / 3 / 3;
}
```

### Alignment per Item
```css
.item {
  justify-self: start | end | center | stretch;
  align-self:   start | end | center | stretch;
}
```

---

## 💡 Common Grid Patterns

### Page Layout
```css
.layout {
  display: grid;
  grid-template-columns: 240px 1fr;
  grid-template-rows: 60px 1fr 50px;
  grid-template-areas:
    "header  header"
    "sidebar main"
    "footer  footer";
  min-height: 100vh;
  gap: 0;
}
```

### Responsive Card Grid
```css
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
}
/* Cards auto-wrap and fill available space */
```

### 12-Column Grid
```css
.grid {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: 16px;
}
.col-4 { grid-column: span 4; }
.col-8 { grid-column: span 8; }
```

---

## Flexbox vs Grid

| Feature | Flexbox | Grid |
|---------|---------|------|
| Dimensions | 1D (row or column) | 2D (rows AND columns) |
| Best for | Components, navbars | Full page layouts |
| Content vs Layout | Content drives layout | Layout drives placement |
| Browser support | Excellent | Excellent |

> **Rule of thumb:** Use Grid for the page layout; use Flexbox inside components.

---

## 📝 Interview Questions

**Q1. What is the difference between Flexbox and CSS Grid?**
> Flexbox is one-dimensional (works along one axis at a time). Grid is two-dimensional (rows and columns simultaneously). Use Flexbox for components and linear layouts, Grid for full page layouts and complex two-axis positioning.

**Q2. What is the `fr` unit in CSS Grid?**
> `fr` stands for *fraction* of available space. `repeat(3, 1fr)` creates 3 equal columns that share the available space. `2fr 1fr` makes the first column twice as wide as the second.

**Q3. What does `repeat(auto-fit, minmax(200px, 1fr))` do?**
> It creates as many columns as fit in the container, each at least 200px wide and growing to fill available space. This creates a fully responsive grid with no media queries.

**Q4. What is the difference between `auto-fit` and `auto-fill`?**
> Both create as many columns as fit. With `auto-fill`, empty columns still occupy space. With `auto-fit`, empty columns collapse to 0 width, allowing items to stretch and fill the row.

**Q5. How do you make one item span multiple columns?**
> Use `grid-column: 1 / 3` (from line 1 to 3) or `grid-column: span 2` (span 2 columns from wherever it lands).

**Q6. What is `grid-template-areas` and why is it useful?**
> It lets you define the layout using named areas in an ASCII-art style. It makes the layout visually obvious in the CSS and lets you easily rearrange regions by just editing the template string.

**Q7. Can Grid items overlap? How?**
> Yes. You can assign multiple items to the same grid lines or areas. Use `z-index` to control which appears on top.

---

*Next: Positioning →*
