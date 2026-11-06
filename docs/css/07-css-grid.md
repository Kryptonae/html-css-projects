# 07. CSS Grid

## A. Introduction

CSS Grid is a two-dimensional layout system. You define columns and rows, then place items into the resulting cells. It is the right tool for page layouts, card grids, magazines, dashboards, and any design where alignment must hold in both directions.

The repository uses Grid in three distinct ways: the Magazine builds a page with named tracks and nested media grids, the Newspaper Layout uses `grid-template-areas`, and the standalone portfolio uses `auto-fit` with `minmax()` for responsive card rows.

> **Code conventions:** A code block followed by a **Source:** link is a repository example taken from that file; the excerpt may leave out unrelated markup, and the link opens the complete source. A block without a source link is a teaching example — either a generic syntax illustration or a shortened or adapted excerpt named in the surrounding prose. Section H contains new practice tasks, not requirements from the original freeCodeCamp exercises. The original HTML and CSS files are not modified by this course.

## B. Learning objectives

By the end of this chapter you should be able to:

- Create a grid with `display: grid`.
- Define columns and rows with `grid-template-columns`, `grid-template-rows`, `repeat()`, and `fr`.
- Use `minmax()` and `auto-fit` for responsive card grids.
- Place items with `grid-column`, `grid-row`, and line numbers.
- Build a layout with `grid-template-areas` and `grid-area`.
- Use `gap`, `place-items`, and nested grids.
- Explain when Grid is a better choice than Flexbox.
- Identify the responsive limits of a fixed grid.

## C. Core concepts

### The grid container

```css
main {
  display: grid;
}
```

The direct children become grid items. The container defines the tracks.

### Columns, rows, and fr

```css
main {
  display: grid;
  grid-template-columns: 200px 1fr 200px;
  grid-template-rows: auto 1fr auto;
}
```

- `200px` is a fixed track.
- `1fr` takes one share of the remaining space.
- `auto` sizes to the content or the available space.

The `fr` unit is flexible. `2fr` takes twice the share of `1fr`.

`repeat()` avoids repetition:

```css
.grid {
  grid-template-columns: repeat(3, 1fr);
}
```

### minmax and auto-fit

```css
.card-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 30px;
}
```

This creates as many columns as fit, each at least 280px wide and at most one equal share of the remaining space. It is one of the most useful responsive patterns in CSS.

`auto-fill` also creates as many tracks as fit, but it keeps empty tracks. `auto-fit` collapses empty tracks, letting the existing items grow. The portfolio uses `auto-fit`.

### Gap

```css
.grid {
  gap: 20px;
  column-gap: 3rem;
  row-gap: 1.5rem;
}
```

`gap` is the shorthand for row and column gaps. It replaces margin hacks between grid items.

### Placing items by line

```css
.heading {
  grid-column: 2 / 3;
}

.hero {
  grid-column: 1 / -1;
}
```

Grid lines are numbered from 1. `1 / -1` spans from the first line to the last line. This is how the Magazine makes its hero span the full width and keeps the main content in the middle column.

### Named areas

The Newspaper Layout uses named areas:

```css
.newspaper-layout {
  display: grid;
  grid-template-areas:
    "title title title"
    "feature-article feature-article cover-image"
    "secondary-article secondary-article cover-image"
    "small-article1 small-article2 small-article3";
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: auto repeat(3, 1fr);
  gap: 10px;
}

.title {
  grid-area: title;
}

.feature-article {
  grid-area: feature-article;
}
```

Each string is a row. Each word is a cell. The area name must match the `grid-area` value on the child. This is the easiest way to understand a complex page layout because the CSS looks like a diagram.

### Nested grids

A grid item can also be a grid container:

```css
.heading {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  row-gap: 1.5rem;
}
```

The Magazine nests a heading grid inside the main page grid. Nested grids are normal; each one has its own tracks and items.

### Grid versus Flexbox

Use Grid when you need alignment in two dimensions or when the layout has a clear row/column structure. Use Flexbox when you need a single row or column that distributes space or wraps naturally.

They work well together. The Magazine uses Grid for the page and Flexbox for some internal alignment. The portfolio uses Grid for card collections and Flexbox for navigation.

### A fixed grid is not automatically responsive

The Newspaper Layout defines three columns and four rows, but it has no media query. On a narrow screen, the grid still tries to fit three columns, so the content becomes cramped or overflows. Adding a small-screen rule would fix it:

```css
@media (max-width: 700px) {
  .newspaper-layout {
    grid-template-areas:
      "title"
      "feature-article"
      "secondary-article"
      "cover-image"
      "small-article1"
      "small-article2"
      "small-article3";
    grid-template-columns: 1fr;
  }
}
```

That is a new improvement suggestion, not a change to the repository file.

## D. Syntax

```css
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: auto 1fr auto;
  gap: 1rem;
}

.item {
  grid-column: 1 / 3;
  grid-row: 2 / 4;
}
```

Named areas:

```css
.layout {
  display: grid;
  grid-template-areas:
    "header header"
    "sidebar main"
    "footer footer";
  grid-template-columns: 200px 1fr;
}

.header { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main { grid-area: main; }
.footer { grid-area: footer; }
```

Responsive cards:

```css
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
}
```

## E. Code examples

### Example 1: The Magazine page grid

```css
main {
  display: grid;
  grid-template-columns: minmax(2rem, 1fr) minmax(min-content, 94rem) minmax(
      2rem,
      1fr
    );
  row-gap: 3rem;
}

.heading {
  grid-column: 2 / 3;
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  row-gap: 1.5rem;
}

.hero {
  grid-column: 1 / -1;
  position: relative;
}

.text {
  grid-column: 2 / 3;
  font-size: 1.8rem;
  column-width: 25rem;
  text-align: justify;
}
```

Source: [`CSS/Grid/Build a Magazine/style.css`](<../../CSS/Grid/Build a Magazine/style.css>). Status: **Implemented**.

The page has three columns: a flexible gutter, a content column up to 94rem, and another flexible gutter. The heading and text sit in the middle column, while the hero spans all three. `column-width` inside `.text` is a multi-column layout property, not a grid property; it lets the article text flow into columns.

### Example 2: Named areas in a newspaper

```css
.newspaper-layout {
  display: grid;
  grid-template-areas:
    "title title title"
    "feature-article feature-article cover-image"
    "secondary-article secondary-article cover-image"
    "small-article1 small-article2 small-article3";
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: auto repeat(3, 1fr);
  gap: 10px;
}

.title { grid-area: title; }
.feature-article { grid-area: feature-article; }
.secondary-article { grid-area: secondary-article; }
.cover-image { grid-area: cover-image; }
.small-article1 { grid-area: small-article1; }
.small-article2 { grid-area: small-article2; }
.small-article3 { grid-area: small-article3; }
```

Source: [`CSS/Grid/Design a Newspaper Layout/styles.css`](<../../CSS/Grid/Design a Newspaper Layout/styles.css>). Status: **Implemented**.

The layout has no media query, so it does not reflow on a phone. The file is still a clear example of named areas and visual hierarchy.

### Example 3: Responsive card grid

```css
.card-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 30px;
}

.small-card-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(230px, 1fr));
  gap: 20px;
}
```

Source: [`Personal Portfolio/style.css`](<../../Personal%20Portfolio/style.css>). Status: **Implemented**.

The portfolio is tracked directly in the main repository. It uses Grid for the card collections and Flexbox for navigation and other one-dimensional rows. It has no media query, but the `auto-fit` grid still reflows because the tracks are responsive by design.

### Example 4: Image gallery grid

```css
.image-wrapper {
  display: grid;
  grid-template-columns: 2fr 1fr;
  grid-template-rows: repeat(3, min-content);
  gap: 2rem;
  place-items: center;
}

.image-1,
.image-3 {
  grid-column: 1 / -1;
}
```

Source: [`CSS/Grid/Build a Magazine/style.css`](<../../CSS/Grid/Build a Magazine/style.css>). Status: **Implemented**.

The first and third images span both columns, while the second image occupies the smaller column. `place-items: center` centres each item in its cell.

## F. Step-by-step explanation

1. **Decide whether the layout is two-dimensional.** If it needs aligned rows and columns, Grid is a good fit.
2. **Sketch the tracks.** Count the columns and rows before writing code.
3. **Use `fr` for flexible space and `minmax()` for limits.**
4. **Add `gap`.** Avoid margins between grid items.
5. **Place the major regions first.** Header, main, sidebar, footer.
6. **Use named areas for complex pages.** The CSS becomes a readable diagram.
7. **Nest grids only when a region needs its own alignment.** Do not create a grid for every div.
8. **Add responsive rules.** A fixed number of columns usually needs a breakpoint.
9. **Test with long content.** A grid cell can overflow if its content cannot shrink.
10. **Check the DOM order.** Grid placement can change visual order; keep the source order meaningful.

## G. Repository implementations

| Implementation | Grid feature | Status | Source |
| --- | --- | --- | --- |
| Magazine | Page grid, `minmax()`, line placement, nested grids, overlay | Implemented | [Open](<../../CSS/Grid/Build a Magazine/index.html>) |
| Newspaper Layout | `grid-template-areas`, named regions, fixed three-column layout | Implemented | [Open](<../../CSS/Grid/Design a Newspaper Layout/index.html>) |
| Personal Portfolio | `auto-fit`, `minmax()`, two card grids | Implemented | [Open](<../../Personal Portfolio/index.html>) |
| Product Landing Page | Page regions via `grid-template-areas` | Implemented\* | [Open](<../../CSS/CERTIFICATION PROJECTS/Build a Product Landing Page/index.html>) |
| Availability Table | Grid-free table layout with CSS variables | Implemented | [Open](<../../CSS/Variables/Build an Availability Table/index.html>) |

## H. Additional challenges

These are new practice tasks for this course; they are not requirements from the original exercises.

1. Build a three-column page with a full-width header and footer. Use `grid-template-areas`.
2. Create a card grid with `repeat(auto-fit, minmax(220px, 1fr))` and test it at three widths.
3. Add a small-screen media query to the Newspaper Layout that stacks the areas into one column.
4. Recreate the Magazine's middle-column layout with named areas instead of line numbers.
5. Build a photo mosaic where the first image spans two columns and two rows.
6. Compare a card row built with Flexbox and the same row built with Grid. Which is easier to align? Why?
7. Use `place-items` and `place-self` to centre one item differently from its siblings.
8. Inspect the portfolio's card grid at 320px. How many columns appear, and why?

## I. Common mistakes

- **Using Grid for a simple row.** Flexbox may be simpler.
- **Forgetting `display: grid`.** The track properties have no effect on a non-grid container.
- **Mismatched area names.** A `grid-area` value must match a name in `grid-template-areas`.
- **Leaving empty cells unintentionally.** Grid auto-placement fills the next available cell.
- **Assuming `auto-fit` and `auto-fill` are identical.** They differ when there are empty tracks.
- **Using fixed columns with no breakpoint.** The layout overflows on small screens.
- **Putting margins on grid items instead of using `gap`.** Spacing becomes uneven.
- **Nesting too many grids.** Each layer makes the layout harder to reason about.
- **Changing visual order without checking keyboard order.** Grid placement can diverge from the DOM.
- **Forgetting `min-width: 0` on a grid item with long content.** The item may refuse to shrink.

## J. Summary

Grid defines rows and columns and places items into the resulting cells. `fr` distributes free space, `minmax()` sets limits, `repeat()` keeps track definitions short, and `grid-template-areas` makes complex layouts readable. `auto-fit` with `minmax()` is a compact responsive card pattern.

The Magazine shows a page grid with a full-width hero and a nested heading grid. The Newspaper Layout shows named areas but lacks a mobile breakpoint. The portfolio shows how a card grid can reflow without media queries. Grid and Flexbox are complementary; the next chapter focuses on making either layout adapt to the viewport.

## K. Next module

Continue to [08. Responsive Design](08-responsive-design.md) to combine fluid units, media queries, and flexible layouts into pages that work on small and large screens.
