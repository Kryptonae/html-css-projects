# 01. HTML Fundamentals

## A. Introduction

HTML (HyperText Markup Language) describes the structure and meaning of a web page. A browser reads the HTML file, builds a document tree, and decides which parts are headings, paragraphs, links, images, and landmarks. CSS can change how that structure looks, but it cannot repair a structure that was never described.

This chapter starts with the smallest useful HTML document and then examines the skeleton used by the pages in this repository. The goal is not to memorise every tag. The goal is to understand the parts of a document and why they appear in a particular order.

> **Code conventions:** A code block followed by a **Source:** link is a repository example taken from that file; the excerpt may leave out unrelated markup, and the link opens the complete source. A block without a source link is a teaching example — either a generic syntax illustration or a shortened or adapted excerpt named in the surrounding prose. Section H contains new practice tasks, not requirements from the original freeCodeCamp exercises. The original HTML and CSS files are not modified by this course.

## B. Learning objectives

By the end of this chapter you should be able to:

- Write a valid HTML document skeleton with `<!doctype html>`, `<html>`, `<head>`, and `<body>`.
- Set the document language and character encoding.
- Add a page title, viewport metadata, and a description.
- Recognise the difference between metadata in `<head>` and visible content in `<body>`.
- Explain what a parent, child, and sibling element are.
- Place page content inside landmarks such as `<main>`, `<header>`, and `<footer>`.
- Identify the document-structure choices in the repository examples.

## C. Core concepts

### The document skeleton

Every page in this repository follows the same basic pattern:

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Page title</title>
  </head>
  <body>
    <!-- visible page content -->
  </body>
</html>
```

Each part has one job:

| Part | Job |
| --- | --- |
| `<!doctype html>` | Tells the browser to use standards mode. |
| `<html lang="en">` | Wraps the document and declares its language. |
| `<head>` | Contains metadata that describes the page. |
| `<meta charset="UTF-8" />` | Declares the character encoding so text displays correctly. |
| `<meta name="viewport" ... />` | Tells mobile browsers how to size the layout. |
| `<title>` | Sets the browser-tab title and the default page title in search results. |
| `<body>` | Contains everything the visitor can see. |

`<!doctype html>` is not an HTML element. It is a declaration that comes before the root element. The repository uses both `<!doctype html>` and `<!DOCTYPE html>`; HTML is case-insensitive here, and both are accepted.

### The document tree

HTML elements form a tree. In this example, `<main>` is a child of `<body>`, and `<h1>` is a child of `<main>`:

```html
<body>
  <main>
    <h1>CatPhotoApp</h1>
    <p>Everyone loves cute cats online!</p>
  </main>
</body>
```

The `<h1>` and `<p>` are siblings because they share the same parent. The `<main>` element is the parent of both. Indentation does not create the tree, but it makes the relationships easier to read.

### Metadata is not visible content

The `<head>` describes the page. The `<body>` displays it. Putting a heading or paragraph inside `<head>` is a structural mistake because the browser does not render general content there in the same way.

The Travel Agency page shows a useful metadata set:

```html
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta name="description" content="Build a Travel Agency Page" />
  <title>Travel Agency Page</title>
</head>
```

The `description` is not shown on the page. It is a summary that search engines and other tools may use.

### Landmarks give the page shape

A landmark is a major region of a page. The most common beginner-level landmarks are:

- `<header>` for introductory content and navigation.
- `<nav>` for a set of navigation links.
- `<main>` for the primary content of the page.
- `<footer>` for closing information such as copyright or contact details.

The Cat Photo App uses these regions directly:

```html
<body>
  <main>
    <h1>CatPhotoApp</h1>
    <section>
      <h2>Cat Photos</h2>
      <!-- photos and links -->
    </section>
    <section>
      <h2>Cat Lists</h2>
      <!-- lists and figures -->
    </section>
  </main>

  <footer>
    <p>No Copyright - <a href="https://www.freecodecamp.org">freeCodeCamp.org</a></p>
  </footer>
</body>
```

There is one `<main>` because it represents the one primary content area of the page. Headers and footers can appear more than once when they belong to different sections or articles.

### Nesting and closing elements

Most elements have an opening tag and a closing tag:

```html
<p>This is a paragraph.</p>
```

Some elements are void elements and do not wrap content:

```html
<img src="cat.jpg" alt="A cat sleeping" />
<meta charset="UTF-8" />
```

A void element may end with `>` or `/>`. Both forms are used in the repository. The important rule is that elements must not overlap:

```html
<!-- Correct: the paragraph is inside the section -->
<section>
  <p>Text</p>
</section>

<!-- Incorrect: the tags cross each other -->
<section>
  <p>Text
</section>
</p>
```

## D. Syntax

The general form of an element is:

```html
<element attribute="value">content</element>
```

- `element` is the tag name.
- `attribute="value"` supplies extra information.
- `content` is the material between the tags.
- Attributes are written in the opening tag.

The root element usually carries a language attribute:

```html
<html lang="en">
```

The viewport metadata uses a content value with two parts:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

Comments are written like this:

```html
<!-- This is a comment. It is not displayed. -->
```

## E. Code examples

### Example 1: The repository skeleton

This is the opening of the Travel Agency page, including its description metadata:

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" content="Build a Travel Agency Page" />
    <title>Travel Agency Page</title>
  </head>
  <body>
    <h1>Discover Italy</h1>
    <!-- page content -->
  </body>
</html>
```

Source: [`HTML/Basic HTML Project/Build a Travel Agency Page/Build_a_Travel_Agency_Page.html`](<../../HTML/Basic HTML Project/Build a Travel Agency Page/Build_a_Travel_Agency_Page.html>).

### Example 2: Content inside landmarks

The Cat Photo App places its main content in `<main>` and its copyright line in `<footer>`:

```html
<main>
  <h1>CatPhotoApp</h1>
  <section>
    <h2>Cat Photos</h2>
    <p>Everyone loves <a href="https://cdn.freecodecamp.org/curriculum/cat-photo-app/running-cats.jpg">cute cats</a> online!</p>
  </section>
</main>

<footer>
  <p>No Copyright - <a href="https://www.freecodecamp.org">freeCodeCamp.org</a></p>
</footer>
```

Source: [`Build_a_Cat_Photo_App.html`](<../../HTML/Basic HTML Project/Build a Cat Photo App/Build_a_Cat_Photo_App.html>).

### Example 3: A page with no CSS

The Bookstore page is a plain HTML practice page. It uses headings, paragraphs, `<div>` containers, and buttons, but no stylesheet:

```html
<h1>XYZ Bookstore</h1>
<p>Browse our collection of amazing books!</p>

<div class="card-container">
  <div class="card" id="sally-adventure-book">
    <h2>Sally's SciFi Adventure</h2>
    <p>This is an epic story of Sally and her dog Rex as they navigate through other worlds.</p>
    <button class="btn">Buy Now</button>
  </div>
</div>
```

Source: [`HTML/Basic HTML Project/Build a Bookstore Page/bookstore_page.html`](<../../HTML/Basic HTML Project/Build a Bookstore Page/bookstore_page.html>). Status: **HTML-only**. The page is structurally complete as a markup exercise; it simply has no stylesheet.

## F. Step-by-step explanation

1. **Start with the doctype.** Add `<!doctype html>` so the browser does not fall back to an older rendering mode.
2. **Open the root element.** Write `<html lang="en">`. Use the language that the page is actually written in.
3. **Open the head.** Add the character encoding first so the rest of the text is interpreted correctly.
4. **Add the viewport line.** Without it, many mobile browsers assume a wide desktop layout and shrink the page.
5. **Add a descriptive title.** The title should identify the specific page, not just repeat the site name on every page.
6. **Add a description when useful.** The Travel Agency page does this; it is optional but helpful for search and sharing.
7. **Close the head and open the body.** Everything visible goes after `<body>`.
8. **Add one main region.** Put the primary content inside `<main>`.
9. **Add sections with headings.** A `<section>` should normally begin with a heading that describes it.
10. **Close elements in the reverse order they were opened.** Check the indentation when a page becomes long.
11. **Open the file in a browser.** If the structure is correct, the headings and paragraphs should appear in the expected order even before any CSS is added.

## G. Repository implementations

| Implementation | What it demonstrates | Status | Source |
| --- | --- | --- | --- |
| Travel Agency Page | Full skeleton, viewport metadata, page description | HTML-only | [Open](<../../HTML/Basic HTML Project/Build a Travel Agency Page/Build_a_Travel_Agency_Page.html>) |
| Cat Photo App | `<main>`, `<section>`, `<footer>`, nested content | HTML-only | [Open](<../../HTML/Basic HTML Project/Build a Cat Photo App/Build_a_Cat_Photo_App.html>) |
| Bookstore Page | Headings, paragraphs, `<div>` containers, buttons | HTML-only | [Open](<../../HTML/Basic HTML Project/Build a Bookstore Page/bookstore_page.html>) |
| Recipe Page | Headings, lists, image, short practice content | HTML-only | [Open](<../../HTML/Basic HTML Project/Build a Cat Photo App/HW_Build_a_Recipe_Page.html>) |
| Heart Icon | A complete document containing one inline SVG | HTML-only | [Open](<../../HTML/Basic HTML Project/Build a Heart Icon/Heart_Icon.html>) |

The Recipe Page is deliberately placeholder-like: its ingredients are "Ingredient 1", "Ingredient 2", and so on. That is the state of the practice file, not a hidden finished recipe.

## H. Additional challenges

These are new practice tasks for this course; they are not requirements from the original exercises.

1. Create `profile.html` with the full document skeleton, a meaningful `<title>`, `lang="en"`, and a one-sentence description.
2. Add one `<header>`, one `<main>`, and one `<footer>`. Put a single `<h1>` in the main region.
3. Add three sections inside `<main>`, each starting with an `<h2>`.
4. Open the page in a browser and use the developer tools to inspect the tree. Confirm which element is the parent of the `<h1>`.
5. Deliberately remove `</main>` and observe how the browser repairs the tree. Put it back afterwards and explain what changed.
6. Compare the Travel Agency and Bookstore pages. Which one uses more semantic landmarks? What would you change in the other?

## I. Common mistakes

- **Forgetting the doctype.** The page may still render, but the browser can use quirks mode.
- **Putting visible content in `<head>`.** Paragraphs and headings belong in `<body>`.
- **Omitting `lang`.** Screen readers and translation tools lose useful information about pronunciation and language.
- **Using more than one `<main>`.** A page should normally have one primary content region.
- **Skipping heading levels.** Going from `<h1>` to `<h3>` without an `<h2>` makes the outline harder to follow.
- **Closing tags in the wrong order.** Overlapping elements force the browser to guess what you meant.
- **Treating indentation as structure.** Indentation is for humans; the tags create the tree.
- **Copying a whole page just to change the title.** Reuse the skeleton, but give each page its own meaningful metadata.

## J. Summary

HTML gives a page its structure. The doctype selects standards mode, `<html lang="en">` declares the document language, `<head>` carries metadata, and `<body>` carries visible content. Landmarks such as `<header>`, `<main>`, and `<footer>` describe the major regions of the page. Nesting creates a tree, and that tree is what CSS and assistive technology read.

The repository pages are intentionally small. Their value is in the repeated skeleton and the different content structures built on top of it. Once the skeleton is familiar, the next step is to describe text, links, and images precisely.

## K. Next module

Continue to [02. Text, Links, and Images](02-text-links-and-images.md) to learn how headings, paragraphs, quotations, links, figures, and alternative text turn a skeleton into readable content.
