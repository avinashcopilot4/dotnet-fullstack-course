# CSS – Overflow, Shadows, Miscellaneous & Best Practices

---

## 📘 Overflow

Controls what happens when content is larger than its container.

```css
overflow: visible;  /* default: content spills out */
overflow: hidden;   /* clip the overflow */
overflow: scroll;   /* always show scrollbars */
overflow: auto;     /* show scrollbars only when needed */

overflow-x: hidden;   /* hide horizontal overflow only */
overflow-y: scroll;   /* scroll vertical only */
```

```css
/* Scrollable container */
.scrollable-box {
  height: 200px;
  overflow-y: auto;
  border: 1px solid #ddd;
}
```

---

## 🌑 Box Shadow & Text Shadow

### box-shadow
```css
/* offset-x | offset-y | blur | color */
box-shadow: 4px 4px 10px rgba(0,0,0,0.2);

/* offset-x | offset-y | blur | spread | color */
box-shadow: 0 4px 15px 0 rgba(0,0,0,0.15);

/* Inset shadow */
box-shadow: inset 0 2px 4px rgba(0,0,0,0.1);

/* Multiple shadows */
box-shadow: 0 2px 4px rgba(0,0,0,0.1),
            0 8px 16px rgba(0,0,0,0.15);

/* No shadow (reset) */
box-shadow: none;
```

### text-shadow
```css
/* offset-x | offset-y | blur | color */
text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
text-shadow: 0 0 10px rgba(255, 100, 0, 0.8);  /* glow */
```

---

## 🔲 Border Radius

```css
border-radius: 8px;              /* all corners */
border-radius: 4px 8px 4px 8px; /* TL TR BR BL */
border-radius: 50%;              /* circle (square element) */
border-radius: 999px;            /* pill / capsule shape */

/* Individual corners */
border-top-left-radius: 8px;
border-bottom-right-radius: 50%;
```

---

## 🎭 Opacity & Visibility

```css
/* opacity: 0 = invisible but still takes space */
.faded { opacity: 0.5; }    /* 50% transparent */

/* visibility: hidden = invisible, takes space */
.hidden { visibility: hidden; }

/* display: none = removed from layout entirely */
.gone { display: none; }
```

---

## 🖱️ Cursor

```css
cursor: default;     /* arrow */
cursor: pointer;     /* hand — use on clickable elements */
cursor: text;        /* I-beam */
cursor: move;        /* four arrows */
cursor: not-allowed; /* circle-slash */
cursor: wait;        /* spinner */
cursor: grab;        /* open hand */
cursor: grabbing;    /* closed hand */
```

---

## 📋 Lists

```css
ul {
  list-style-type: disc | circle | square | none;
  list-style-image: url('bullet.png');
  list-style-position: inside | outside;
  list-style: none;        /* remove bullets */
  padding-left: 0;
  margin: 0;
}
```

---

## 🔢 CSS Counters

```css
/* Auto-number sections */
body { counter-reset: section; }

h2::before {
  counter-increment: section;
  content: counter(section) ". ";
}
```

---

## 🔲 Outline vs Border

```css
/* Border: part of the box model (takes up space) */
border: 2px solid blue;

/* Outline: drawn outside border, doesn't affect layout */
outline: 2px solid orange;
outline-offset: 4px;   /* gap between element and outline */
```

> Never remove `:focus` outline without a replacement — it's critical for keyboard accessibility.
```css
/* Accessible replacement */
button:focus-visible {
  outline: 3px solid #005fcc;
  outline-offset: 2px;
}
```

---

## ⚡ CSS Best Practices

1. **Use `box-sizing: border-box` globally** — makes sizing predictable.
2. **Mobile-first approach** — base styles for mobile, enhance for larger screens.
3. **Use CSS variables** — for colors, spacing, fonts. Easy theming and changes.
4. **Prefer `rem` over `px` for font sizes** — respects user browser settings.
5. **Don't remove focus styles** — keyboard users need them.
6. **Avoid `!important`** — it breaks the cascade. Increase specificity instead.
7. **Use semantic class names** — `.card-title` over `.blue-text`.
8. **Organize CSS** — Reset → Base → Layout → Components → Utilities.
9. **Minimize repaints/reflows** — animate `transform` and `opacity` only.
10. **Test across browsers** — use developer tools and browser compatibility checks.

---

## 📝 Interview Questions

**Q1. What is the difference between `overflow: scroll` and `overflow: auto`?**
> `scroll` always shows scrollbars even when content fits. `auto` only shows scrollbars when the content overflows. `auto` is almost always preferred for cleaner UI.

**Q2. What is the difference between `border` and `outline`?**
> Border is part of the box model and affects layout/spacing. Outline is drawn outside the border and does not affect layout or take up space. Outline is often used for focus indicators.

**Q3. Why should you never set `outline: none` on focus without a replacement?**
> Focus outlines indicate which element has keyboard focus. Removing them without a replacement makes the page inaccessible for keyboard and screen reader users.

**Q4. What does `opacity: 0` vs `display: none` vs `visibility: hidden` do?**
> All three hide elements, but differently: `opacity: 0` — invisible, still in layout, still receives events. `visibility: hidden` — invisible, still in layout, no events. `display: none` — removed from layout entirely, no events.

**Q5. What is the `spread` value in `box-shadow`?**
> The 4th value in `box-shadow` (optional). Positive values expand the shadow in all directions; negative values shrink it. Example: `box-shadow: 0 0 0 3px blue;` creates a solid border-like ring.

**Q6. What is `outline-offset`?**
> It creates a gap between the element's border and the outline. Useful for focus rings that don't touch the element, improving visibility.

**Q7. When should `cursor: pointer` be applied?**
> On any element the user can **click** to trigger an action — buttons, links, interactive cards. It signals interactivity. Don't add it to non-interactive decorative elements.

---

*Congratulations — you've covered all the core CSS fundamentals!*
