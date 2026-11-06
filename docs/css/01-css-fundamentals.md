# 01. CSS Fundamentals

## A. Introduction

CSS (Cascading Style Sheets) controls how HTML is presented. HTML says what something is; CSS says how it should look. A heading can be large, a paragraph can be centred, and a container can have a background, a border, and spacing without changing the HTML structure.

This chapter starts with the stylesheet link, the anatomy of a rule, and the cascade. Those three ideas explain most of the "why is my style not applying?" questions beginners run into.

> **Code conventions:** A code block followed by a **Source:** link is a repository example taken from that file; the excerpt may leave out unrelated markup, and the link opens the complete source. A block without a source link is a teaching example — either a generic syntax illustration or a shortened or adapted excerpt named in the surrounding prose. Section H contains new practice tasks, not requirements from the original freeCodeCamp exercises. The original HTML and CSS files are not modified by this course.

## B. Learning objectives

By the end of this chapter you should be able to:

- Link an external stylesheet to an HTML page.
- Identify selectors, declarations, properties, and values.
- Explain what the cascade and inheritance do.
- Use a simple reset to make box sizing predictable.
- Read a stylesheet from top to bottom and predict which rule wins.
- Recognise the stylesheet link and rule structure used in the repository.

## C. Core concepts

### Linking a stylesheet

A page loads CSS with a `<link>` element in the `<head>`:

```html
<link href="style.css" rel="stylesheet" />
```

The Cafe Menu uses this exact pattern:

```html
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Cafe Menu</title>
  <link href="style.css" rel="stylesheet" />
</head>
```

`href` is the stylesheet location. `rel="stylesheet"` tells the browser what kind of resource it is. The link belongs in the head so the browser can load the styles before painting the page.

### Rule anatomy

A CSS rule has a selector and a declaration block:

```css
h1 {
  text-align: center;
  color: brown;
}
```

- `h1` is the selector. It chooses the elements to style.
- `text-align: center;` is a declaration.
- `text-align` is the property.
- `center` is the value.
- The braces group the declarations.
- The semicolon ends each declaration.

A selector can target more than one element:

```css
h1,
h2,
p {
  text-align: center;
}
```

This is the grouping used by the Cafe Menu. It applies one rule to three element types.

### The cascade

When several rules match the same element, the browser decides which declaration wins. The main inputs are:

1. **Importance.** `!important` declarations win over normal declarations.
2. **Origin.** Author styles normally win over browser default styles.
3. **Specificity.** A more specific selector wins over a less specific one.
4. **Source order.** If specificity is equal, the later rule wins.

A simple example:

```css
p {
  color: black;
}

.menu p {
  color: brown;
}
```

The second rule is more specific because it has a class plus an element. A paragraph inside `.menu` becomes brown.

The repository's Cafe Menu has two rules that target paragraphs:

```css
h1,
h2,
p {
  text-align: center;
}

.item p {
  display: inline-block;
  margin-top: 5px;
  margin-bottom: 5px;
  font-size: 18px;
}
```

The second rule does not repeat `text-align`, because the first rule already applies to every paragraph. Both rules can affect the same element; the cascade combines them.

### Inheritance

Some properties inherit from parent to child. Text-related properties such as `color`, `font-family`, and `line-height` usually do. Layout properties such as `margin`, `padding`, and `border` do not.

```css
body {
  font-family: Arial, Helvetica, sans-serif;
}

p {
  /* inherits Arial unless another rule changes it */
}
```

The Blog Post Card sets the font on `<body>` and lets the descendants inherit it:

```css
body {
  background-color: lightgray;
  font-family: Arial, Helvetica, sans-serif;
}
```

This is why a single body rule can set the typography for a whole page.

### Resets and box sizing

Browsers apply their own default margins, padding, and font sizes. A reset removes or normalises some of those defaults:

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
```

The Confidential Email page uses this reset. So does the Newspaper Article:

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
```

`box-sizing: border-box` makes an element's declared width include its padding and border. Without it, a 500px box with 50px padding becomes 600px wide on screen. This is one of the most useful defaults in modern CSS.

The Magazine uses a slightly different reset:

```css
*,
::before,
::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
```

Including `::before` and `::after` makes generated content follow the same box model.

### Comments

```css
/* This is a comment. */
```

The City Skyline stylesheet uses a comment to explain a selector:

```css
/* BACKGROUND BUILDINGS - "bb" stands for "background building" */
```

Comments are for the next reader, not the browser.

## D. Syntax

```css
selector {
  property: value;
  property: value;
}
```

Multiple selectors:

```css
h1,
h2,
p {
  text-align: center;
}
```

Descendant selector:

```css
.item p {
  font-size: 18px;
}
```

Universal selector with a reset:

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
```

External stylesheet:

```html
<link rel="stylesheet" href="style.css" />
```

Internal stylesheet:

```html
<style>
  body {
    background-color: whitesmoke;
  }
</style>
```

The repository uses external stylesheets. Internal CSS is useful for a quick test, but an external file keeps structure and presentation separate.

## E. Code examples

### Example 1: The Cafe Menu link

```html
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Cafe Menu</title>
  <link href="style.css" rel="stylesheet" />
</head>
```

Source: [`CSS/Basic CSS/Design a Cafe Menu/index.html`](<../../CSS/Basic CSS/Design a Cafe Menu/index.html>). Status: **Implemented**.

### Example 2: A grouped rule and a descendant rule

```css
h1,
h2,
p {
  text-align: center;
}

.item p {
  display: inline-block;
  margin-top: 5px;
  margin-bottom: 5px;
  font-size: 18px;
}
```

Source: [`CSS/Basic CSS/Design a Cafe Menu/style.css`](<../../CSS/Basic CSS/Design a Cafe Menu/style.css>). Status: **Implemented**.

The first rule centres headings and paragraphs. The second turns the paragraphs inside `.item` into inline blocks so the flavour and price can sit on one line.

### Example 3: A reset

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-color: whitesmoke;
}
```

Source: [`CSS/The Box Model/Build a Confidential Email Page/style.css`](<../../CSS/The Box Model/Build a Confidential Email Page/style.css>). Status: **Implemented**.

### Example 4: Inherited typography

```css
body {
  background-color: lightgray;
  font-family: Arial, Helvetica, sans-serif;
}

.blog-post-card {
  background-color: white;
  border-radius: 10px;
  width: 25%;
  text-align: center;
  margin: 100px auto 10px;
}
```

Source: [`CSS/Basic CSS/Design a Blog Post Card/style.css`](<../../CSS/Basic CSS/Design a Blog Post Card/style.css>). Status: **Implemented**.

The card inherits the body font and centres the text inside itself.

## F. Step-by-step explanation

1. **Create the HTML file.** Add the document skeleton and the content you want to style.
2. **Create a CSS file next to it.** Use a name such as `style.css`.
3. **Link the file in the head.** Check the path. A stylesheet in the same folder is just `style.css`.
4. **Start with a reset or a base rule.** Set `box-sizing`, margins, and a body font.
5. **Style the largest regions first.** Page background, main container, header, footer.
6. **Add component rules.** Cards, lists, buttons, and individual text elements.
7. **Read the cascade.** If a rule is not winning, check specificity and source order.
8. **Use the browser's inspector.** The Styles panel shows which declarations won and which were overridden.
9. **Remove dead rules.** A stylesheet is easier to maintain when every rule has a purpose.
10. **Test without CSS.** The HTML should still make sense if the stylesheet fails to load.

## G. Repository implementations

| Implementation | What it demonstrates | Status | Source |
| --- | --- | --- | --- |
| Cafe Menu | External link, grouped selectors, descendant selector, cascade | Implemented | [Open](<../../CSS/Basic CSS/Design a Cafe Menu/index.html>) |
| Confidential Email | Universal reset and `box-sizing` | Implemented | [Open](<../../CSS/The Box Model/Build a Confidential Email Page/index.html>) |
| Blog Post Card | Body typography inheritance and card styling | Implemented | [Open](<../../CSS/Basic CSS/Design a Blog Post Card/index.html>) |
| Business Card | Simple centred card with inherited font | Implemented | [Open](<../../CSS/Basic CSS/Design a Business Card/index.html>) |
| Newspaper Article | Reset plus inherited and local typography | Implemented | [Open](<../../CSS/Typography/Build a Newspaper Article/index.html>) |
| Stylized To-Do List | Base styles plus link states | Implemented | [Open](<../../CSS/Basic CSS/Build a Stylized To-Do List/index.html>) |

## H. Additional challenges

These are new practice tasks for this course; they are not requirements from the original exercises.

1. Create a page with one heading and two paragraphs. Link a stylesheet and centre only the heading.
2. Add a second rule that turns one paragraph brown. Predict which rule wins before you test it.
3. Remove `box-sizing: border-box` from a copy of the Confidential Email page. Measure the width change.
4. Build a page with a body font and a card that inherits it. Override the font on one child element.
5. Use the browser inspector to find every declaration that applies to the Cafe Menu's `h1`. List the winner and the overridden rules.
6. Write a comment above a rule that explains why the rule exists. Remove the comment and decide whether the rule is still self-explanatory.

## I. Common mistakes

- **Linking the wrong stylesheet filename.** The Quiz project links `styles.css` while the file is named `style.css`.
- **Putting the link in the body.** It may work, but it belongs in the head.
- **Forgetting the semicolon.** A missing semicolon can swallow the next declaration.
- **Assuming the last rule always wins.** Specificity can override source order.
- **Using `!important` to fix every conflict.** It makes the cascade harder to reason about.
- **Setting width without `box-sizing: border-box`.** Padding and borders make the element larger than expected.
- **Styling everything with IDs.** IDs create unnecessary specificity; classes are usually more reusable.
- **Leaving browser defaults unexamined.** Margins and font sizes may not match your design.
- **Deleting the stylesheet link while experimenting.** The page looks "broken" when it is simply unstyled.

## J. Summary

CSS attaches presentation rules to HTML. A rule contains a selector and declarations; declarations contain properties and values. The cascade decides which rule wins, and inheritance passes some text properties down the tree. A reset and `box-sizing: border-box` make layouts easier to predict.

The Cafe Menu and Confidential Email pages show the core pattern: link a stylesheet, reset the box model, then layer rules from general to specific. Once that pattern is comfortable, the next step is to choose selectors deliberately.

## K. Next module

Continue to [02. Selectors and Specificity](02-selectors-and-specificity.md) to learn how type, class, ID, descendant, child, and attribute selectors interact.
