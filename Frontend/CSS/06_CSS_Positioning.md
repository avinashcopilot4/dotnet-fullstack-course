# CSS – Positioning

---

## 📘 The `position` Property

The `position` property controls how an element is placed in the document. The offset properties `top`, `right`, `bottom`, and `left` determine its final location.

---

## 🗂️ Position Values

### `static` (default)
Elements flow in normal document order. Offset properties have **no effect**.
```css
div { position: static; }  /* default — offset ignored */
```

### `relative`
Positioned **relative to its own normal position**. Space is still reserved in the document flow.
```css
.box {
  position: relative;
  top: 20px;    /* moves DOWN 20px from normal position */
  left: 30px;   /* moves RIGHT 30px from normal position */
}
```

### `absolute`
Removed from document flow. Positioned **relative to the nearest positioned ancestor** (any position other than `static`).
```css
.parent {
  position: relative;   /* creates positioning context */
}
.child {
  position: absolute;
  top: 0;
  right: 0;             /* top-right corner of parent */
}
```

> If no positioned ancestor exists, it positions relative to the `<html>` element.

### `fixed`
Removed from document flow. Positioned **relative to the viewport** — stays in place when scrolling.
```css
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 1000;
}
```

### `sticky`
Acts like `relative` until the element reaches a scroll threshold, then acts like `fixed`.
```css
.header {
  position: sticky;
  top: 0;           /* sticks when reaching top of viewport */
  background: white;
  z-index: 100;
}
```

---

## ⬆️ z-index

Controls the **stacking order** of positioned elements. Higher value = in front.

```css
.overlay {
  position: fixed;
  z-index: 999;
}
.modal {
  position: fixed;
  z-index: 1000;  /* appears above overlay */
}
```

> `z-index` only works on elements with `position` other than `static`.

---

## 📊 Quick Comparison

| Value | Flow | Positioned Relative To | Scrolls With Page |
|-------|------|------------------------|-------------------|
| `static` | Normal | N/A | ✅ |
| `relative` | Normal (space kept) | Itself | ✅ |
| `absolute` | Removed | Nearest positioned ancestor | ✅ |
| `fixed` | Removed | Viewport | ❌ (stays fixed) |
| `sticky` | Normal → Fixed | Scroll container | Partial |

---

## 💡 Common Patterns

### Overlay on a Card
```css
.card {
  position: relative;
}
.badge {
  position: absolute;
  top: 10px;
  right: 10px;
}
```

### Full Screen Modal Backdrop
```css
.backdrop {
  position: fixed;
  top: 0; left: 0;
  width: 100%; height: 100%;
  background: rgba(0,0,0,0.5);
  z-index: 100;
}
```

### Sticky Table Header
```css
thead th {
  position: sticky;
  top: 0;
  background: white;
}
```

### Centering with Absolute
```css
.parent { position: relative; }

.child {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```

---

## 📝 Interview Questions

**Q1. What is the difference between `absolute` and `relative` positioning?**
> `relative` keeps the element in the normal flow and offsets it from its original position. `absolute` removes it from normal flow entirely and positions it relative to the nearest positioned ancestor.

**Q2. What is a "positioning context"?**
> Any element with `position` other than `static` creates a positioning context (anchor point) for absolutely positioned children. Developers commonly set `position: relative` on a parent just to create this context.

**Q3. What is the difference between `fixed` and `sticky`?**
> `fixed` is always relative to the viewport and never moves with the page scroll. `sticky` is part of the normal flow until it reaches a threshold (e.g., `top: 0`), then it "sticks" like `fixed` — but only within its parent container.

**Q4. When does `z-index` not work?**
> `z-index` only applies to positioned elements (position other than `static`). On a `static` element, setting `z-index` has no effect.

**Q5. What happens if an absolutely positioned element has no positioned ancestor?**
> It positions itself relative to the initial containing block, which is the `<html>` element (effectively the entire page).

**Q6. How do you center a div absolutely within its parent?**
> Set parent to `position: relative`. On the child: `position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%);`.

**Q7. What is the difference between `top: 0` on `fixed` vs `sticky`?**
> On `fixed`, the element immediately stays at the top of the viewport regardless of scroll position. On `sticky`, the element scrolls normally until it *reaches* the top of the viewport (scroll threshold), then sticks — and unsticks when you scroll back past it.

---

*Next: Responsive Design & Media Queries →*
