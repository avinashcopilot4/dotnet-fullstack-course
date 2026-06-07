# CSS – Transitions & Animations

---

## 📘 CSS Transitions

Transitions create smooth changes between two CSS states (e.g., on hover).

### Syntax
```css
transition: property duration timing-function delay;
```

```css
button {
  background: blue;
  transition: background 0.3s ease;
}

button:hover {
  background: darkblue;
}
```

### Transition Properties

```css
.box {
  transition-property:  background, transform;  /* what to animate */
  transition-duration:  0.3s;                   /* how long */
  transition-timing-function: ease;             /* speed curve */
  transition-delay:     0.1s;                   /* wait before starting */
}

/* Shorthand for multiple properties */
transition: background 0.3s ease, transform 0.5s ease-in-out;

/* Animate everything */
transition: all 0.3s ease;
```

### Timing Functions

```css
transition-timing-function: ease;         /* slow-fast-slow (default) */
transition-timing-function: linear;       /* constant speed */
transition-timing-function: ease-in;      /* slow start */
transition-timing-function: ease-out;     /* slow end */
transition-timing-function: ease-in-out;  /* slow start and end */
transition-timing-function: cubic-bezier(0.25, 0.1, 0.25, 1.0); /* custom */
```

---

## 🎬 CSS Animations

Animations allow complex, multi-step changes using `@keyframes`.

### Defining Keyframes
```css
@keyframes fadeIn {
  from { opacity: 0; }
  to   { opacity: 1; }
}

@keyframes slideUp {
  0%   { transform: translateY(30px); opacity: 0; }
  100% { transform: translateY(0);    opacity: 1; }
}

@keyframes pulse {
  0%   { transform: scale(1); }
  50%  { transform: scale(1.1); }
  100% { transform: scale(1); }
}
```

### Applying Animations
```css
.card {
  animation-name:            fadeIn;
  animation-duration:        0.5s;
  animation-timing-function: ease-out;
  animation-delay:           0.2s;
  animation-iteration-count: 1;          /* or: infinite */
  animation-direction:       normal;     /* reverse | alternate */
  animation-fill-mode:       forwards;   /* keeps end state */
  animation-play-state:      running;    /* or: paused */

  /* Shorthand: name duration timing delay iteration direction fill */
  animation: fadeIn 0.5s ease-out 0.2s 1 normal forwards;
}
```

### animation-fill-mode
```css
animation-fill-mode: none;      /* default: resets after */
animation-fill-mode: forwards;  /* stays at final keyframe */
animation-fill-mode: backwards; /* starts at first keyframe (during delay) */
animation-fill-mode: both;      /* both forwards and backwards */
```

---

## 🔄 CSS `transform`

Transform visually moves/scales/rotates elements **without affecting document flow**.

```css
transform: translateX(50px);        /* move right */
transform: translateY(-20px);       /* move up */
transform: translate(50px, -20px);  /* move right and up */

transform: scale(1.5);              /* 150% of original */
transform: scaleX(2);               /* double width */
transform: scaleY(0.5);             /* half height */

transform: rotate(45deg);           /* clockwise */
transform: rotate(-90deg);          /* counter-clockwise */

transform: skew(15deg);             /* skew */

/* Chain multiple transforms */
transform: translateX(50px) rotate(45deg) scale(1.2);
```

### transform-origin
```css
transform-origin: center;    /* default */
transform-origin: top left;
transform-origin: 0 0;
```

---

## 💡 Common Animation Patterns

### Hover Card Lift
```css
.card {
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}
.card:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 24px rgba(0,0,0,0.15);
}
```

### Loading Spinner
```css
@keyframes spin {
  to { transform: rotate(360deg); }
}

.spinner {
  width: 40px;
  height: 40px;
  border: 4px solid #ddd;
  border-top-color: #3498db;
  border-radius: 50%;
  animation: spin 0.8s linear infinite;
}
```

### Fade In on Load
```css
@keyframes fadeInUp {
  from { opacity: 0; transform: translateY(20px); }
  to   { opacity: 1; transform: translateY(0); }
}

.hero {
  animation: fadeInUp 0.6s ease-out both;
}
```

---

## 📝 Interview Questions

**Q1. What is the difference between CSS transitions and animations?**
> Transitions animate between **two states** (e.g., normal → hover) and require a trigger. Animations use `@keyframes` for **multi-step**, complex sequences that can run automatically and loop.

**Q2. What does `animation-fill-mode: forwards` do?**
> After the animation completes, the element stays at the last keyframe's state instead of reverting to its original styles.

**Q3. What is `transition: all` and why should it be used carefully?**
> It applies a transition to every animatable property. This can cause unexpected animations (e.g., layout reflows) and hurt performance. It's better to specify only the properties you intend to animate.

**Q4. What properties are cheapest to animate?**
> `transform` and `opacity` are the most performant — they run on the GPU and don't trigger layout recalculations. Avoid animating `width`, `height`, `margin`, or `top/left` as they trigger layout reflows.

**Q5. How do you pause a CSS animation?**
> Set `animation-play-state: paused` on the element (often toggled via JavaScript or a class).

**Q6. What does `transform: translate(-50%, -50%)` do?**
> Moves the element left by 50% of its own width and up by 50% of its own height. Combined with `position: absolute; top: 50%; left: 50%;` this perfectly centers an element in its parent.

**Q7. What is `animation-iteration-count: infinite` used for?**
> It makes the animation loop forever. Useful for loaders, spinners, or background animations.

---

*Next: CSS Pseudo-classes, Overflow & Miscellaneous →*
