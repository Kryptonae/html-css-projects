# 05. Display and Positioning

## A. Introduction

Normal flow is the browser's default layout algorithm. Block boxes stack vertically, inline boxes sit in a line, and every element takes up space. Display and positioning properties let you change that behaviour, but they also make it easier to create overlaps, hidden content, and layouts that collapse on small screens.

This chapter starts with `display`, then moves to the `position` property, `z-index`, and floats. The Confidential Email and Cat Painting use absolute positioning for layered art. The Piano uses a legacy float layout. The House Painting folder is a placeholder, so it is documented as unfinished rather than presented as a working example.

> **Code conventions:** A code block followed by a **Source:** link is a repository example taken from that file; the excerpt may leave out unrelated markup, and the link opens the complete source. A block without a source link is a teaching example — either a generic syntax illustration or a shortened or adapted excerpt named in the surrounding prose. Section H contains new practice tasks, not requirements from the original freeCodeCamp exercises. The original HTML and CSS files are not modified by this course.

## B. Learning objectives

By the end of this chapter you should be able to:

- Explain normal flow and how block and inline boxes differ.
- Change an element with `display: block`, `inline`, `inline-block`, `flex`, `grid`, or `none`.
- Use `position: relative`, `absolute`, `fixed`, and `sticky` with a clear containing block.
- Layer positioned elements with `z-index`.
- Understand the purpose and risks of `float`.
- Recognise when absolute positioning helps and when it harms a layout.
- Identify the placeholder and legacy-layout files in the repository.

## C. Core concepts

### Normal flow

In normal flow:

- Block-level elements such as `<div>`, `<p>`, and `<h1>` start on a new line and fill the available width.
- Inline elements such as `<span>`, `<a>`, and `<em>` sit in the text line.
- Margins create space between blocks; vertical margins can collapse when adjacent.

Most pages should work in normal flow. Positioning is an enhancement, not a replacement for structure.

### display

```css
.block {
  display: block;
}

.inline {
  display: inline;
}

.inline-block {
  display: inline-block;
}

.hidden {
  display: none;
}
```

- `block` takes a new line and accepts width and height.
- `inline` stays in the text flow; width and height are ignored.
- `inline-block` stays in the text flow but accepts width, height, margins, and padding.
- `none` removes the element from layout and from the accessibility tree.

The Cafe Menu uses `inline-block` for the flavour and price paragraphs:

```css
.item p {
  display: inline-block;
  margin-top: 5px;
  margin-bottom: 5px;
  font-size: 18px;
}

.flavor,
.dessert {
  text-align: left;
  width: 70%;
}

.price {
  text-align: right;
  width: 29%;
}
```

The two paragraphs sit on one line because they are inline blocks with widths that add up to roughly 99%.

`display: none` is used by the Greeting Card to hide its sections until a link targets them:

```css
section {
  display: none;
}

section:target {
  display: block;
}
```

This is a CSS-only interaction, but it has accessibility consequences: content hidden with `display: none` is unavailable to screen readers and the keyboard until it is shown. Use it deliberately.

### position: relative

`position: relative` keeps the element in normal flow but allows offsets:

```css
#email {
  position: relative;
}
```

Offsets move the element visually without removing the space it originally occupied. It also creates a containing block for absolutely positioned descendants.

### position: absolute

`position: absolute` removes the element from normal flow and positions it relative to its nearest positioned ancestor. If there is no positioned ancestor, it positions relative to the initial containing block.

The Confidential Email uses a relative parent and two absolute stamps:

```css
#email {
  position: relative;
}

#confidential,
#top-secret {
  position: absolute;
}

#confidential {
  top: 50px;
  right: 85px;
  transform: rotate(-15deg);
}

#top-secret {
  right: 90px;
  bottom: 45px;
  transform: rotate(10deg);
}
```

The stamps sit inside the email panel because `#email` is positioned. Without `position: relative` on the parent, they could escape to the page viewport.

### position: fixed

`position: fixed` positions an element relative to the viewport. It stays in place when the page scrolls:

```css
#header {
  position: fixed;
  left: 0;
  right: 0;
}
```

A fixed header or floating action button needs space reserved for it. Otherwise it can cover content at the top or bottom of the page.

### position: sticky

`position: sticky` behaves like relative positioning until a scroll threshold is reached, then sticks:

```css
.summary {
  position: sticky;
  top: 20px;
}
```

The element stays within its parent's bounds. It needs a threshold such as `top`, and it needs a scrolling ancestor. The Balance Sheet uses sticky positioning on `#years`, with `top: 0` and `z-index: 999`, so the year labels stay visible while the table scrolls.

### z-index

`z-index` controls the stacking order of positioned elements:

```css
.cat-left-ear {
  position: absolute;
  z-index: 1;
}
```

A higher `z-index` paints above a lower one, but only within the same stacking context. A positioned parent with its own `z-index` creates a new context, so a child's z-index is relative to that context rather than the whole page.

### Floats

`float: left` or `float: right` pushes an element to the side and lets following content wrap around it:

```css
.key {
  float: left;
}
```

The Piano uses floats for its keys. Its `.keys` container uses `overflow: hidden` to contain the floated children:

```css
.keys {
  background-color: #040404;
  width: 949px;
  height: 180px;
  padding-left: 2px;
  overflow: hidden;
}
```

Floats were the main layout technique before Flexbox and Grid. They are still useful for wrapping text around an image, but they are a poor choice for whole-page layouts today.

### The placeholder page

The House Painting folder contains an `index.html` and an empty `style.css`. The HTML body is empty and does not link the stylesheet. It is a **Placeholder**, not an example of positioning. If you open it, you will see a blank page.

## D. Syntax

```css
/* Normal and display */
div { display: block; }
span { display: inline; }
.card { display: inline-block; }
.hidden { display: none; }

/* Positioning */
.parent { position: relative; }
.badge {
  position: absolute;
  top: 10px;
  right: 10px;
}
.header { position: fixed; top: 0; left: 0; right: 0; }
.sidebar { position: sticky; top: 20px; }

/* Stacking */
.badge { z-index: 2; }

/* Float */
.key { float: left; }
.keys { overflow: hidden; }
```

## E. Code examples

### Example 1: Relative parent, absolute children

```css
#email {
  position: relative;
  box-sizing: border-box;
  width: 500px;
  padding: 50px;
  margin: 50px auto;
  border: 2px solid black;
}

#confidential,
#top-secret {
  position: absolute;
}

#confidential {
  display: inline-block;
  top: 50px;
  right: 85px;
  border: 5px solid red;
  color: red;
  padding: 12px;
  font-size: 1.7rem;
  font-weight: 600;
  transform: rotate(-15deg);
}
```

Source: [`CSS/The Box Model/Build a Confidential Email Page/style.css`](<../../CSS/The Box Model/Build a Confidential Email Page/style.css>). Status: **Implemented**.

The `right` offset is measured from the right edge of the email panel. The rotation is visual only; the stamp still occupies its original box for layout purposes.

### Example 2: Centring an absolutely positioned element

```css
.cat-head {
  position: absolute;
  right: 0;
  left: 0;
  top: 0;
  bottom: 0;
  margin: auto;
  background: linear-gradient(#5e5e5e 85%, #45454f 100%);
  width: 205px;
  height: 180px;
  border: 1px solid #000;
  border-radius: 46%;
}
```

Source: [`CSS/Positioning/Build a Cat Painting/styles.css`](<../../CSS/Positioning/Build a Cat Painting/styles.css>). Status: **Implemented\***.

Setting all four offsets to `0` and using `margin: auto` centres a fixed-size absolutely positioned box. The cat's features are then positioned relative to the cat head, which is the nearest positioned ancestor.

### Example 3: A float-based keyboard

```css
#piano {
  background-color: #00471b;
  width: 992px;
  height: 290px;
  margin: 80px auto;
  padding: 90px 20px 0 20px;
  position: relative;
  border-radius: 10px;
}

.keys {
  background-color: #040404;
  width: 949px;
  height: 180px;
  padding-left: 2px;
  overflow: hidden;
}

.key {
  background-color: #ffffff;
  position: relative;
  width: 41px;
  height: 175px;
  margin: 2px;
  float: left;
  border-radius: 0 0 3px 3px;
}

.key.black--key::after {
  background-color: #1d1e22;
  content: "";
  position: absolute;
  left: -18px;
  width: 32px;
  height: 100px;
  border-radius: 0 0 3px 3px;
}
```

Source: [`CSS/Responsive Design/Design a Piano/style.css`](<../../CSS/Responsive Design/Design a Piano/style.css>). Status: **Implemented**.

The white keys float left, and each black key is a pseudo-element positioned over its white key. The keys container contains the floats with `overflow: hidden`. This works, but it is a visual-only keyboard with no audio or JavaScript.

### Example 4: Fixed header

```css
#header {
  display: flex;
  justify-content: space-around;
  align-items: center;
  padding: 10px 0;
  grid-area: header;
  position: fixed;
  left: 0;
  right: 0;
}
```

Source: [`CSS/CERTIFICATION PROJECTS/Build a Product Landing Page/style.css`](<../../CSS/CERTIFICATION PROJECTS/Build a Product Landing Page/style.css>). Status: **Implemented\***.

Because the header is fixed, it no longer occupies space in the page flow. The page's top spacing needs to account for the header's height, or the first section can sit underneath it.

### Example 5: A placeholder

```html
<body>
</body>
```

Source: [`CSS/Positioning/Build a House Painting/index.html`](<../../CSS/Positioning/Build a House Painting/index.html>). Status: **Placeholder**.

The folder has an empty stylesheet as well. There is no house to inspect and no positioning lesson in the source yet.

## F. Step-by-step explanation

1. **Build the layout in normal flow first.** Do not position elements until the content order makes sense.
2. **Choose display by behaviour.** Block for sections, inline for text-level elements, inline-block for buttons and small boxes.
3. **Use Flexbox or Grid for layout.** Reserve absolute positioning for overlays, badges, and art.
4. **Create a containing block.** Give the positioned parent `position: relative` before positioning a child absolutely.
5. **Set only the offsets you need.** Too many offsets can make the element stretch unexpectedly.
6. **Check the element in the accessibility tree.** `display: none` removes it completely.
7. **Use z-index only on positioned elements.** It has no effect on static elements.
8. **Contain floats.** Use `overflow: hidden`, a clearfix, or a modern layout method.
9. **Test at a small width.** Absolutely positioned art often overflows or overlaps.
10. **Remove positioning that is not needed.** Normal flow is easier to maintain.

## G. Repository implementations

| Implementation | Display/positioning feature | Status | Source |
| --- | --- | --- | --- |
| Confidential Email | Relative parent, absolute stamps, rotation | Implemented | [Open](<../../CSS/The Box Model/Build a Confidential Email Page/index.html>) |
| Cat Painting | Absolute cat head, absolute features, z-index, transforms | Implemented\* | [Open](<../../CSS/Positioning/Build a Cat Painting/index.html>) |
| Piano | Floats, relative/absolute keys, responsive widths | Implemented | [Open](<../../CSS/Responsive Design/Design a Piano/index.html>) |
| Product Landing Page | Fixed header | Implemented\* | [Open](<../../CSS/CERTIFICATION PROJECTS/Build a Product Landing Page/index.html>) |
| Balance Sheet | Sticky year row, flex heading | Implemented\* | [Open](<../../CSS/Attribute Selectors/Build a Balance Sheet/index.html>) |
| Greeting Card | `display: none` and `:target` reveal | Implemented | [Open](<../../CSS/Pseudo Classes and Elements/Design a Greeting Card/index.html>) |
| House Painting | Empty body and empty stylesheet | Placeholder | [Open](<../../CSS/Positioning/Build a House Painting/index.html>) |

## H. Additional challenges

These are new practice tasks for this course; they are not requirements from the original exercises.

1. Rebuild the Confidential Email stamp using `position: absolute` inside a relative card. Move it to each corner.
2. Create a card with a "New" badge in the top-right corner. Confirm that the badge stays inside the card when the text length changes.
3. Replace the Piano's float layout with Flexbox. Compare the source and the result.
4. Build a page with a fixed header and add enough top padding that the first heading is not covered.
5. Create a sticky table of contents inside a scrolling article. Test where it stops.
6. Use `display: none` and `:target` to build a CSS-only tab panel. Check whether keyboard users can reach the hidden content.
7. Make a decorative shape with absolute positioning and `z-index`. Explain which element creates the stacking context.
8. Open the House Painting folder and describe what is missing before it could become a real exercise.

## I. Common mistakes

- **Positioning everything absolutely.** The page loses normal flow and becomes fragile.
- **Forgetting a positioned ancestor.** An absolute child may position against the viewport instead of its card.
- **Using `top` and `bottom` together without a height.** The element can stretch or behave unexpectedly.
- **Using `z-index` on a static element.** It has no effect.
- **Assuming z-index compares across the whole page.** Stacking contexts limit the comparison.
- **Forgetting that fixed elements leave the flow.** Content can hide underneath them.
- **Floating a container's children without containing the floats.** The parent can collapse to zero height.
- **Using `display: none` for content that should be accessible.** Use a visually-hidden utility when the content must remain available.
- **Testing only at desktop size.** Absolute art and fixed headers often break on mobile.

## J. Summary

Normal flow is the baseline. `display` changes how an element participates in that flow; `position` removes it or offsets it; `z-index` controls painting order; floats wrap content and were once used for layout.

The Confidential Email shows a clean relative/absolute relationship. The Cat Painting uses absolute positioning as a drawing technique. The Piano shows the strengths and limits of floats. The Balance Sheet uses sticky positioning for its year row. The House Painting is honest about being unfinished. Choose the least powerful technique that solves the layout problem.

## K. Next module

Continue to [06. Flexbox](06-flexbox.md) to lay out items along a single axis with alignment, wrapping, and flexible sizing.
