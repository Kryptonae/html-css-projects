# 06. Flexbox

## A. Introduction

Flexbox is a one-dimensional layout system. It distributes space and aligns items along a main axis and a cross axis. It is ideal for navigation bars, card rows, centred content, and components that need to wrap or grow.

The repository uses Flexbox more than any other layout method. The Photo Gallery wraps images, the Colorful Boxes demonstrate order and growth, the Pricing Plans show flexible cards, and the Playing Cards use alignment inside each card.

> **Code conventions:** A code block followed by a **Source:** link is a repository example taken from that file; the excerpt may leave out unrelated markup, and the link opens the complete source. A block without a source link is a teaching example — either a generic syntax illustration or a shortened or adapted excerpt named in the surrounding prose. Section H contains new practice tasks, not requirements from the original freeCodeCamp exercises. The original HTML and CSS files are not modified by this course.

## B. Learning objectives

By the end of this chapter you should be able to:

- Turn a container into a flex container with `display: flex`.
- Identify the main axis and cross axis for each `flex-direction`.
- Use `justify-content`, `align-items`, `align-content`, and `gap`.
- Control wrapping with `flex-wrap`.
- Use `flex-grow`, `flex-shrink`, `flex-basis`, and the `flex` shorthand.
- Reorder items with `order` while understanding the accessibility trade-off.
- Align a single item with `align-self`.
- Recognise Flexbox patterns in the repository.

## C. Core concepts

### The flex container and its items

```css
.gallery {
  display: flex;
}
```

The element with `display: flex` is the flex container. Its direct children become flex items. The container controls their distribution.

### Main axis and cross axis

`flex-direction` sets the main axis:

```css
.row {
  flex-direction: row; /* main axis: left to right */
}

.column {
  flex-direction: column; /* main axis: top to bottom */
}
```

- `row` is the default: main axis horizontal, cross axis vertical.
- `column`: main axis vertical, cross axis horizontal.
- `row-reverse` and `column-reverse` reverse the direction.

`justify-content` works along the main axis. `align-items` works along the cross axis.

### justify-content

```css
.gallery {
  display: flex;
  justify-content: center;
}
```

Common values:

- `flex-start` — pack at the start.
- `flex-end` — pack at the end.
- `center` — centre the items.
- `space-between` — first item at the start, last at the end, equal gaps between.
- `space-around` — equal space around each item.
- `space-evenly` — equal space between items and at the edges.

### align-items and align-content

```css
.gallery {
  display: flex;
  align-items: center;
}
```

`align-items` aligns items on the cross axis of a single line. `align-content` distributes multiple wrapped lines:

```css
.flex-container {
  display: flex;
  flex-wrap: wrap;
  align-content: space-around;
}
```

`align-content` has no effect when there is only one line.

### Wrapping and gap

```css
.gallery {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
}
```

`flex-wrap: wrap` lets items move to a new line when they do not fit. `gap` adds space between items without adding margin to the outer edges.

The Photo Gallery uses `flex-wrap: wrap`, `gap: 16px`, and a max-width:

```css
.gallery {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  padding: 20px 10px;
  max-width: 1400px;
  margin: 0 auto;
  gap: 16px;
}
```

### The flex shorthand

```css
.box {
  flex: 0 0 150px;
}
```

The three values are:

1. `flex-grow: 0` — do not grow.
2. `flex-shrink: 0` — do not shrink.
3. `flex-basis: 150px` — start at 150px.

Compare:

```css
.pricing-card {
  flex: 0 0 200px;
}

.pro-plan {
  flex-grow: 2;
}
```

The pricing cards start at 200px. The Pro plan can grow twice as much as the others when there is extra space.

A simpler `flex: 1` means `flex-grow: 1`, `flex-shrink: 1`, `flex-basis: 0%`. The item takes an equal share of the available space.

### order

`order` changes visual order without changing the DOM:

```css
.box1 { order: 1; flex-grow: 1; }
.box2 { order: 2; flex-grow: 2; }
.box3 { order: 2; flex-shrink: 3; }
.box4 { order: 3; }
```

Items with the same order value keep their source order. Reordering can be visually useful, but it changes the reading order for keyboard and screen-reader users. Keep the DOM order meaningful.

### align-self

`align-self` overrides `align-items` for one item:

```css
.card {
  display: flex;
  justify-content: space-between;
}

.left {
  align-self: flex-start;
}

.middle {
  align-self: center;
}

.right {
  align-self: flex-end;
}
```

The Playing Cards use this to place the rank and suit in the corners and the large suit in the middle.

### A spacer with ::after

The Photo Gallery adds a generated element after the images:

```css
.gallery::after {
  content: "";
  width: 350px;
}
```

The spacer helps the final row balance when the images wrap. It is a layout trick, not content; the empty `content` keeps it out of the accessibility tree.

## D. Syntax

```css
.container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  align-content: space-between;
  gap: 1rem;
}

.item {
  flex: 1 1 200px;
  order: 2;
  align-self: flex-end;
}
```

## E. Code examples

### Example 1: A wrapping photo gallery

```css
.gallery {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  padding: 20px 10px;
  max-width: 1400px;
  margin: 0 auto;
  gap: 16px;
}

.gallery img {
  width: 100%;
  max-width: 350px;
  height: 300px;
  object-fit: cover;
  border-radius: 10px;
}

.gallery::after {
  content: "";
  width: 350px;
}
```

Source: [`CSS/Flexbox/Build a Flexbox Photo Gallery/style.css`](<../../CSS/Flexbox/Build a Flexbox Photo Gallery/style.css>). Status: **Implemented**.

`object-fit: cover` keeps each image's aspect ratio while filling the fixed 350×300 box. Without it, the images would be stretched.

### Example 2: Growth, shrinking, and order

```css
.flex-container {
  display: flex;
  flex-wrap: wrap;
  width: 70%;
  height: 600px;
  padding: 10px;
  margin: 20px auto;
  align-content: space-around;
}

.box {
  border: 1px solid #000;
  max-height: 120px;
  color: #000;
  display: flex;
  flex: 0 0 150px;
  flex-direction: column;
  align-items: center;
  margin: 10px;
  font-weight: bold;
  font-size: 1.125rem;
  border-radius: 5px;
  order: 0;
}

.box1 {
  background: #f16e79;
  order: 1;
  flex-grow: 1;
}

.box2 {
  background: #f1c40f;
  order: 2;
  flex-grow: 2;
}

.box3 {
  background: #ffd166;
  order: 2;
  flex-shrink: 3;
}
```

Source: [`CSS/Flexbox/Design a Set of Colorful Boxes/style.css`](<../../CSS/Flexbox/Design a Set of Colorful Boxes/style.css>). Status: **Implemented**.

The container has a fixed height and wraps its items, so `align-content` distributes the lines. The boxes also use `display: flex` internally to centre their text.

### Example 3: Pricing cards with a featured plan

```css
.pricing-container {
  display: flex;
  flex-wrap: wrap;
  border: 1px solid black;
  padding: 15px;
}

.pricing-card {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  flex: 0 0 200px;
  border: 2px solid black;
  padding: 15px;
  transform: scale(1);
  transition: transform 0.3s ease-in-out;
  margin: 10px;
}

.pro-plan {
  order: 1;
  flex-grow: 2;
}
```

Source: [`CSS/Flexbox/Design a Pricing Plans Layout Page/style.css`](<../../CSS/Flexbox/Design a Pricing Plans Layout Page/style.css>). Status: **Implemented**.

The cards are flex containers themselves. `flex-direction: column` and `justify-content: space-between` push the button to the bottom even when the feature lists have different lengths.

### Example 4: Alignment inside a card

```css
.card {
  display: flex;
  justify-content: space-between;
  border: 1px solid black;
  width: 200px;
  height: 250px;
  border-radius: 10px;
  box-shadow: 5px 2px 8px black;
}

.left {
  align-self: flex-start;
}

.middle {
  display: flex;
  flex-direction: column;
  align-self: center;
  justify-content: center;
}

.right {
  display: flex;
  justify-content: end;
  align-self: flex-end;
  flex-direction: column-reverse;
}
```

Source: [`CSS/Flexbox/Build a Page of Playing Cards, Not started [Certification Project]/style.css`](<../../CSS/Flexbox/Build a Page of Playing Cards, Not started [Certification Project]/style.css>). Status: **Implemented**.

The folder name says "Not started", but the HTML and stylesheet contain a complete visual card layout. The status label follows the source, not the folder name.

### Example 5: Centring a page column

```css
body {
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
```

Source: [`CSS/Variables/Build an Availability Table/styles.css`](<../../CSS/Variables/Build an Availability Table/styles.css>). Status: **Implemented**.

This is the shortest way to centre a single column of content in the viewport. It also demonstrates the difference between the main axis (`justify-content`) and the cross axis (`align-items`).

## F. Step-by-step explanation

1. **Decide whether the layout is one-dimensional.** If items are arranged in a row or a column, Flexbox is a good fit.
2. **Set `display: flex` on the container.** The direct children become items.
3. **Choose the direction.** Use `row` for horizontal, `column` for vertical.
4. **Allow wrapping if needed.** Add `flex-wrap: wrap` for card rows and galleries.
5. **Align along the main axis.** Use `justify-content`.
6. **Align along the cross axis.** Use `align-items` or `align-self`.
7. **Add `gap`.** It is cleaner than margins on every item.
8. **Set flex sizing.** Use `flex: 1` for equal sharing or `flex: 0 0 200px` for a fixed basis.
9. **Check the DOM order.** If you use `order`, make sure the visual order still makes sense for keyboard users.
10. **Test with long content.** Flex items can shrink below their content width unless you set a minimum.
11. **Test at 320px.** A row with fixed-basis items may overflow unless it wraps.

## G. Repository implementations

| Implementation | Flexbox feature | Status | Source |
| --- | --- | --- | --- |
| Flexbox Photo Gallery | Wrap, centre, gap, `object-fit`, spacer | Implemented | [Open](<../../CSS/Flexbox/Build a Flexbox Photo Gallery/index.html>) |
| Colorful Boxes | `order`, `flex-grow`, `flex-shrink`, `align-content` | Implemented | [Open](<../../CSS/Flexbox/Design a Set of Colorful Boxes/index.html>) |
| Pricing Plans | Wrapping cards, column flex, `space-between`, growth | Implemented | [Open](<../../CSS/Flexbox/Design a Pricing Plans Layout Page/index.html>) |
| Playing Cards | Nested flex containers, `align-self`, `flex-direction` | Implemented | [Open](<../../CSS/Flexbox/Build a Page of Playing Cards, Not started [Certification Project]/index.html>) |
| Availability Table | Page-level centring with a column flex container | Implemented | [Open](<../../CSS/Variables/Build an Availability Table/index.html>) |
| Product Landing Page | Header and feature rows using flex | Implemented\* | [Open](<../../CSS/CERTIFICATION PROJECTS/Build a Product Landing Page/index.html>) |

## H. Additional challenges

These are new practice tasks for this course; they are not requirements from the original exercises.

1. Build a navigation bar with a logo on the left and three links on the right. Use `justify-content: space-between`.
2. Create a card row with `flex-wrap: wrap` and `gap`. Test it at 320px, 768px, and 1440px.
3. Recreate the pricing cards with `flex: 1 1 200px` instead of `flex: 0 0 200px`. Compare the behaviour.
4. Build a vertical card with a header, body, and footer. Push the footer to the bottom with `margin-top: auto`.
5. Reorder three boxes with `order`. Then navigate the page with Tab and decide whether the visual order still makes sense.
6. Replace the Photo Gallery's `::after` spacer with a different technique, such as `justify-content: flex-start` plus auto margins.
7. Build a playing card with four corners using nested flex containers and `align-self`.
8. Take a float-based layout and convert it to Flexbox. List the properties that became unnecessary.

## I. Common mistakes

- **Putting `display: flex` on the wrong element.** The container is the parent, not the item.
- **Expecting `justify-content` to align vertically in a row.** It works on the main axis; use `align-items` for the cross axis.
- **Forgetting `flex-wrap`.** Items shrink or overflow instead of moving to a new line.
- **Using `flex: 1` when you mean a fixed basis.** The shorthand resets several properties.
- **Forgetting that flex items can shrink below their content width.** Set `min-width: 0` or a suitable `flex-shrink` when needed.
- **Using `order` to change reading order.** It only changes visual order.
- **Adding margins to every item instead of `gap`.** The outer spacing becomes uneven.
- **Expecting `align-content` to work on one line.** It only distributes wrapped lines.
- **Nesting flex containers without a reason.** Each layer adds complexity.
- **Testing only with short content.** Longer labels expose shrinking and wrapping problems.

## J. Summary

Flexbox arranges items along a main axis and aligns them on a cross axis. `display: flex` creates the container; `flex-direction` chooses the axis; `justify-content` and `align-items` handle alignment; `gap` handles spacing; `flex-grow`, `flex-shrink`, `flex-basis`, and `order` control sizing and sequence.

The Photo Gallery shows wrapping and `object-fit`. The Colorful Boxes show growth and order. The Pricing Plans show cards that stretch while keeping their buttons aligned. The Playing Cards show nested flex containers. Flexbox is powerful precisely because it is one-dimensional; for two-dimensional layouts, the next chapter uses Grid.

## K. Next module

Continue to [07. CSS Grid](07-css-grid.md) to build two-dimensional layouts with tracks, areas, and explicit placement.
