# 03. Colours and Typography

## A. Introduction

Colour and type do most of the visual work on a page. CSS gives you several ways to write a colour, several ways to build a gradient, and a font system that can fall back gracefully when a font is unavailable. It also gives you relative units that let text scale with the user's settings.

This chapter uses the coloured markers and boxes for colour formats, the newspaper article for type hierarchy, and the nutritional label for compact information design. It also looks at an invalid `font` shorthand in the Technical Documentation page.

> **Code conventions:** A code block followed by a **Source:** link is a repository example taken from that file; the excerpt may leave out unrelated markup, and the link opens the complete source. A block without a source link is a teaching example — either a generic syntax illustration or a shortened or adapted excerpt named in the surrounding prose. Section H contains new practice tasks, not requirements from the original freeCodeCamp exercises. The original HTML and CSS files are not modified by this course.

## B. Learning objectives

By the end of this chapter you should be able to:

- Write colours with named values, hexadecimal, `rgb()`/`rgba()`, and `hsl()`/`hsla()`.
- Build linear and radial gradients.
- Choose a readable font stack with generic fallbacks.
- Control font size, weight, line height, letter spacing, alignment, and transformation.
- Use `rem`, `em`, percentages, and viewport units appropriately.
- Notice and fix an invalid `font` shorthand.
- Evaluate colour contrast and typographic hierarchy.

## C. Core concepts

### Colour formats

Named colours are convenient:

```css
body {
  background-color: whitesmoke;
  color: black;
}
```

Hexadecimal colours use a `#` followed by three, four, six, or eight digits:

```css
.color1 {
  background-color: #33ff57;
}
```

`rgb()` uses red, green, and blue channels from 0 to 255. `rgba()` adds an alpha channel from 0 to 1:

```css
.container {
  background-color: rgb(255, 255, 255);
}

.sleeve {
  background-color: rgba(255, 255, 255, 0.5);
}
```

`hsl()` uses hue, saturation, and lightness. `hsla()` adds alpha:

```css
.blue {
  background: linear-gradient(
    hsl(186, 76%, 16%),
    hsl(223, 90%, 60%),
    hsl(240, 56%, 42%)
  );
}
```

The Colored Markers project deliberately uses all three families: RGB for the red marker, hex for the green marker, and HSL for the blue marker.

### Gradients

A linear gradient blends colours along a line:

```css
.red {
  background: linear-gradient(
    rgb(122, 74, 14),
    rgb(245, 62, 113),
    rgb(162, 27, 27)
  );
}
```

A radial gradient blends from a centre point outward:

```css
.sky {
  background: radial-gradient(
    circle closest-corner at 15% 15%,
    #ffcf33,
    #ffcf33 20%,
    #ffff66 21%,
    #bbeeff 100%
  );
}
```

Gradients are images, so they use `background` or `background-image`, not `background-color`.

### Font stacks

A font stack lists the preferred font first and fallbacks after it:

```css
body {
  font-family: Arial, Helvetica, sans-serif;
}
```

If Arial is unavailable, the browser tries Helvetica, then any available sans-serif font. The generic family at the end is important.

The Newspaper Article uses a serif stack for the newspaper name and a sans-serif stack for the body:

```css
.newspaper {
  font-size: 16px;
  font-family: "Open Sans", sans-serif;
}

.name {
  font-size: 2rem;
  font-family: "Times New Roman", serif;
}
```

The quoted family name is needed when the name contains a space.

### Type scale and units

`px` is an absolute CSS unit. `rem` is relative to the root font size. `em` is relative to the current element's font size. Percentages are often relative to the parent.

```css
html {
  font-size: 24px;
}

.newspaper {
  font-size: 16px;
}

.name {
  font-size: 2rem; /* 2 × 24px = 48px */
}
```

Because the root size is 24px, `2rem` is 48px. If the user changes their default font size, the root-relative value can scale with it.

The Nutritional Label uses `rem` for small text and `em` for indentation:

```css
.small-text {
  font-size: 0.85rem;
}

.indent {
  margin-left: 1em;
}

.double-indent {
  margin-left: 2em;
}
```

`1em` here is relative to the element's own font size, so indentation scales with the label's typography.

### Line height, spacing, and case

```css
.text {
  text-indent: 20px;
  line-height: 2em;
  margin: 15px 0;
}

.name,
.author {
  text-transform: uppercase;
}

.header h1 {
  letter-spacing: 0.15px;
}
```

- `line-height` controls the space between lines.
- `text-indent` indents the first line of a block.
- `text-transform` changes case visually without changing the HTML.
- `letter-spacing` adds or removes space between characters.

A `line-height` value without a unit, such as `1.5`, is relative to the element's font size and is usually more flexible than a fixed pixel value.

### Font shorthand

The `font` shorthand combines several font properties:

```css
font: italic bold 16px/1.5 Arial, sans-serif;
```

A valid shorthand must include a font size and a font family. This declaration is invalid:

```css
font: 1.2rem;
```

The Technical Documentation page contains exactly that line in its `.code` rule. The browser drops the declaration, so the code block inherits the surrounding font instead of receiving a 1.2rem size. The fix would be:

```css
font: 1.2rem sans-serif;
```

or, more safely, separate declarations:

```css
font-size: 1.2rem;
font-family: monospace;
```

### Contrast and readability

Colour is not only decoration. Text needs enough contrast against its background. The repository's dark pages use light text on dark backgrounds, while the newspaper uses dark text on a light background. When changing colours, test contrast rather than judging by appearance alone.

Avoid using colour as the only signal. The Job Application Form uses green, red, and gold borders to indicate valid, invalid, and focused fields, but a colour-blind user may not distinguish them. The border change is helpful, but text feedback or an icon would make the state clearer.

## D. Syntax

```css
/* Named colour */
color: brown;

/* Hex */
color: #333333;

/* RGB and alpha */
background-color: rgba(255, 255, 255, 0.5);

/* HSL */
color: hsl(240, 56%, 42%);

/* Linear gradient */
background: linear-gradient(#55680d, #71f53e, #116c31);

/* Font stack */
font-family: "Open Sans", Arial, sans-serif;

/* Type properties */
font-size: 1.5rem;
font-weight: 700;
line-height: 1.6;
letter-spacing: 0.5px;
text-align: center;
text-transform: uppercase;

/* Valid shorthand */
font: italic 700 1rem/1.5 Arial, sans-serif;
```

## E. Code examples

### Example 1: Three colour formats

```css
.red {
  background: linear-gradient(
    rgb(122, 74, 14),
    rgb(245, 62, 113),
    rgb(162, 27, 27)
  );
  box-shadow: 0 0 20px 0 rgba(83, 14, 14, 0.8);
}

.green {
  background: linear-gradient(#55680d, #71f53e, #116c31);
  box-shadow: 0 0 20px 0 #3b7e20cc;
}

.blue {
  background: linear-gradient(
    hsl(186, 76%, 16%),
    hsl(223, 90%, 60%),
    hsl(240, 56%, 42%)
  );
  box-shadow: 0 0 20px 0 hsla(223, 59%, 31%, 0.8);
}
```

Source: [`CSS/Colors/Build a Set of Colored Markers/style.css`](<../../CSS/Colors/Build a Set of Colored Markers/style.css>). Status: **Implemented**.

The green box-shadow uses an eight-digit hex colour: `#3b7e20cc`. The last two digits are the alpha channel.

### Example 2: A compact colour palette

```css
.color1 {
  background-color: #33ff57;
}
.color2 {
  background-color: rgb(128, 0, 128);
}
.color3 {
  background-color: orange;
}
.color4 {
  background-color: hsl(59, 61%, 26%);
}
.color5 {
  background-color: red;
}
```

Source: [`CSS/Colors/Design a Set of Colored Boxes/style.css`](<../../CSS/Colors/Design a Set of Colored Boxes/style.css>). Status: **Implemented**.

This exercise isolates the colour syntax from layout. Each box has the same size and border radius, so the only variable is the colour.

### Example 3: A newspaper type hierarchy

```css
.newspaper {
  font-size: 16px;
  font-family: "Open Sans", sans-serif;
  margin: 50px auto;
  background-color: white;
  max-width: 800px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  padding: 40px 15px 25px 15px;
}

.name {
  font-size: 2rem;
  font-family: "Times New Roman", serif;
  margin-bottom: 10px;
}

.headline {
  font-size: 2em;
  font-weight: bold;
  margin-bottom: 20px;
}

.sub-headline {
  font-weight: 100;
  font-size: 1.5em;
  font-style: italic;
  margin-bottom: 15px;
}

.text {
  text-indent: 20px;
  line-height: 2em;
  margin: 15px 0;
}

.text::first-letter {
  font-size: 2em;
  font-weight: bold;
}
```

Source: [`CSS/Typography/Build a Newspaper Article/style.css`](<../../CSS/Typography/Build a Newspaper Article/style.css>). Status: **Implemented**.

The name uses `rem` because it is a page-level masthead. The headline and sub-headline use `em` because they scale relative to the article's font size. The drop cap uses `::first-letter`, which is covered in the pseudo-element chapter.

### Example 4: Small informational type

```css
.label {
  border: 2px solid black;
  width: 270px;
  margin: 20px auto;
  padding: 0 7px;
}

.small-text {
  font-size: 0.85rem;
}

.note {
  font-size: 0.6rem;
  margin: 5px 0;
  padding: 0 8px;
  text-indent: -8px;
}
```

Source: [`CSS/Typography/Build a Nutritional Label/style.css`](<../../CSS/Typography/Build a Nutritional Label/style.css>). Status: **Implemented\***.

The nutritional label is a dense typographic layout: small text, bold labels, dividers, and indentation all carry meaning. The page is flagged because it lacks a viewport meta tag, so the small design may be scaled down on a phone. The typography itself is complete.

### Example 5: Invalid font shorthand

```css
#main-doc .code {
  padding: 20px 10px;
  background-color: rgb(88, 89, 91);
  color: azure;
  margin: 0 70px 20px 30px;
  border-radius: 10px;
  text-align: center;
  font: 1.2rem;
  margin-bottom: 20px;
}
```

Source: [`CSS/CERTIFICATION PROJECTS/Build a Technical Documentation Page/style.css`](<../../CSS/CERTIFICATION PROJECTS/Build a Technical Documentation Page/style.css>). Status: **Implemented**.

The `font` declaration is invalid because it has no font family. The browser ignores it. A more explicit version would use `font-size: 1.2rem;` and a separate `font-family` declaration.

## F. Step-by-step explanation

1. **Choose a base background and text colour.** Test the contrast before adding decoration.
2. **Pick a colour format.** Use what is easiest to maintain. Hex and `rgb()` are common; `hsl()` is convenient for adjusting lightness.
3. **Create a small palette.** A background, a text colour, one accent, and one muted colour are usually enough.
4. **Choose a font stack.** Start with the preferred font and always include a generic family.
5. **Set a base font size.** Use `html` or `body` so descendants can inherit or use `rem`.
6. **Build a type scale.** Give headings, body text, captions, and small print distinct sizes.
7. **Set line height for body text.** A value around `1.5` to `1.8` is comfortable for long paragraphs.
8. **Add spacing.** Use margins between blocks, not empty paragraphs.
9. **Use gradients sparingly.** They are backgrounds, not a substitute for a colour system.
10. **Test at different sizes.** Zoom to 200% and check that text does not overlap or disappear.
11. **Check contrast.** Use a contrast checker or the browser's accessibility tools.
12. **Remove invalid declarations.** The inspector will show a warning or drop the rule.

## G. Repository implementations

| Implementation | Colour and type feature | Status | Source |
| --- | --- | --- | --- |
| Colored Markers | RGB, hex, HSL, gradients, box shadows | Implemented | [Open](<../../CSS/Colors/Build a Set of Colored Markers/index.html>) |
| Colored Boxes | Named, hex, RGB, HSL colours | Implemented | [Open](<../../CSS/Colors/Design a Set of Colored Boxes/index.html>) |
| Newspaper Article | Font stacks, rem/em scale, line height, drop cap | Implemented | [Open](<../../CSS/Typography/Build a Newspaper Article/index.html>) |
| Nutritional Label | Dense typography, small text, indentation | Implemented\* | [Open](<../../CSS/Typography/Build a Nutritional Label/index.html>) |
| Technical Documentation | Invalid `font` shorthand | Implemented | [Open](<../../CSS/CERTIFICATION PROJECTS/Build a Technical Documentation Page/index.html>) |
| Blog Post Card | Simple card typography and link colour | Implemented | [Open](<../../CSS/Basic CSS/Design a Blog Post Card/index.html>) |

## H. Additional challenges

These are new practice tasks for this course; they are not requirements from the original exercises.

1. Recreate the five Colored Boxes using a single colour format instead of five different formats. Compare readability and maintainability.
2. Add a third gradient stop to the red marker and observe how the blend changes.
3. Build a page with a masthead, headline, sub-headline, byline, and body text. Use a consistent type scale.
4. Change the Newspaper Article's root font size and record how the `rem` and `em` values change.
5. Fix the Technical Documentation `font` declaration. Test both the shorthand and the separate-property version.
6. Choose two colours from the repository and check their contrast with a contrast tool. Record the ratio.
7. Create a dark-mode version of the Nutritional Label without changing its HTML.
8. Replace one named colour with an equivalent hex value and confirm that the rendering is unchanged.

## I. Common mistakes

- **Low-contrast text.** Light grey on white may look elegant and be unreadable.
- **Too many font families.** Two families are usually enough.
- **No generic fallback.** A missing font should not leave the page with the browser default.
- **Using `em` without understanding the parent size.** Nested `em` values compound.
- **Using `px` for every font size.** Relative units scale better with user preferences.
- **Using `text-transform` to change the underlying content.** It changes appearance, not the DOM text.
- **Writing an invalid `font` shorthand.** Include at least a size and a family.
- **Using gradients where a solid colour would be clearer.** Decoration should not reduce readability.
- **Relying on colour alone for state.** Add text or another visual cue.
- **Forgetting line height on long paragraphs.** Dense text is tiring to read.

## J. Summary

Colour can be written in several formats, and gradients are background images built from colour stops. Typography is a system: font stacks, a base size, a scale, line height, and spacing. `rem` and `em` connect text to user settings and parent sizes; `px` is fixed.

The Colored Markers and Colored Boxes isolate colour syntax. The Newspaper Article shows a deliberate type hierarchy. The Nutritional Label shows how much information typography can carry in a small space. The Technical Documentation page is a reminder that one invalid shorthand can silently remove a declaration.

## K. Next module

Continue to [04. Box Model and Units](04-box-model-and-units.md) to learn how content, padding, borders, and margins determine the size of every element.
