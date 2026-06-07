# CSS – Flexbox

---

## 📘 What is Flexbox?

Flexbox (Flexible Box Layout) is a **one-dimensional** layout system for arranging items in a row or column. It makes alignment and spacing easy without floats or positioning hacks.

```css
.container {
  display: flex;  /* activate flexbox */
}
```

---

## 🗂️ Flex Container Properties

### flex-direction
Controls the **main axis** direction.
```css
flex-direction: row;            /* → left to right (default) */
flex-direction: row-reverse;    /* ← right to left */
flex-direction: column;         /* ↓ top to bottom */
flex-direction: column-reverse; /* ↑ bottom to top */
```

### justify-content
Aligns items along the **main axis**.
```css
justify-content: flex-start;    /* default: items at start */
justify-content: flex-end;      /* items at end */
justify-content: center;        /* items centered */
justify-content: space-between; /* equal space BETWEEN items */
justify-content: space-around;  /* equal space AROUND items */
justify-content: space-evenly;  /* equal space including edges */
```

### align-items
Aligns items along the **cross axis** (single line).
```css
align-items: stretch;           /* default: fill cross axis */
align-items: flex-start;        /* align to start */
align-items: flex-end;          /* align to end */
align-items: center;            /* vertically centered */
align-items: baseline;          /* align by text baseline */
```

### flex-wrap
Controls whether items wrap to new lines.
```css
flex-wrap: nowrap;    /* default: single line, may overflow */
flex-wrap: wrap;      /* wraps to next line */
flex-wrap: wrap-reverse;
```

### align-content
Aligns **multiple lines** when wrapping (cross axis).
```css
align-content: flex-start | flex-end | center |
               space-between | space-around | stretch;
```

### gap
Space between flex items.
```css
gap: 16px;           /* row and column gap */
gap: 10px 20px;      /* row-gap column-gap */
```

### flex-flow (shorthand)
```css
flex-flow: row wrap;   /* flex-direction + flex-wrap */
```

---

## 🧩 Flex Item Properties

### flex-grow
How much an item **grows** to fill available space.
```css
.item { flex-grow: 1; }   /* all items equal width */
.item:nth-child(2) { flex-grow: 2; }  /* twice as wide */
```

### flex-shrink
How much an item **shrinks** when space is tight.
```css
.item { flex-shrink: 1; }   /* default: can shrink */
.item { flex-shrink: 0; }   /* won't shrink */
```

### flex-basis
The **initial size** of an item before grow/shrink.
```css
.item { flex-basis: 200px; }
.item { flex-basis: auto; }  /* default */
```

### flex (shorthand)
```css
flex: 1;            /* grow: 1, shrink: 1, basis: 0 */
flex: 1 1 200px;    /* grow shrink basis */
flex: none;         /* 0 0 auto — no flex */
```

### align-self
Overrides `align-items` for a single item.
```css
.item { align-self: flex-start | flex-end | center | stretch; }
```

### order
Changes visual order (not DOM order).
```css
.item { order: 2; }   /* default is 0 */
```

---

## 💡 Common Flexbox Patterns

### Perfect Centering
```css
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
```

### Navigation Bar
```css
nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem;
}
```

### Equal-Width Cards
```css
.cards {
  display: flex;
  gap: 20px;
}
.card {
  flex: 1;  /* all equal width */
}
```

### Sidebar Layout
```css
.layout {
  display: flex;
}
.sidebar { width: 250px; flex-shrink: 0; }
.main    { flex: 1; }
```

---

## 📝 Interview Questions

**Q1. What is Flexbox and when would you use it?**
> Flexbox is a one-dimensional layout model (row or column). Use it for navbars, card rows, centering elements, distributing space among items, and any layout that aligns along a single axis.

**Q2. What is the difference between `justify-content` and `align-items`?**
> `justify-content` controls alignment along the **main axis** (direction of flex-direction). `align-items` controls alignment along the **cross axis** (perpendicular to main axis).

**Q3. What does `flex: 1` mean?**
> It's shorthand for `flex-grow: 1; flex-shrink: 1; flex-basis: 0`. The item will grow to fill available space equally with other `flex: 1` siblings.

**Q4. How do you perfectly center a div both horizontally and vertically?**
> Apply `display: flex; justify-content: center; align-items: center;` to the parent container.

**Q5. What is the difference between `flex-wrap: wrap` and `nowrap`?**
> `nowrap` (default) keeps all items on one line, potentially causing overflow. `wrap` allows items to wrap onto new lines when they run out of space.

**Q6. What is the difference between `align-items` and `align-content`?**
> `align-items` aligns items within a single flex line. `align-content` aligns multiple flex lines when wrapping is enabled — it has no effect when there's only one line.

**Q7. How does `order` work in Flexbox? Does it change the HTML structure?**
> `order` changes the *visual* order of items. It doesn't change the DOM order — only how items are rendered. Default order is `0`; lower values appear first.

---

*Next: CSS Grid →*
