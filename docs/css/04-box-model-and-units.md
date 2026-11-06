# 04. Box Model and Units

## A. Introduction

Every element is a box. The box has content, padding, a border, and a margin. Understanding those four layers explains why a 500px-wide element can take up 700px on screen, why two margins sometimes collapse, and why `width: 100%` plus padding can overflow its parent.

This chapter uses the Confidential Email page for a controlled box, the Event Flyer for viewport units, and the Rothko Painting for a frame built from borders and padding. It also covers the units you will use most often.

> **Code conventions:** A code block followed by a **Source:** link is a repository example taken from that file; the excerpt may leave out unrelated markup, and the link opens the complete source. A block without a source link is a teaching example — either a generic syntax illustration or a shortened or adapted excerpt named in the surrounding prose. Section H contains new practice tasks, not requirements from the original freeCodeCamp exercises. The original HTML and CSS files are not modified by this course.

## B. Learning objectives

By the end of this chapter you should be able to:

- Name the four layers of the CSS box model.
- Calculate the rendered size of an element with and without `box-sizing: border-box`.
- Centre a block with `margin: 0 auto` and a width.
- Use `max-width` to keep a layout readable on large screens.
- Choose between `px`, `rem`, `em`, `%`, `vw`, `vh`, and `calc()`.
- Explain why percentage heights can behave unexpectedly.
- Identify the box-model choices in the repository examples.

## C. Core concepts

### The four layers

From the inside out:

1. **Content** — the text or child elements.
2. **Padding** — space inside the border, around the content.
3. **Border** — the line between padding and margin.
4. **Margin** — space outside the border, between this box and its neighbours.

```css
.box {
  width: 300px;
  padding: 20px;
  border: 5px solid black;
  margin: 30px;
}
```

With the default `content-box`, the rendered width is:

```text
300px content + 40px padding + 10px border = 350px
```

The margin is outside that width and adds space around the box.

### box-sizing: border-box

With `border-box`, the declared width includes padding and border:

```css
* {
  box-sizing: border-box;
}

.box {
  width: 300px;
  padding: 20px;
  border: 5px solid black;
}
```

Now the visible border box is 300px wide, and the content area shrinks to:

```text
300px - 40px padding - 10px border = 250px
```

The Confidential Email page uses this reset:

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#email {
  padding: 50px;
  margin: 50px auto;
  width: 500px;
  border: 2px solid black;
  background-color: #fff5ee;
  box-shadow: 5px 5px 15px black;
  position: relative;
  box-sizing: border-box;
}
```

The `#email` rule repeats `box-sizing: border-box`, even though the universal reset already applies it. Repetition is harmless here; it makes the rule explicit.

### Centring with auto margins

A block with a definite width can be centred horizontally:

```css
.menu {
  width: 80%;
  max-width: 500px;
  margin-left: auto;
  margin-right: auto;
}
```

`auto` margins absorb the leftover space equally. The Cafe Menu also uses `max-width: 500px` so the menu does not become too wide on a large screen.

`margin: 50px auto;` is the shorthand: 50px top and bottom, auto left and right.

### Padding versus margin

Padding is inside the box and takes the background colour. Margin is outside the box and is always transparent.

```css
.card {
  padding: 20px;
  margin: 20px;
  background-color: white;
}
```

The padding gives the content breathing room inside the white card. The margin separates the card from its neighbours.

### Borders

```css
.frame {
  border: 50px solid black;
}
```

A border has a width, a style, and a colour. `50px solid black` is a thick frame. Borders can also be used to draw shapes, as the Cat Painting does with transparent left and right borders and a coloured bottom border.

### Units

| Unit | Relative to | Good for |
| --- | --- | --- |
| `px` | CSS pixel | Borders, small fixed details |
| `rem` | Root font size | Typography, spacing systems |
| `em` | Current element's font size | Component-relative spacing |
| `%` | Parent or containing block | Fluid widths |
| `vw` | Viewport width | Full-width layouts |
| `vh` | Viewport height | Full-height sections |
| `calc()` | Mixed units | Combining fixed and fluid values |

The Event Flyer uses viewport width and a calculated minimum height:

```css
body {
  width: 90vw;
  min-height: calc(100% - 100px);
  padding-top: 50px;
  padding-bottom: 50px;
  margin-left: auto;
  margin-right: auto;
}
```

`90vw` means 90% of the viewport width. `calc(100% - 100px)` subtracts 100px from the parent's height. The calculation only has a definite result when the parent's height is definite; a percentage height inside an auto-height parent can behave differently than expected.

### max-width and fluid layouts

```css
.newspaper {
  max-width: 800px;
  margin: 50px auto;
  padding: 40px 15px 25px 15px;
}
```

The newspaper is fluid below 800px and stops growing above it. This pattern is more robust than a fixed width because it works on small screens without a media query.

### Overflow

When content is larger than its box, `overflow` decides what happens:

```css
.canvas {
  width: 500px;
  height: 600px;
  overflow: hidden;
}
```

`hidden` clips the overflowing content. The Rothko canvas uses it to keep the painted rectangles inside the canvas. Be careful with `overflow: hidden` on containers that hold focusable content; it can hide focus outlines.

## D. Syntax

```css
.box {
  width: 300px;
  height: 200px;
  padding: 20px 10px;
  border: 2px solid black;
  margin: 20px auto;
  box-sizing: border-box;
}
```

Shorthand order:

- `padding: top right bottom left;`
- `padding: vertical horizontal;`
- `margin: top right bottom left;`
- `margin: vertical horizontal;`

Fluid width:

```css
.container {
  width: 90%;
  max-width: 1200px;
  margin: 0 auto;
}
```

Calculation:

```css
.hero {
  min-height: calc(100vh - 80px);
}
```

## E. Code examples

### Example 1: A bordered email panel

```css
#email {
  padding: 50px;
  margin: 50px auto;
  width: 500px;
  border: 2px solid black;
  background-color: #fff5ee;
  box-shadow: 5px 5px 15px black;
  position: relative;
  box-sizing: border-box;
}
```

Source: [`CSS/The Box Model/Build a Confidential Email Page/style.css`](<../../CSS/The Box Model/Build a Confidential Email Page/style.css>). Status: **Implemented**.

With `border-box`, the panel stays 500px wide. The 50px padding and 2px border are included in that width.

### Example 2: A fluid page width

```css
body {
  background-color: grey;
  font-family: Arial, Helvetica, sans-serif;
  padding-top: 50px;
  padding-bottom: 50px;
  margin-top: 0px;
  margin-bottom: 0px;
  margin-left: auto;
  margin-right: auto;
  width: 90vw;
  min-height: calc(100% - 100px);
}
```

Source: [`CSS/Absolute and Relative Units/Build an Event Flyer Page/style.css`](<../../CSS/Absolute and Relative Units/Build an Event Flyer Page/style.css>). Status: **Implemented**.

The body is 90% of the viewport width and centred with auto margins. The top and bottom padding create space inside the body, while the auto margins centre the body itself.

### Example 3: A frame built from the box model

```css
.frame {
  border: 50px solid black;
  width: 500px;
  padding: 50px;
  margin: 20px auto;
}

.canvas {
  width: 500px;
  height: 600px;
  background-color: #4d0f00;
  overflow: hidden;
  filter: blur(2px);
}
```

Source: [`CSS/The Box Model/Design a Rothko Painting/style.css`](<../../CSS/The Box Model/Design a Rothko Painting/style.css>). Status: **Implemented**.

The Rothko stylesheet does not set `box-sizing: border-box`, so the frame's outer width is 500px content + 100px horizontal padding + 100px horizontal border = 700px. The canvas fits inside the frame's 500px content area. This is a useful example of the default content-box model.

### Example 4: Centred menu with a maximum width

```css
.menu {
  width: 80%;
  background-color: burlywood;
  margin-left: auto;
  margin-right: auto;
  padding: 20px;
  max-width: 500px;
}
```

Source: [`CSS/Basic CSS/Design a Cafe Menu/style.css`](<../../CSS/Basic CSS/Design a Cafe Menu/style.css>). Status: **Implemented**.

On a narrow screen the menu takes 80% of the available width. On a wide screen it stops at 500px.

### Example 5: Nested padding in a card

```css
.business-card {
  width: 300px;
  background-color: lavenderblush;
  padding: 20px;
  margin-top: 100px;
  text-align: center;
  font-size: 16px;
  margin-left: auto;
  margin-right: auto;
  border: 3px solid black;
}
```

Source: [`CSS/Basic CSS/Design a Business Card/style.css`](<../../CSS/Basic CSS/Design a Business Card/style.css>). Status: **Implemented**.

Without `box-sizing: border-box`, the card's outer width is 300px + 40px padding + 6px border = 346px. The source does not set a global reset, so the declared 300px is the content width.

## F. Step-by-step explanation

1. **Draw the box.** Sketch content, padding, border, and margin before writing CSS.
2. **Decide on `box-sizing`.** A global `border-box` reset makes width calculations predictable.
3. **Set a width or a max-width.** Prefer fluid widths with a maximum for content-heavy pages.
4. **Add padding for breathing room.** Padding belongs inside the visual boundary.
5. **Add margins for separation.** Margins belong outside the visual boundary.
6. **Use `auto` margins for horizontal centring.** The element needs a definite width or max-width.
7. **Choose units by role.** `rem` for type and spacing, `%`/`vw` for fluid layout, `px` for borders.
8. **Test the calculated size.** Use the inspector's box model view to see content, padding, border, and margin.
9. **Check for overflow.** A child wider than its parent can cause horizontal scrolling.
10. **Test at 320px and at a large desktop width.** A fluid layout should work at both ends.

## G. Repository implementations

| Implementation | Box-model feature | Status | Source |
| --- | --- | --- | --- |
| Confidential Email | `border-box`, padding, border, shadow, auto margins | Implemented | [Open](<../../CSS/The Box Model/Build a Confidential Email Page/index.html>) |
| Event Flyer | `vw`, `calc()`, viewport-based spacing | Implemented | [Open](<../../CSS/Absolute and Relative Units/Build an Event Flyer Page/index.html>) |
| Rothko Painting | Default content-box, large border, padding, overflow | Implemented | [Open](<../../CSS/The Box Model/Design a Rothko Painting/index.html>) |
| Cafe Menu | Percentage width, `max-width`, auto margins | Implemented | [Open](<../../CSS/Basic CSS/Design a Cafe Menu/index.html>) |
| Business Card | Fixed width, padding, border, auto margins | Implemented | [Open](<../../CSS/Basic CSS/Design a Business Card/index.html>) |
| Newspaper Article | `max-width`, padding, auto margins | Implemented | [Open](<../../CSS/Typography/Build a Newspaper Article/index.html>) |

## H. Additional challenges

These are new practice tasks for this course; they are not requirements from the original exercises.

1. Build a 300px card with 20px padding and a 5px border. Calculate its outer width with and without `border-box`, then verify in the inspector.
2. Centre a 70%-width container with `margin: 0 auto` and a 900px `max-width`.
3. Recreate the Rothko frame with `box-sizing: border-box`. What happens to the canvas size?
4. Build a full-height hero with `min-height: calc(100vh - 80px)` and a fixed 80px header.
5. Create a two-column layout using percentage widths and padding. Does it overflow? Fix it with `border-box`.
6. Make a card whose padding scales with its font size using `em`. Change the font size and observe the padding.
7. Use the browser's box-model inspector to measure one repository card. Record content, padding, border, and margin.

## I. Common mistakes

- **Forgetting that width excludes padding by default.** The rendered box is larger than the declared width.
- **Adding `width: 100%` plus padding without `border-box`.** The element overflows its parent.
- **Using percentage heights without a definite parent height.** The result may be auto rather than the percentage you expected.
- **Confusing padding and margin.** Padding takes the background; margin is transparent.
- **Using fixed widths for content pages.** The layout breaks on small screens.
- **Using `vw` for text without a maximum.** Text can become enormous on wide screens.
- **Centring without a width.** An auto-width block already fills the available space, so auto margins have nothing to distribute.
- **Forgetting `overflow` when clipping art.** Child elements can spill outside the frame.
- **Using `overflow: hidden` on a container with focusable children.** Focus outlines may be clipped.
- **Not testing at 320px.** A layout that works at 1440px may fail on a phone.

## J. Summary

The box model is content, padding, border, and margin. `box-sizing: border-box` makes width include padding and border, which is usually easier to reason about. Auto margins centre a box with a definite width, and `max-width` keeps fluid layouts readable.

Units are tools, not rules. `px` is useful for borders and small details, `rem` for typography and spacing, and percentages or viewport units for fluid layout. The repository shows both content-box and border-box approaches, which makes it a good place to compare the results.

## K. Next module

Continue to [05. Display and Positioning](05-display-and-positioning.md) to learn how boxes participate in normal flow and how to move them without breaking the document.
