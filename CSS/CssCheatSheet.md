# 📘 Complete CSS Cheat Sheet

A comprehensive guide covering all essential CSS concepts with examples.

---

## 📌 Table of Contents
1. [Selectors](#selectors)
2. [Units](#units)
3. [Pseudo Selectors](#pseudo-selectors)
4. [List Styling](#list-styling)
5. [Position](#position)
6. [Background](#background)
7. [Font Properties](#font-properties)
8. [Text Properties](#text-properties)
9. [Transition](#transition)
10. [Animation](#animation)
11. [Transform](#transform)

---

## 1️⃣ Selectors

### Basic Selectors

```css
/* Universal Selector - Selects all elements */
* {
  margin: 0;
  padding: 0;
}

/* Element Selector - Selects all <p> tags */
p {
  color: blue;
}

/* Class Selector - Selects elements with class="container" */
.container {
  width: 100%;
}

/* ID Selector - Selects element with id="header" */
#header {
  background: #333;
}

/* Multiple Selectors - Groups selectors */
h1, h2, h3 {
  font-family: Arial;
}
```

### Combinators

```css
/* Descendant Selector - All <p> inside <div> */
div p {
  color: red;
}

/* Child Selector - Direct children only */
div > p {
  color: green;
}

/* Adjacent Sibling - Immediately after */
h1 + p {
  font-weight: bold;
}

/* General Sibling - All siblings after */
h1 ~ p {
  color: gray;
}
```

### Attribute Selectors

```css
/* Has attribute */
[type] {
  border: 1px solid;
}

/* Exact match */
[type="text"] {
  background: white;
}

/* Contains word */
[class~="button"] {
  cursor: pointer;
}

/* Starts with */
[href^="https"] {
  color: green;
}

/* Ends with */
[src$=".jpg"] {
  border: 2px solid;
}

/* Contains substring */
[href*="example"] {
  text-decoration: underline;
}
```

---

## 2️⃣ Units

### Absolute Units

```css
.element {
  /* Pixels - Most common */
  width: 200px;
  
  /* Points - Used in print */
  font-size: 12pt;
  
  /* Centimeters */
  margin: 1cm;
  
  /* Millimeters */
  padding: 10mm;
  
  /* Inches */
  width: 2in;
}
```

### Relative Units

```css
.parent {
  font-size: 16px;
}

.child {
  /* em - Relative to parent font-size */
  font-size: 2em; /* 32px */
  padding: 1.5em; /* 24px */
  
  /* rem - Relative to root (html) font-size */
  margin: 2rem; /* 32px if root is 16px */
  
  /* % - Relative to parent */
  width: 50%; /* Half of parent width */
  
  /* vw - Viewport width (1vw = 1% of viewport width) */
  width: 50vw; /* 50% of screen width */
  
  /* vh - Viewport height */
  height: 100vh; /* Full screen height */
  
  /* vmin - Smaller of vw or vh */
  font-size: 5vmin;
  
  /* vmax - Larger of vw or vh */
  font-size: 5vmax;
}

/* ch - Width of "0" character */
.text {
  max-width: 60ch; /* ~60 characters wide */
}

/* ex - Height of lowercase "x" */
.subscript {
  font-size: 1ex;
}
```

---

## 3️⃣ Pseudo Selectors

### Pseudo-Classes (State-based)

```css
/* Link states */
a:link { color: blue; }
a:visited { color: purple; }
a:hover { color: red; }
a:active { color: orange; }
a:focus { outline: 2px solid blue; }

/* Form states */
input:enabled { background: white; }
input:disabled { background: gray; }
input:checked { border: 2px solid green; }
input:required { border-left: 3px solid red; }
input:optional { border-left: 3px solid green; }
input:valid { border-color: green; }
input:invalid { border-color: red; }
input:in-range { background: lightgreen; }
input:out-of-range { background: lightcoral; }

/* Structural pseudo-classes */
p:first-child { font-weight: bold; }
p:last-child { margin-bottom: 0; }
p:only-child { text-align: center; }
p:nth-child(2) { color: blue; }
p:nth-child(odd) { background: #f0f0f0; }
p:nth-child(even) { background: white; }
p:nth-child(3n) { color: red; } /* Every 3rd */
p:nth-last-child(2) { font-style: italic; }

/* Type-based */
p:first-of-type { font-size: 1.2em; }
p:last-of-type { margin-bottom: 0; }
p:nth-of-type(2) { color: green; }
p:only-of-type { text-align: center; }

/* Other useful pseudo-classes */
div:empty { display: none; }
:root { --main-color: #333; } /* CSS variables */
p:not(.special) { color: gray; }
:target { background: yellow; } /* Matched by URL #fragment */
```

### Pseudo-Elements (Parts of elements)

```css
/* First line/letter */
p::first-line {
  font-weight: bold;
}

p::first-letter {
  font-size: 2em;
  float: left;
}

/* Before/After (requires content property) */
.quote::before {
  content: "❝ ";
  color: gray;
}

.quote::after {
  content: " ❞";
  color: gray;
}

/* Selection styling */
::selection {
  background: yellow;
  color: black;
}

/* Placeholder text */
input::placeholder {
  color: #999;
  font-style: italic;
}

/* Marker (list bullets/numbers) */
li::marker {
  color: red;
  font-weight: bold;
}
```

---

## 4️⃣ List Styling

```css
/* List style type */
ul {
  list-style-type: disc;        /* Default */
  list-style-type: circle;
  list-style-type: square;
  list-style-type: none;         /* Remove bullets */
}

ol {
  list-style-type: decimal;      /* 1, 2, 3 */
  list-style-type: decimal-leading-zero; /* 01, 02, 03 */
  list-style-type: lower-roman;  /* i, ii, iii */
  list-style-type: upper-roman;  /* I, II, III */
  list-style-type: lower-alpha;  /* a, b, c */
  list-style-type: upper-alpha;  /* A, B, C */
  list-style-type: lower-greek;  /* α, β, γ */
}

/* List style position */
ul {
  list-style-position: inside;   /* Bullet inside content */
  list-style-position: outside;  /* Bullet outside (default) */
}

/* Custom list image */
ul {
  list-style-image: url('arrow.png');
}

/* Shorthand */
ul {
  list-style: square inside url('bullet.png');
  /*          type   position image */
}

/* Custom styled lists */
ul.custom {
  list-style: none;
  padding-left: 0;
}

ul.custom li {
  padding-left: 1.5em;
  position: relative;
}

ul.custom li::before {
  content: "→";
  position: absolute;
  left: 0;
  color: blue;
}

/* Counter-based custom numbering */
ol.custom-counter {
  counter-reset: item;
  list-style: none;
}

ol.custom-counter li {
  counter-increment: item;
}

ol.custom-counter li::before {
  content: "Step " counter(item) ": ";
  font-weight: bold;
  color: #333;
}
```

---

## 5️⃣ Position

```css
/* Static - Default, normal flow */
.static {
  position: static;
  /* top, right, bottom, left don't work */
}

/* Relative - Positioned relative to normal position */
.relative {
  position: relative;
  top: 10px;      /* Moves down 10px */
  left: 20px;     /* Moves right 20px */
  /* Original space is preserved */
}

/* Absolute - Positioned relative to nearest positioned ancestor */
.absolute {
  position: absolute;
  top: 0;
  right: 0;
  /* Removed from normal flow */
  /* Parent must have position: relative/absolute/fixed */
}

/* Fixed - Positioned relative to viewport */
.fixed {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  /* Stays in place during scroll */
  z-index: 1000;
}

/* Sticky - Hybrid of relative and fixed */
.sticky {
  position: sticky;
  top: 0;
  /* Acts relative until scroll threshold, then fixed */
}

/* Z-index - Stacking order (only works with positioned elements) */
.layer1 { z-index: 1; }
.layer2 { z-index: 10; }
.layer3 { z-index: 100; }

/* Common use cases */

/* Centered absolute element */
.centered {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

/* Full coverage overlay */
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
}

/* Sticky header */
.header {
  position: sticky;
  top: 0;
  background: white;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}
```

---

## 6️⃣ Background

```css
/* Background color */
.element {
  background-color: red;
  background-color: #ff0000;
  background-color: rgb(255, 0, 0);
  background-color: rgba(255, 0, 0, 0.5); /* With transparency */
  background-color: hsl(0, 100%, 50%);
  background-color: transparent;
}

/* Background image */
.element {
  background-image: url('image.jpg');
  background-image: url('https://example.com/image.png');
  
  /* Multiple backgrounds */
  background-image: url('front.png'), url('back.jpg');
}

/* Background repeat */
.element {
  background-repeat: repeat;      /* Default */
  background-repeat: repeat-x;    /* Horizontal only */
  background-repeat: repeat-y;    /* Vertical only */
  background-repeat: no-repeat;   /* Once only */
  background-repeat: space;       /* Repeat with spacing */
  background-repeat: round;       /* Repeat and stretch to fit */
}

/* Background position */
.element {
  background-position: left top;
  background-position: center;
  background-position: right bottom;
  background-position: 50% 50%;
  background-position: 10px 20px;
  background-position: center top 20px; /* Offset from position */
}

/* Background size */
.element {
  background-size: auto;          /* Original size */
  background-size: cover;         /* Cover entire element */
  background-size: contain;       /* Fit inside element */
  background-size: 100px 200px;   /* Specific size */
  background-size: 50% 50%;       /* Percentage */
}

/* Background attachment */
.element {
  background-attachment: scroll;  /* Scrolls with content (default) */
  background-attachment: fixed;   /* Fixed to viewport (parallax) */
  background-attachment: local;   /* Scrolls with element's content */
}

/* Background origin */
.element {
  background-origin: padding-box; /* Default */
  background-origin: border-box;
  background-origin: content-box;
}

/* Background clip */
.element {
  background-clip: border-box;    /* Default */
  background-clip: padding-box;
  background-clip: content-box;
  background-clip: text;          /* Clip to text (with -webkit-) */
  -webkit-background-clip: text;
  color: transparent;             /* Makes gradient text */
}

/* Gradient backgrounds */
.element {
  /* Linear gradient */
  background: linear-gradient(to right, red, blue);
  background: linear-gradient(45deg, red, yellow, green);
  background: linear-gradient(to bottom, rgba(0,0,0,0), rgba(0,0,0,1));
  
  /* Radial gradient */
  background: radial-gradient(circle, red, blue);
  background: radial-gradient(ellipse at center, red, yellow, green);
  
  /* Conic gradient */
  background: conic-gradient(red, yellow, green, blue, red);
  background: conic-gradient(from 45deg, red, blue);
}

/* Shorthand property */
.element {
  background: #fff url('bg.jpg') no-repeat center/cover fixed;
  /*          color image        repeat    position/size attachment */
}

/* Multiple backgrounds */
.element {
  background: 
    url('front.png') no-repeat top right,
    url('middle.png') repeat-x center,
    url('back.jpg') no-repeat center/cover;
}

/* Common patterns */

/* Hero section with overlay */
.hero {
  background: 
    linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.5)),
    url('hero.jpg') center/cover no-repeat;
}

/* Parallax effect */
.parallax {
  background: url('mountain.jpg') center/cover fixed;
  min-height: 500px;
}

/* Gradient text */
.gradient-text {
  background: linear-gradient(45deg, #f06, #48f);
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
  color: transparent;
}
```

---

## 7️⃣ Font Properties

```css
/* Font family */
.element {
  font-family: Arial;
  font-family: 'Times New Roman', serif;
  font-family: Georgia, 'Times New Roman', serif; /* Fallbacks */
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

/* Generic font families */
.element {
  font-family: serif;      /* Times, Georgia */
  font-family: sans-serif; /* Arial, Helvetica */
  font-family: monospace;  /* Courier, Monaco */
  font-family: cursive;    /* Comic Sans, Brush Script */
  font-family: fantasy;    /* Impact, Papyrus */
}

/* Font size */
.element {
  font-size: 16px;
  font-size: 1em;
  font-size: 1.5rem;
  font-size: 100%;
  font-size: larger;
  font-size: smaller;
  font-size: xx-small;  /* Keywords: xx-small to xx-large */
  font-size: small;
  font-size: medium;
  font-size: large;
  font-size: x-large;
  font-size: xx-large;
}

/* Font weight */
.element {
  font-weight: normal;    /* 400 */
  font-weight: bold;      /* 700 */
  font-weight: bolder;    /* Relative to parent */
  font-weight: lighter;
  font-weight: 100;       /* Thin */
  font-weight: 200;       /* Extra Light */
  font-weight: 300;       /* Light */
  font-weight: 400;       /* Normal */
  font-weight: 500;       /* Medium */
  font-weight: 600;       /* Semi Bold */
  font-weight: 700;       /* Bold */
  font-weight: 800;       /* Extra Bold */
  font-weight: 900;       /* Black */
}

/* Font style */
.element {
  font-style: normal;
  font-style: italic;
  font-style: oblique;
  font-style: oblique 10deg; /* With angle */
}

/* Font variant */
.element {
  font-variant: normal;
  font-variant: small-caps;     /* SMALL CAPS TEXT */
  font-variant: all-small-caps;
  font-variant: petite-caps;
  font-variant: all-petite-caps;
}

/* Font stretch */
.element {
  font-stretch: normal;
  font-stretch: ultra-condensed;
  font-stretch: extra-condensed;
  font-stretch: condensed;
  font-stretch: semi-condensed;
  font-stretch: semi-expanded;
  font-stretch: expanded;
  font-stretch: extra-expanded;
  font-stretch: ultra-expanded;
}

/* Line height */
.element {
  line-height: normal;    /* ~1.2 */
  line-height: 1.5;       /* Multiplier (recommended) */
  line-height: 150%;
  line-height: 24px;
  line-height: 1.5em;
}

/* Font shorthand */
.element {
  font: italic small-caps bold 16px/1.5 Arial, sans-serif;
  /*    style  variant      weight size/line-height family */
}

/* Minimum shorthand */
.element {
  font: 16px Arial;
  font: 1rem/1.5 'Helvetica Neue', sans-serif;
}

/* Google Fonts / Web Fonts */
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;700&display=swap');

.element {
  font-family: 'Roboto', sans-serif;
}

/* Custom fonts with @font-face */
@font-face {
  font-family: 'CustomFont';
  src: url('font.woff2') format('woff2'),
       url('font.woff') format('woff'),
       url('font.ttf') format('truetype');
  font-weight: normal;
  font-style: normal;
  font-display: swap; /* Performance optimization */
}

.element {
  font-family: 'CustomFont', sans-serif;
}

/* Variable fonts */
@font-face {
  font-family: 'InterVariable';
  src: url('Inter-Variable.woff2') format('woff2');
  font-weight: 100 900; /* Range */
}

.element {
  font-family: 'InterVariable', sans-serif;
  font-weight: 450; /* Any value in range */
  font-variation-settings: 'wght' 450, 'slnt' -10;
}
```

---

## 8️⃣ Text Properties

```css
/* Text color */
.element {
  color: red;
  color: #ff0000;
  color: rgb(255, 0, 0);
  color: rgba(255, 0, 0, 0.5);
  color: hsl(0, 100%, 50%);
}

/* Text alignment */
.element {
  text-align: left;
  text-align: right;
  text-align: center;
  text-align: justify;      /* Stretch to fill width */
  text-align: start;        /* Same as left in LTR */
  text-align: end;          /* Same as right in LTR */
}

/* Vertical alignment (inline/table-cell elements) */
.element {
  vertical-align: baseline;  /* Default */
  vertical-align: top;
  vertical-align: middle;
  vertical-align: bottom;
  vertical-align: text-top;
  vertical-align: text-bottom;
  vertical-align: sub;       /* Subscript */
  vertical-align: super;     /* Superscript */
  vertical-align: 10px;      /* Custom offset */
}

/* Text decoration */
.element {
  text-decoration: none;
  text-decoration: underline;
  text-decoration: overline;
  text-decoration: line-through;
  text-decoration: underline wavy red; /* style color */
}

/* Individual properties */
.element {
  text-decoration-line: underline;
  text-decoration-style: solid;    /* solid, double, dotted, dashed, wavy */
  text-decoration-color: red;
  text-decoration-thickness: 2px;
}

/* Text transform */
.element {
  text-transform: none;
  text-transform: uppercase;    /* ALL CAPS */
  text-transform: lowercase;    /* all lowercase */
  text-transform: capitalize;   /* First Letter Of Each Word */
  text-transform: full-width;
}

/* Text indent */
.element {
  text-indent: 50px;
  text-indent: 2em;
  text-indent: 10%;
  text-indent: -9999px; /* Hide text (image replacement) */
}

/* Letter spacing */
.element {
  letter-spacing: normal;
  letter-spacing: 2px;
  letter-spacing: 0.1em;
  letter-spacing: -1px;  /* Tighter spacing */
}

/* Word spacing */
.element {
  word-spacing: normal;
  word-spacing: 5px;
  word-spacing: 0.3em;
}

/* White space handling */
.element {
  white-space: normal;      /* Default, collapses whitespace */
  white-space: nowrap;      /* No wrapping */
  white-space: pre;         /* Preserves all whitespace */
  white-space: pre-wrap;    /* Preserves whitespace, wraps */
  white-space: pre-line;    /* Preserves line breaks only */
  white-space: break-spaces;
}

/* Text overflow */
.element {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: clip;      /* Cut off */
  text-overflow: ellipsis;  /* Show ... */
  text-overflow: "»";       /* Custom string */
}

/* Multi-line ellipsis */
.multiline-ellipsis {
  display: -webkit-box;
  -webkit-line-clamp: 3;    /* Number of lines */
  -webkit-box-orient: vertical;
  overflow: hidden;
}

/* Word break */
.element {
  word-break: normal;
  word-break: break-all;    /* Break anywhere */
  word-break: keep-all;     /* Don't break CJK text */
  word-break: break-word;   /* Break long words */
}

/* Overflow wrap (word wrap) */
.element {
  overflow-wrap: normal;
  overflow-wrap: break-word;    /* Break long words if needed */
  overflow-wrap: anywhere;
}

/* Hyphens */
.element {
  hyphens: none;
  hyphens: manual;     /* Only at &shy; or <wbr> */
  hyphens: auto;       /* Automatic hyphenation */
}

/* Text shadow */
.element {
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
  /*           x   y   blur color */
  
  /* Multiple shadows */
  text-shadow: 
    2px 2px 4px rgba(0, 0, 0, 0.5),
    -2px -2px 4px rgba(255, 255, 255, 0.5);
}

/* Writing mode */
.element {
  writing-mode: horizontal-tb;  /* Default, top to bottom */
  writing-mode: vertical-rl;    /* Vertical, right to left */
  writing-mode: vertical-lr;    /* Vertical, left to right */
}

/* Text orientation */
.element {
  text-orientation: mixed;      /* Default */
  text-orientation: upright;
  text-orientation: sideways;
}

/* Direction */
.element {
  direction: ltr;  /* Left to right */
  direction: rtl;  /* Right to left */
}

/* Text rendering (performance vs quality) */
.element {
  text-rendering: auto;
  text-rendering: optimizeSpeed;
  text-rendering: optimizeLegibility;  /* Better kerning */
  text-rendering: geometricPrecision;
}

/* Column layout for text */
.element {
  column-count: 3;
  column-width: 200px;
  column-gap: 20px;
  column-rule: 1px solid #ccc;
  
  /* Shorthand */
  columns: 3 200px;  /* count width */
}

/* Prevent column breaks */
.no-break {
  break-inside: avoid;
  page-break-inside: avoid; /* Older browsers */
}

/* Common text patterns */

/* Truncate with ellipsis */
.truncate {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  max-width: 200px;
}

/* Responsive font size */
.responsive-text {
  font-size: calc(16px + 0.5vw);
  font-size: clamp(14px, 2vw, 24px); /* min, preferred, max */
}

/* Accessible hidden text */
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}
```

---

## 9️⃣ Transition

```css
/* Basic transition */
.element {
  transition: all 0.3s ease;
  /*          property duration timing-function */
}

/* Transition property (what to animate) */
.element {
  transition-property: all;
  transition-property: background-color;
  transition-property: width, height, opacity;
  transition-property: transform, opacity;
}

/* Transition duration */
.element {
  transition-duration: 0.3s;
  transition-duration: 300ms;
  transition-duration: 1s, 0.5s, 2s; /* Multiple properties */
}

/* Transition timing function (easing) */
.element {
  transition-timing-function: ease;          /* Slow-fast-slow (default) */
  transition-timing-function: linear;        /* Constant speed */
  transition-timing-function: ease-in;       /* Slow start */
  transition-timing-function: ease-out;      /* Slow end */
  transition-timing-function: ease-in-out;   /* Slow start and end */
  
  /* Cubic bezier (custom) */
  transition-timing-function: cubic-bezier(0.42, 0, 0.58, 1);
  
  /* Steps */
  transition-timing-function: steps(4);
  transition-timing-function: steps(10, start);
  transition-timing-function: steps(10, end);
}

/* Transition delay */
.element {
  transition-delay: 0s;
  transition-delay: 0.5s;
  transition-delay: 200ms;
}

/* Shorthand syntax */
.element {
  transition: property duration timing-function delay;
  
  /* Examples */
  transition: all 0.3s ease 0s;
  transition: opacity 0.5s linear;
  transition: transform 0.3s ease-in-out 0.1s;
  
  /* Multiple transitions */
  transition: 
    background-color 0.3s ease,
    transform 0.5s ease-in-out,
    opacity 0.2s linear 0.1s;
}

/* Common use cases */

/* Hover effect */
.button {
  background-color: blue;
  transform: scale(1);
  transition: all 0.3s ease;
}

.button:hover {
  background-color: darkblue;
  transform: scale(1.05);
}

/* Smooth color change */
.link {
  color: blue;
  transition: color 0.2s ease;
}

.link:hover {
  color: red;
}

/* Accordion/Dropdown */
.dropdown-content {
  max-height: 0;
  overflow: hidden;
  transition: max-height 0.3s ease-out;
}

.dropdown:hover .dropdown-content {
  max-height: 500px;
}

/* Card lift effect */
.card {
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
  transform: translateY(0);
  transition: box-shadow 0.3s ease, transform 0.3s ease;
}

.card:hover {
  box-shadow: 0 8px 16px rgba(0,0,0,0.2);
  transform: translateY(-5px);
}

/* Smooth width change */
.sidebar {
  width: 250px;
  transition: width 0.3s ease;
}

.sidebar.collapsed {
  width: 60px;
}

/* Fade in/out */
.modal {
  opacity: 0;
  visibility: hidden;
  transition: opacity 0.3s ease, visibility 0.3s ease;
}

.modal.active {
  opacity: 1;
  visibility: visible;
}

/* Performance tip: Only transition transform and opacity */
.optimized {
  transition: transform 0.3s ease, opacity 0.3s ease;
  /* These don't trigger layout reflow */
}

/* Complex example */
.interactive-card {
  background: white;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  transform: scale(1) rotate(0deg);
  opacity: 1;
  transition: 
    transform 0.3s cubic-bezier(0.34, 1.56, 0.64, 1),
    box-shadow 0.3s ease,
    opacity 0.2s ease;
}

.interactive-card:hover {
  transform: scale(1.05) rotate(2deg);
  box-shadow: 0 8px 24px rgba(0,0,0,0.15);
}

.interactive-card:active {
  transform: scale(0.95) rotate(0deg);
  opacity: 0.9;
}
```

---

## 🔟 Animation

```css
/* Define animation with @keyframes */
@keyframes slideIn {
  from {
    transform: translateX(-100%);
    opacity: 0;
  }
  to {
    transform: translateX(0);
    opacity: 1;
  }
}

/* Using percentages */
@keyframes pulse {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.1);
  }
  100% {
    transform: scale(1);
  }
}

/* Multiple keyframes */
@keyframes colorChange {
  0% { background-color: red; }
  25% { background-color: yellow; }
  50% { background-color: green; }
  75% { background-color: blue; }
  100% { background-color: red; }
}

/* Animation properties */

/* Animation name */
.element {
  animation-name: slideIn;
}

/* Animation duration */
.element {
  animation-duration: 2s;
  animation-duration: 500ms;
}

/* Animation timing function */
.element {
  animation-timing-function: ease;
  animation-timing-function: linear;
  animation-timing-function: ease-in;
  animation-timing-function: ease-out;
  animation-timing-function: ease-in-out;
  animation-timing-function: cubic-bezier(0.68, -0.55, 0.265, 1.55);
  animation-timing-function: steps(5);
}

/* Animation delay */
.element {
  animation-delay: 0s;
  animation-delay: 1s;
  animation-delay: -0.5s; /* Starts mid-animation */
}

/* Animation iteration count */
.element {
  animation-iteration-count: 1;        /* Play once */
  animation-iteration-count: 3;        /* Play 3 times */
  animation-iteration-count: infinite; /* Loop forever */
}

/* Animation direction */
.element {
  animation-direction: normal;          /* 0% → 100% */
  animation-direction: reverse;         /* 100% → 0% */
  animation-direction: alternate;       /* 0% → 100% → 0% */
  animation-direction: alternate-reverse;
}

/* Animation fill mode */
.element {
  animation-fill-mode: none;      /* Default */
  animation-fill-mode: forwards;  /* Keep final state */
  animation-fill-mode: backwards; /* Apply first keyframe during delay */
  animation-fill-mode: both;      /* Both forwards and backwards */
}

/* Animation play state */
.element {
  animation-play-state: running;  /* Default */
  animation-play-state: paused;   /* Pause animation */
}

.element:hover {
  animation-play-state: paused;
}

/* Shorthand syntax */
.element {
  animation: name duration timing-function delay iteration-count direction fill-mode play-state;
  
  /* Examples */
  animation: slideIn 1s ease 0s 1 normal forwards running;
  animation: pulse 2s infinite;
  animation: colorChange 5s linear infinite;
}

/* Multiple animations */
.element {
  animation: 
    slideIn 1s ease forwards,
    pulse 2s ease-in-out infinite 1s,
    rotate 3s linear infinite;
}

/* Common animation examples */

/* Fade in */
@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

.fade-in {
  animation: fadeIn 0.5s ease-in;
}

/* Slide from left */
@keyframes slideFromLeft {
  from {
    transform: translateX(-100%);
  }
  to {
    transform: translateX(0);
  }
}

/* Bounce */
@keyframes bounce {
  0%, 20%, 50%, 80%, 100% {
    transform: translateY(0);
  }
  40% {
    transform: translateY(-30px);
  }
  60% {
    transform: translateY(-15px);
  }
}

.bounce {
  animation: bounce 2s infinite;
}

/* Shake */
@keyframes shake {
  0%, 100% { transform: translateX(0); }
  10%, 30%, 50%, 70%, 90% { transform: translateX(-10px); }
  20%, 40%, 60%, 80% { transform: translateX(10px); }
}

.shake {
  animation: shake 0.5s;
}

/* Rotate */
@keyframes rotate {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

.spin {
  animation: rotate 2s linear infinite;
}

/* Loading spinner */
@keyframes spinner {
  to {
    transform: rotate(360deg);
  }
}

.loader {
  border: 4px solid #f3f3f3;
  border-top: 4px solid #3498db;
  border-radius: 50%;
  width: 40px;
  height: 40px;
  animation: spinner 1s linear infinite;
}

/* Heartbeat */
@keyframes heartbeat {
  0% { transform: scale(1); }
  14% { transform: scale(1.3); }
  28% { transform: scale(1); }
  42% { transform: scale(1.3); }
  70% { transform: scale(1); }
}

.heartbeat {
  animation: heartbeat 1.3s ease infinite;
}

/* Wave effect */
@keyframes wave {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-20px); }
}

.wave span {
  display: inline-block;
  animation: wave 1s ease-in-out infinite;
}

.wave span:nth-child(2) { animation-delay: 0.1s; }
.wave span:nth-child(3) { animation-delay: 0.2s; }
.wave span:nth-child(4) { animation-delay: 0.3s; }

/* Typing effect */
@keyframes typing {
  from { width: 0; }
  to { width: 100%; }
}

@keyframes blink {
  50% { border-color: transparent; }
}

.typewriter {
  overflow: hidden;
  border-right: 2px solid;
  white-space: nowrap;
  animation: 
    typing 3.5s steps(40, end),
    blink 0.75s step-end infinite;
}

/* Gradient animation */
@keyframes gradientShift {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}

.animated-gradient {
  background: linear-gradient(270deg, #ff6ec4, #7873f5, #4facfe);
  background-size: 400% 400%;
  animation: gradientShift 15s ease infinite;
}

/* Neon glow */
@keyframes neonGlow {
  0%, 100% {
    text-shadow: 
      0 0 10px #fff,
      0 0 20px #fff,
      0 0 30px #fff,
      0 0 40px #0ff,
      0 0 70px #0ff,
      0 0 80px #0ff,
      0 0 100px #0ff;
  }
  50% {
    text-shadow: 
      0 0 5px #fff,
      0 0 10px #fff,
      0 0 15px #fff,
      0 0 20px #0ff,
      0 0 35px #0ff,
      0 0 40px #0ff,
      0 0 50px #0ff;
  }
}

.neon {
  color: #fff;
  animation: neonGlow 1.5s ease-in-out infinite;
}

/* Floating element */
@keyframes float {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-20px);
  }
}

.floating {
  animation: float 3s ease-in-out infinite;
}
```

---

## 1️⃣1️⃣ Transform

```css
/* Transform property combines multiple transformations */

/* Translate - Move element */
.element {
  transform: translate(50px, 100px);      /* X, Y */
  transform: translateX(50px);             /* Horizontal only */
  transform: translateY(100px);            /* Vertical only */
  transform: translateZ(50px);             /* 3D depth */
  transform: translate3d(50px, 100px, 20px); /* X, Y, Z */
}

/* Scale - Resize element */
.element {
  transform: scale(1.5);           /* Uniform scaling (150%) */
  transform: scale(2, 0.5);        /* X, Y (200%, 50%) */
  transform: scaleX(1.5);          /* Horizontal only */
  transform: scaleY(0.5);          /* Vertical only */
  transform: scaleZ(2);            /* 3D depth */
  transform: scale3d(1.5, 2, 1);   /* X, Y, Z */
}

/* Rotate - Spin element */
.element {
  transform: rotate(45deg);        /* 2D rotation */
  transform: rotate(-90deg);
  transform: rotateX(45deg);       /* Rotate around X-axis */
  transform: rotateY(45deg);       /* Rotate around Y-axis */
  transform: rotateZ(45deg);       /* Same as rotate() */
  transform: rotate3d(1, 1, 0, 45deg); /* X, Y, Z, angle */
}

/* Skew - Distort element */
.element {
  transform: skew(20deg, 10deg);   /* X, Y angles */
  transform: skewX(20deg);         /* Horizontal skew */
  transform: skewY(10deg);         /* Vertical skew */
}

/* Matrix - Advanced (combines all) */
.element {
  transform: matrix(1, 0, 0, 1, 0, 0);
  transform: matrix3d(1,0,0,0, 0,1,0,0, 0,0,1,0, 0,0,0,1);
}

/* Perspective - 3D depth */
.parent {
  perspective: 1000px;
  perspective-origin: 50% 50%;
}

.element {
  transform: perspective(1000px) rotateY(45deg);
}

/* Multiple transforms (applied right to left) */
.element {
  transform: translate(50px, 100px) rotate(45deg) scale(1.5);
  /* Scale → Rotate → Translate */
}

/* Transform origin - Point of transformation */
.element {
  transform-origin: center;           /* Default */
  transform-origin: top left;
  transform-origin: bottom right;
  transform-origin: 50% 50%;
  transform-origin: 0 0;              /* Top left corner */
  transform-origin: 100px 200px;
  transform-origin: left center 50px; /* 3D */
}

/* Transform style - Preserve 3D */
.parent {
  transform-style: flat;              /* Default */
  transform-style: preserve-3d;       /* Children in 3D space */
}

/* Backface visibility */
.element {
  backface-visibility: visible;       /* Default */
  backface-visibility: hidden;        /* Hide when rotated 180° */
}

/* Common transform examples */

/* Center element */
.centered {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

/* Hover grow effect */
.card {
  transition: transform 0.3s ease;
}

.card:hover {
  transform: scale(1.05);
}

/* Rotate on hover */
.icon {
  transition: transform 0.3s ease;
}

.icon:hover {
  transform: rotate(360deg);
}

/* Flip card */
.flip-card {
  perspective: 1000px;
}

.flip-card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  transition: transform 0.6s;
  transform-style: preserve-3d;
}

.flip-card:hover .flip-card-inner {
  transform: rotateY(180deg);
}

.flip-card-front,
.flip-card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
}

.flip-card-back {
  transform: rotateY(180deg);
}

/* 3D cube */
.cube {
  width: 200px;
  height: 200px;
  position: relative;
  transform-style: preserve-3d;
  transform: rotateX(-30deg) rotateY(45deg);
  transition: transform 1s;
}

.cube-face {
  position: absolute;
  width: 200px;
  height: 200px;
  border: 2px solid black;
  opacity: 0.8;
}

.cube-face.front  { transform: translateZ(100px); }
.cube-face.back   { transform: rotateY(180deg) translateZ(100px); }
.cube-face.right  { transform: rotateY(90deg) translateZ(100px); }
.cube-face.left   { transform: rotateY(-90deg) translateZ(100px); }
.cube-face.top    { transform: rotateX(90deg) translateZ(100px); }
.cube-face.bottom { transform: rotateX(-90deg) translateZ(100px); }

/* Parallax scrolling effect */
.parallax-layer {
  position: absolute;
  transform: translateZ(-1px) scale(2);
}

/* Skewed section */
.skewed-section {
  position: relative;
  background: #3498db;
  padding: 100px 0;
}

.skewed-section::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: inherit;
  transform: skewY(-3deg);
  transform-origin: top left;
  z-index: -1;
}

/* Bouncing arrow */
.arrow-down {
  animation: bounce-arrow 2s infinite;
}

@keyframes bounce-arrow {
  0%, 20%, 50%, 80%, 100% {
    transform: translateY(0);
  }
  40% {
    transform: translateY(-20px);
  }
  60% {
    transform: translateY(-10px);
  }
}

/* Image zoom on hover */
.image-container {
  overflow: hidden;
}

.image-container img {
  transition: transform 0.5s ease;
}

.image-container:hover img {
  transform: scale(1.2);
}

/* 3D button press */
.button-3d {
  transform: translateY(0);
  box-shadow: 0 5px 0 #2c3e50;
  transition: all 0.1s;
}

.button-3d:active {
  transform: translateY(5px);
  box-shadow: 0 0 0 #2c3e50;
}

/* Perspective text */
.perspective-text {
  perspective: 1000px;
}

.perspective-text span {
  display: inline-block;
  transform: rotateY(20deg);
  transition: transform 0.3s;
}

.perspective-text span:hover {
  transform: rotateY(0deg);
}

/* Combined complex transform */
.complex-transform {
  transform: 
    perspective(1000px)
    translateZ(100px)
    rotateX(10deg)
    rotateY(20deg)
    scale(1.2)
    translate(50px, 20px);
}

/* GPU acceleration (performance) */
.gpu-accelerated {
  transform: translateZ(0);
  will-change: transform;
}
```

---

## 🎯 Quick Reference Summary

### Most Common Patterns

```css
/* Center anything */
.center {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

/* Smooth hover effect */
.hover-effect {
  transition: all 0.3s ease;
}

.hover-effect:hover {
  transform: scale(1.05);
  box-shadow: 0 10px 20px rgba(0,0,0,0.2);
}

/* Truncate text */
.truncate {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

/* Responsive text */
.responsive-text {
  font-size: clamp(1rem, 2vw, 2rem);
}

/* Full screen background */
.hero {
  background: url('image.jpg') center/cover no-repeat;
  min-height: 100vh;
}

/* Gradient text */
.gradient-text {
  background: linear-gradient(45deg, #f06, #48f);
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
}

/* Loading spinner */
.spinner {
  border: 4px solid #f3f3f3;
  border-top: 4px solid #3498db;
  border-radius: 50%;
  width: 40px;
  height: 40px;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}
```

---

## 📚 Best Practices

1. **Use CSS Variables** for maintainable code
2. **Prefer `transform` and `opacity`** for animations (better performance)
3. **Use `rem` and `em`** for scalability
4. **Use `clamp()`** for responsive typography
5. **Add vendor prefixes** when needed
6. **Optimize with `will-change`** for heavy animations
7. **Use semantic class names**
8. **Keep specificity low**
9. **Mobile-first approach**
10. **Test cross-browser compatibility**

---

**Happy Coding! 🚀** 
