# 08. Responsive Design

## A. Introduction

A responsive page adapts to the space it is given. That space might be a phone, a tablet, a laptop, a large monitor, or a narrow browser window on a desktop. Responsive design is not a single property or a list of device widths; it is a way of building with fluid sizes, sensible maximums, and content-driven breakpoints.

The repository contains several responsive practice pages and two pages that are missing the viewport metadata entirely. It also contains layouts with no media query at all. That mix makes it a useful place to compare intention with result.

> **Code conventions:** A code block followed by a **Source:** link is a repository example taken from that file; the excerpt may leave out unrelated markup, and the link opens the complete source. A block without a source link is a teaching example — either a generic syntax illustration or a shortened or adapted excerpt named in the surrounding prose. Section H contains new practice tasks, not requirements from the original freeCodeCamp exercises. The original HTML and CSS files are not modified by this course.

## B. Learning objectives

By the end of this chapter you should be able to:

- Add the viewport meta tag and explain what it does.
- Use fluid widths, `max-width`, and `min()`/`max()`/`clamp()`.
- Write media queries with `min-width` and `max-width`.
- Choose breakpoints based on content rather than device names.
- Reflow a multi-column layout into a single column.
- Make images and embedded media scale without distortion.
- Respect reduced-motion preferences.
- Identify pages in the repository that are not responsive.

## C. Core concepts

### The viewport meta tag

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

`width=device-width` makes the layout viewport match the device width. `initial-scale=1.0` starts at 100% zoom. Without this tag, a phone may render the page as a wide desktop layout and shrink it to fit.

The audit found 57 of 59 pages with viewport metadata. The two missing pages are:

- [Cat Painting](<../../CSS/Positioning/Build a Cat Painting/index.html>)
- [Nutritional Label](<../../CSS/Typography/Build a Nutritional Label/index.html>)

Both pages are otherwise complete CSS exercises. They are labelled **Implemented\*** because of the missing metadata.

### Fluid widths and maximums

```css
.newspaper {
  max-width: 800px;
  margin: 50px auto;
}

img {
  max-width: 100%;
  height: auto;
}
```

A fluid element shrinks with its container but stops growing at `max-width`. This is often enough for simple pages and requires no media query.

### Relative units and functions

```css
h1 {
  font-size: min(5vw, 1.2em);
}

#logo {
  width: max(10rem, 18vw);
  aspect-ratio: 35 / 4;
}
```

- `min()` chooses the smaller value.
- `max()` chooses the larger value.
- `clamp(min, preferred, max)` keeps a value between two limits.

The Quiz stylesheet uses `min()` and `max()` to keep the heading and logo from becoming too small or too large.

### Media queries

```css
@media (max-width: 768px) {
  #piano {
    width: 358px;
  }
}

@media (min-width: 769px) and (max-width: 1199px) {
  #piano {
    width: 675px;
  }
}
```

A media query applies rules only when the condition is true. The Piano uses two ranges: small screens and medium screens. The base styles handle the large layout.

`min-width` queries are often used for a mobile-first approach: write the small-screen styles first, then add enhancements as the screen grows. `max-width` queries start from the desktop layout and scale down. Both can work; consistency matters more than the choice.

### Content-driven breakpoints

Do not choose `768px` because a popular device uses it. Resize the browser until the content stops looking right, then add a breakpoint there. The repository's breakpoints vary:

- Piano: `768px`, and `769px`–`1199px`.
- Product Landing: `720px`, `650px`, `550px`.
- Technical Documentation: `1024px`, `640px`.
- Magazine: `720px`, `600px`, `550px`, `420px`.

These reflect the content of each page, not a single global device list.

### Reflowing a layout

A common responsive change is to stack columns:

```css
@media (max-width: 700px) {
  .layout {
    grid-template-columns: 1fr;
  }
}
```

The Product Landing header switches from a row to a column:

```css
@media only screen and (max-width: 720px) {
  #header {
    flex-direction: column;
    gap: 2rem;
  }
}
```

The Technical Documentation page switches its two-column body to a stacked header and main region at 1024px.

### Responsive media

```css
img {
  max-width: 100%;
  height: auto;
}

iframe {
  max-width: 100%;
}
```

The Product Landing page also resizes its iframe at the 720px breakpoint:

```css
iframe {
  width: 100%;
  height: 300px;
}
```

Fixed `width` and `height` attributes on an iframe are a starting point, not a responsive solution. CSS must allow the frame to shrink.

`object-fit: cover` is useful when an image must fill a fixed box without distortion. The Photo Gallery uses it:

```css
.gallery img {
  width: 100%;
  max-width: 350px;
  height: 300px;
  object-fit: cover;
}
```

### Reduced motion

```css
@media (prefers-reduced-motion: no-preference) {
  * {
    scroll-behavior: smooth;
  }
}
```

This Quiz rule enables smooth scrolling only when the user has not asked for reduced motion. For larger animations, provide a `prefers-reduced-motion: reduce` rule that shortens or disables them.

### Pages without responsive rules

The Newspaper Layout has a three-column grid and no media query. It will not reflow into a single column on a phone. The standalone portfolio has no media query either, but its `auto-fit` card grids reflow because the tracks are defined with `minmax()`.

The absence of a media query is not automatically a bug. A layout can be responsive through fluid sizing alone. It becomes a limitation when the content cannot fit at a narrow width.

## D. Syntax

Viewport metadata:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

Fluid content:

```css
img {
  max-width: 100%;
  height: auto;
}
```

Media query:

```css
@media (max-width: 600px) {
  .sidebar {
    display: none;
  }
}
```

Range query:

```css
@media (min-width: 600px) and (max-width: 900px) {
  .card {
    flex-basis: 45%;
  }
}
```

Clamped type:

```css
h1 {
  font-size: clamp(1.75rem, 4vw, 3rem);
}
```

## E. Code examples

### Example 1: Piano breakpoints

```css
@media (max-width: 768px) {
  #piano {
    width: 358px;
  }

  .keys {
    width: 318px;
  }

  .logo {
    width: 150px;
  }
}

@media (max-width: 1199px) and (min-width: 769px) {
  #piano {
    width: 675px;
  }

  .keys {
    width: 633px;
  }
}
```

Source: [`CSS/Responsive Design/Design a Piano/style.css`](<../../CSS/Responsive%20Design/Design%20a%20Piano/style.css>). Status: **Implemented**.

The base piano is 992px wide. The medium query reduces it to 675px, and the small query reduces it to 358px. The keys and logo are resized together so the visual proportions stay consistent.

### Example 2: Product Landing breakpoints

```css
@media only screen and (max-width: 720px) {
  #header {
    flex-direction: column;
    gap: 2rem;
  }

  label {
    font-size: 2.8rem;
  }

  #email {
    font-size: 1.7rem;
  }

  iframe {
    width: 100%;
    height: 300px;
  }
}
```

Source: [`CSS/CERTIFICATION PROJECTS/Build a Product Landing Page/style.css`](<../../CSS/CERTIFICATION%20PROJECTS/Build%20a%20Product%20Landing%20Page/style.css>). Status: **Implemented\***.

The page uses three breakpoints (720px, 650px, 550px) to reduce large text and stack the header. The `only screen` keyword is optional for screen media, but it is valid.

### Example 3: A stacked documentation layout

```css
@media (max-width: 1024px) {
  body {
    display: flex;
    flex-direction: column;
  }

  header {
    width: 100%;
    height: auto;
  }

  #main-doc {
    width: 100%;
    height: auto;
    overflow: scroll;
    border: none;
  }
}

@media (max-width: 640px) {
  #main-doc .code {
    font-size: 0.7rem;
    margin: 0;
    padding: 10px 5px;
    font-size: 0.625rem;
    margin-bottom: 20px;
  }
}
```

Source: [`CSS/CERTIFICATION PROJECTS/Build a Technical Documentation Page/style.css`](<../../CSS/CERTIFICATION%20PROJECTS/Build%20a%20Technical%20Documentation%20Page/style.css>). Status: **Implemented**.

The base layout is a fixed-width two-column page. At 1024px it becomes a column, and at 640px the code blocks get smaller. The duplicate `font-size` in the 640px rule is harmless because the later value wins.

### Example 4: Fluid type and logo sizing

```css
#logo {
  width: max(10rem, 18vw);
  background-color: #0a0a23;
  aspect-ratio: 35 / 4;
  padding: 0.4rem;
}

h1 {
  color: #f1be32;
  font-size: min(5vw, 1.2em);
  text-align: center;
}
```

Source: [`CSS/Accessibility/Build a Quiz Webpage, Not started W/style.css`](<../../CSS/Accessibility/Build%20a%20Quiz%20Webpage,%20Not%20started%20W/style.css>). Status: **Link issue**.

The CSS is responsive, but the HTML requests `styles.css` while the file is `style.css`, so none of these rules load. The source is a useful example; the page itself appears unstyled until the filename is corrected.

### Example 5: A grid that reflows without a media query

```css
.card-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 30px;
}
```

Source: [`Personal Portfolio/style.css`](<../../Personal%20Portfolio/style.css>). Status: **Implemented**.

At a narrow width, the `minmax(280px, 1fr)` track can no longer fit more than one column, so the cards stack. No breakpoint is required because the track definition itself responds to available space.

## F. Step-by-step explanation

1. **Add the viewport meta tag.** Do this before testing on a phone.
2. **Build the mobile layout first or the desktop layout first.** Pick one direction and stay consistent.
3. **Use fluid widths.** Prefer percentages, `fr`, and `max-width` over fixed pixels.
4. **Set images to `max-width: 100%`.** Add `height: auto` to preserve the aspect ratio.
5. **Resize the browser slowly.** Note the widths where the content breaks.
6. **Add a breakpoint at each break.** Change the layout, not just the font size.
7. **Stack columns on small screens.** Reflow the content rather than hiding it.
8. **Test long labels and long words.** They often cause overflow before images do.
9. **Test at 320px, 768px, and a wide desktop.** Use the browser's device toolbar for a quick check.
10. **Respect reduced motion.** Add a reduced-motion rule for animations.
11. **Check the viewport metadata on every page.** The repository has two pages missing it.
12. **Test with zoom.** A responsive layout should still work at 200% zoom.

## G. Repository implementations

| Implementation | Responsive feature | Status | Source |
| --- | --- | --- | --- |
| Piano | Two media-query ranges with proportional resizing | Implemented | [Open](<../../CSS/Responsive Design/Design a Piano/index.html>) |
| Product Landing Page | Three breakpoints, stacked header, fluid iframe | Implemented\* | [Open](<../../CSS/CERTIFICATION PROJECTS/Build a Product Landing Page/index.html>) |
| Technical Documentation | 1024px and 640px layout changes | Implemented | [Open](<../../CSS/CERTIFICATION PROJECTS/Build a Technical Documentation Page/index.html>) |
| Magazine | Four breakpoints and a fluid image grid | Implemented | [Open](<../../CSS/Grid/Build a Magazine/index.html>) |
| Quiz Webpage | `min()`, `max()`, `aspect-ratio`, reduced motion | Link issue | [Open](<../../CSS/Accessibility/Build a Quiz Webpage, Not started W/index.html>) |
| Personal Portfolio | Responsive `auto-fit` grids without media queries | Implemented | [Open](<../../Personal Portfolio/index.html>) |
| Newspaper Layout | Fixed three-column grid with no mobile rule | Implemented | [Open](<../../CSS/Grid/Design a Newspaper Layout/index.html>) |
| Cat Painting | No viewport metadata | Implemented\* | [Open](<../../CSS/Positioning/Build a Cat Painting/index.html>) |
| Nutritional Label | No viewport metadata | Implemented\* | [Open](<../../CSS/Typography/Build a Nutritional Label/index.html>) |

## H. Additional challenges

These are new practice tasks for this course; they are not requirements from the original exercises.

1. Add a mobile breakpoint to the Newspaper Layout that stacks every area into one column.
2. Add the viewport meta tag to the Cat Painting and Nutritional Label, then test both on a narrow viewport.
3. Replace one fixed font size in the Product Landing page with `clamp()` and compare the result at three widths.
4. Build a responsive two-column article that becomes one column below 700px.
5. Make a video or iframe scale to its container with a wrapper and `aspect-ratio`.
6. Add a `prefers-reduced-motion: reduce` rule to the Ferris Wheel page that stops the animations.
7. Test the portfolio at 320px. Record how many card columns appear and whether any text overflows.
8. Find a page that uses a fixed width and convert it to a fluid `max-width` layout.
9. Use the browser's device toolbar to test one page at 320px, 768px, and 1440px. List every element that breaks.

## I. Common mistakes

- **Forgetting the viewport meta tag.** Mobile browsers may zoom out the desktop layout.
- **Using `user-scalable=no`.** This blocks zoom and harms accessibility.
- **Choosing breakpoints from device names.** Use the content's breaking points.
- **Hiding content instead of reflowing it.** Hiding an important section is not responsive design.
- **Fixed widths everywhere.** The page cannot adapt to a narrow screen.
- **Fixed-height text containers.** Text can overflow when it wraps.
- **Images without `max-width: 100%`.** Large images cause horizontal scrolling.
- **Forgetting `height: auto`.** Changing only the width can distort images.
- **Testing only in the device toolbar.** Also resize the real browser window and test with zoom.
- **Animating without a reduced-motion path.** Motion can cause discomfort.
- **Assuming a media query is always necessary.** Fluid grids and `auto-fit` can handle many layouts on their own.

## J. Summary

Responsive design combines the viewport meta tag, fluid widths, relative units, flexible images, and content-driven media queries. `max-width` keeps content readable on large screens, while `minmax()` and `auto-fit` let grids reflow without breakpoints. Media queries handle the points where the content needs a structural change.

The Piano, Product Landing, Technical Documentation, and Magazine pages show different breakpoint strategies. The portfolio shows fluid grids without media queries. The Newspaper Layout shows a fixed grid that needs a mobile rule. The Cat Painting and Nutritional Label show why viewport metadata belongs in every page.

## K. Next module

Continue to [09. CSS Custom Properties](09-css-custom-properties.md) to replace repeated values with named, scoped variables that can change at runtime.
