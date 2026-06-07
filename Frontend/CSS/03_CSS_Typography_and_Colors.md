# CSS – Typography & Colors

---

## 📘 Typography

### Font Properties

```css
p {
  font-family: 'Segoe UI', Arial, sans-serif;  /* font stack */
  font-size: 16px;
  font-weight: bold;      /* normal | bold | 100–900 */
  font-style: italic;     /* normal | italic | oblique */
  font-variant: small-caps;
  line-height: 1.6;       /* unitless = recommended */
}

/* Shorthand: style variant weight size/line-height font-family */
font: italic bold 16px/1.5 Arial, sans-serif;
```

### Font Size Units

| Unit | Description | Example |
|------|-------------|---------|
| `px` | Fixed pixels | `16px` |
| `em` | Relative to **parent** font-size | `1.5em` |
| `rem` | Relative to **root** (`html`) font-size | `1rem` |
| `%` | Relative to parent | `150%` |
| `vw/vh` | Relative to viewport width/height | `5vw` |

```css
html { font-size: 16px; }  /* 1rem = 16px */
h1   { font-size: 2rem; }  /* 32px */
p    { font-size: 1rem; }  /* 16px */
```

### Text Properties

```css
p {
  color: #333;
  text-align: left | center | right | justify;
  text-decoration: none | underline | line-through | overline;
  text-transform: uppercase | lowercase | capitalize;
  letter-spacing: 2px;
  word-spacing: 4px;
  text-indent: 30px;
  white-space: nowrap | pre | pre-wrap | normal;
  text-overflow: ellipsis;   /* requires overflow: hidden + white-space: nowrap */
  overflow: hidden;
}
```

### Google Fonts (External)
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap" rel="stylesheet">
```
```css
body { font-family: 'Roboto', sans-serif; }
```

---

## 🎨 Colors

### Color Formats

```css
/* Named colors */
color: red;
color: tomato;
color: cornflowerblue;

/* Hex */
color: #ff0000;        /* red */
color: #f00;           /* shorthand */
color: #ff000088;      /* with alpha (8-digit hex) */

/* RGB */
color: rgb(255, 0, 0);
color: rgba(255, 0, 0, 0.5);  /* 50% transparent */

/* HSL (Hue Saturation Lightness) */
color: hsl(0, 100%, 50%);         /* red */
color: hsla(0, 100%, 50%, 0.5);   /* transparent red */

/* Modern CSS (no comma) */
color: rgb(255 0 0 / 50%);
color: hsl(0 100% 50% / 50%);
```

### Background Properties

```css
div {
  background-color: #f4f4f4;
  background-image: url('image.jpg');
  background-repeat: no-repeat | repeat | repeat-x | repeat-y;
  background-position: center center;
  background-size: cover | contain | 100% auto;
  background-attachment: fixed | scroll;

  /* Shorthand */
  background: #f4f4f4 url('img.jpg') no-repeat center/cover;
}
```

### CSS Gradients

```css
/* Linear gradient */
background: linear-gradient(to right, #ff6b6b, #ffa500);
background: linear-gradient(135deg, #667eea, #764ba2);

/* Radial gradient */
background: radial-gradient(circle, #ff6b6b, #333);

/* Multiple stops */
background: linear-gradient(to right, red 0%, yellow 50%, green 100%);
```

### CSS Custom Properties (Variables)

```css
:root {
  --primary-color: #3498db;
  --secondary-color: #2ecc71;
  --font-size-base: 16px;
  --spacing-md: 1rem;
}

button {
  background-color: var(--primary-color);
  font-size: var(--font-size-base);
  padding: var(--spacing-md);
}

/* Override variable in a specific scope */
.dark-theme {
  --primary-color: #1a73e8;
}
```

---

## 📝 Interview Questions

**Q1. What is the difference between `em` and `rem`?**
> `em` is relative to the *parent element's* font-size — can compound with nesting. `rem` is always relative to the *root HTML element's* font-size, making it more predictable and consistent.

**Q2. Why is `line-height: 1.5` preferred over `line-height: 24px`?**
> Unitless values scale proportionally with font size changes. `1.5` means 1.5 × the element's font-size, maintaining readability at any size. A fixed `px` value won't scale when font size changes.

**Q3. What is the difference between `rgb()` and `rgba()`?**
> `rgb()` takes 3 values (red, green, blue 0–255). `rgba()` adds a 4th value — the **alpha channel** (0 = fully transparent, 1 = fully opaque) for transparency.

**Q4. What are CSS custom properties (variables) and why use them?**
> CSS variables store reusable values using `--name` syntax, accessed via `var()`. They help maintain consistency, make theming easier, and reduce repetition across a stylesheet.

**Q5. What is `text-overflow: ellipsis` and what properties must accompany it?**
> It truncates overflowing text with `...`. It requires `overflow: hidden` and `white-space: nowrap` to work — without those, the text will wrap or overflow instead.

**Q6. What is `background-size: cover` vs `contain`?**
> `cover` scales the image to fill the entire container (may crop). `contain` scales it to fit entirely within the container (may leave empty space). Both preserve aspect ratio.

**Q7. What is HSL and why might a developer prefer it over hex?**
> HSL (Hue, Saturation, Lightness) is human-readable. You can easily adjust lightness to make a color darker/lighter, or saturation to mute it — much harder to intuit from hex values.

---

*Next: Flexbox →*
