# CSS – Box Model

---

## 📘 What is the Box Model?

Every HTML element is a rectangular box made up of **4 layers**:

```
┌──────────────────────────────┐
│           MARGIN             │  ← Outside space (transparent)
│  ┌────────────────────────┐  │
│  │        BORDER          │  │  ← Visible border
│  │  ┌──────────────────┐  │  │
│  │  │     PADDING      │  │  │  ← Inside space (background shows)
│  │  │  ┌────────────┐  │  │  │
│  │  │  │  CONTENT   │  │  │  │  ← Actual content (text/image)
│  │  │  └────────────┘  │  │  │
│  │  └──────────────────┘  │  │
│  └────────────────────────┘  │
└──────────────────────────────┘
```

---

## 📐 Box Model Properties

### Width & Height
```css
div {
  width: 300px;
  height: 150px;
}
```

### Padding (inside space)
```css
/* All sides */
padding: 20px;

/* Top/Bottom  Left/Right */
padding: 10px 20px;

/* Top  Right  Bottom  Left (clockwise) */
padding: 10px 20px 15px 5px;

/* Individual sides */
padding-top: 10px;
padding-right: 20px;
padding-bottom: 10px;
padding-left: 20px;
```

### Margin (outside space)
```css
/* Same shorthand as padding */
margin: 20px;
margin: 10px auto;        /* horizontally center a block element */
margin: 10px 20px 15px 5px;

/* Auto margin centers block elements */
.container {
  width: 800px;
  margin: 0 auto;
}
```

### Border
```css
border: 2px solid #333;
border: 1px dashed red;
border-top: 3px solid blue;

border-radius: 8px;       /* rounded corners */
border-radius: 50%;       /* circle */
```

---

## ⚠️ box-sizing: The Critical Property

### Default: `content-box`
Width/Height = **content only** — padding and border are *added on top*
```css
div {
  box-sizing: content-box;  /* default */
  width: 300px;
  padding: 20px;
  border: 2px solid;
  /* actual rendered width = 300 + 40 + 4 = 344px */
}
```

### Better: `border-box`
Width/Height = **content + padding + border** — total size stays fixed
```css
div {
  box-sizing: border-box;
  width: 300px;
  padding: 20px;
  border: 2px solid;
  /* actual rendered width = 300px (exactly!) */
}
```

### Best Practice — Apply globally:
```css
*, *::before, *::after {
  box-sizing: border-box;
}
```

---

## 📏 Margin Collapse

When two vertical margins meet, they **collapse** into one (the larger value wins).

```css
/* This is margin collapse */
h1 { margin-bottom: 30px; }
p  { margin-top: 20px; }
/* Gap between them = 30px, NOT 50px */
```

> Horizontal margins do NOT collapse. Only vertical (top/bottom) margins do.

---

## 📌 Display Property

```css
display: block;         /* Takes full width, new line */
display: inline;        /* Flows in text, no width/height */
display: inline-block;  /* Inline flow + accepts width/height */
display: none;          /* Removed from layout entirely */
```

| Property | Block | Inline | Inline-block |
|----------|-------|--------|--------------|
| New line | ✅ | ❌ | ❌ |
| Width/Height | ✅ | ❌ | ✅ |
| Padding/Margin | ✅ all sides | ✅ left/right only | ✅ all sides |

---

## 📝 Interview Questions

**Q1. What are the 4 parts of the CSS box model?**
> Content, Padding, Border, and Margin — from inside to outside.

**Q2. What is the difference between `content-box` and `border-box`?**
> With `content-box` (default), padding and border are added to the specified width, making elements larger. With `border-box`, padding and border are *included* in the specified width — making layout math much easier.

**Q3. If `width: 200px`, `padding: 10px`, `border: 5px`, what is the actual rendered width with `content-box`?**
> 200 + 10 + 10 + 5 + 5 = **230px**

**Q4. What is margin collapse and when does it happen?**
> When two vertical margins meet, they collapse into one equal to the larger value. It happens between adjacent block elements and parent-child elements. Horizontal margins never collapse.

**Q5. What is the difference between `padding` and `margin`?**
> Padding is the space *inside* the border (background color shows). Margin is the space *outside* the border (always transparent). Padding affects the element's clickable/visible area; margin affects spacing between elements.

**Q6. How do you horizontally center a block element?**
> Set `margin: 0 auto` with a defined `width` on the element.

**Q7. What is the difference between `display: none` and `visibility: hidden`?**
> `display: none` removes the element from the layout (no space taken). `visibility: hidden` hides the element but it still occupies space in the layout.

---

*Next: Typography & Colors →*
