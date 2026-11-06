# 02. Text, Links, and Images

## A. Introduction

Most web pages are still made of words, links, and pictures. HTML has specific elements for each of them, and the element you choose changes the meaning a browser, search engine, or screen reader receives.

A `<p>` is not just "small text". A `<blockquote>` is not just "indented text". An `<img>` with useful `alt` text is not the same as an image with `alt="Picture1"`. This chapter looks at the text and media elements used across the repository and at the details that make them readable and accessible.

> **Code conventions:** A code block followed by a **Source:** link is a repository example taken from that file; the excerpt may leave out unrelated markup, and the link opens the complete source. A block without a source link is a teaching example — either a generic syntax illustration or a shortened or adapted excerpt named in the surrounding prose. Section H contains new practice tasks, not requirements from the original freeCodeCamp exercises. The original HTML and CSS files are not modified by this course.

## B. Learning objectives

By the end of this chapter you should be able to:

- Build a heading hierarchy with one `<h1>` and nested `<h2>`/`<h3>` elements.
- Write paragraphs and inline emphasis with `<em>` and `<strong>`.
- Mark up short quotations, block quotations, and citations.
- Create absolute and relative links, including email and telephone links.
- Explain why `target="_blank"` should be paired with a safe `rel` value.
- Add images with meaningful alternative text.
- Associate an image with a caption using `<figure>` and `<figcaption>`.
- Identify weak alt text and unsafe link patterns in the repository.

## C. Core concepts

### Headings create an outline

Headings are not a font-size tool. They describe the structure of the document:

```html
<h1>Quincy's Tips for Getting a Developer Job</h1>
<main>
  <section>
    <h2>Envisioning Success</h2>
  </section>
  <section>
    <h2>Importance of Networking</h2>
  </section>
  <section>
    <h2>Importance of Building a Reputation</h2>
  </section>
</main>
```

A useful rule is: one `<h1>` for the page's main subject, `<h2>` for major sections, and `<h3>` for subsections inside them. Do not skip a level just because a smaller visual size looks better; use CSS for size.

### Paragraphs and inline meaning

`<p>` marks a paragraph. `<em>` marks stress emphasis, and `<strong>` marks strong importance. Browsers usually render them as italic and bold, but the meaning matters more than the default appearance.

```html
<p>Cats <em>love</em> lasagna.</p>
<p>Cats <strong>hate</strong> other cats.</p>
```

Both lines are from the Cat Photo App. The first stresses the word "love"; the second gives "hate" strong emphasis. Neither tag means "make this italic" or "make this bold" in the same way a CSS rule does.

### Quotations and citations

HTML distinguishes between a short inline quotation and a block quotation:

```html
<p>
  Learning to code is hard, but as Quincy Larson says,
  <q cite="https://www.freecodecamp.org/news/learn-to-code-book/">You can become a developer.</q>
</p>

<blockquote cite="https://www.freecodecamp.org/news/learn-to-code-book/">
  Can you imagine what it would be like to be a successful developer?
</blockquote>
<p>
  &mdash;Quincy Larson,
  <cite>How to Learn to Code and Get a Developer Job [Full Book]</cite>
</p>
```

- `<q>` is for a short quotation inside a sentence.
- `<blockquote>` is for a longer quotation that stands apart.
- `<cite>` identifies the title of a work.
- The `cite` attribute records a source URL, but browsers do not display it automatically.

The `&mdash;` character reference produces an em dash. It is used here instead of typing the dash directly.

### Addresses and contact links

The Cat Blog uses `<address>` for contact information:

```html
<address>
  <p>Phone: <a href="tel:5555555555">555-555-5555</a></p>
  <p>Email: <a href="mailto:fake@email.com">fake@email.com</a></p>
</address>
```

`tel:` opens a phone dialer on supported devices, and `mailto:` opens an email client. The values in this repository are fictional practice data. Do not treat them as working contact details.

### Links: absolute and relative

An absolute URL includes the scheme and host:

```html
<a href="https://www.freecodecamp.org">freeCodeCamp.org</a>
```

A relative URL is resolved from the current file's location:

```html
<a href="other-page.html">Other page</a>
<a href="../images/cat.jpg">Cat image</a>
```

This repository uses absolute external URLs because the practice pages pull assets from freeCodeCamp's CDN. It does not contain a local navigation system between the exercises, so most links point outside the repository.

### Opening links in a new tab

The Cat Photo App contains this link:

```html
<a href="https://freecatphotoapp.com" target="_blank">cat photos</a>
```

`target="_blank"` opens a new browsing context. Modern browsers protect the original page from most reverse-tabnabbing attacks, but adding `rel="noopener noreferrer"` is still a clear, portable habit:

```html
<a href="https://freecatphotoapp.com" target="_blank" rel="noopener noreferrer">cat photos</a>
```

The repository audit found 23 links with `target="_blank"`. Seventeen of them have no `rel` attribute at all, and six use only `noreferrer`. This is a documentation finding, not a claim that every link is dangerous.

### Images and alternative text

An image needs a text alternative:

```html
<img
  src="https://cdn.freecodecamp.org/curriculum/cat-photo-app/relaxing-cat.jpg"
  alt="A cute orange cat lying on its back"
/>
```

The `src` is the image location. The `alt` describes the image's content or purpose. A screen reader can read the alt text, and the text is displayed if the image fails to load.

There are two different jobs for `alt`:

- **Informative image:** describe what the viewer needs to know. "A cute orange cat lying on its back" is useful.
- **Decorative image:** use `alt=""` so assistive technology skips it. The image adds no information that is missing from the surrounding text.

Weak alt text such as `alt="Picture1"` names the file, not the content. The Travel Agency page uses `Picture1`, `Picture2`, and `Picture3` even though the images show the Colosseum, the Alps, and the sea. The captions carry the real meaning; the alt text should not depend on them.

### Figures and captions

A `<figure>` groups an image with a caption. The caption is written with `<figcaption>`:

```html
<figure>
  <img
    src="https://cdn.freecodecamp.org/curriculum/cat-photo-app/lasagna.jpg"
    alt="A slice of lasagna on a plate."
  />
  <figcaption>Cats <em>love</em> lasagna.</figcaption>
</figure>
```

The figure is a self-contained unit: image plus explanation. The caption is visible content, so it should not simply repeat the alt text word for word. The alt text describes the image; the caption adds context.

## D. Syntax

Headings:

```html
<h1>Page title</h1>
<h2>Section title</h2>
<h3>Subsection title</h3>
```

Paragraph and inline emphasis:

```html
<p>Normal text with <em>emphasis</em> and <strong>importance</strong>.</p>
```

Quotation:

```html
<q cite="https://example.com/source">Short quotation.</q>
<blockquote cite="https://example.com/source">Longer quotation.</blockquote>
<cite>Title of the work</cite>
```

Link:

```html
<a href="https://example.com" target="_blank" rel="noopener noreferrer">Link text</a>
```

Image:

```html
<img src="path-or-url" alt="Description of the image" />
```

Figure:

```html
<figure>
  <img src="path-or-url" alt="Description" />
  <figcaption>Visible caption</figcaption>
</figure>
```

## E. Code examples

### Example 1: A complete text section

The Quincy's Tips page combines a heading, a paragraph, a short quotation, a block quotation, and a citation:

```html
<h1>Quincy's Tips for Getting a Developer Job</h1>
<p>
  Learning to code is hard, but as Quincy Larson says,
  <q cite="https://www.freecodecamp.org/news/learn-to-code-book/">You can become a developer.</q>
</p>

<main>
  <section>
    <h2>Envisioning Success</h2>
    <blockquote cite="https://www.freecodecamp.org/news/learn-to-code-book/">
      Can you imagine what it would be like to be a successful developer? To
      have built software systems that people rely upon?
    </blockquote>
    <p>
      &mdash;Quincy Larson,
      <cite>How to Learn to Code and Get a Developer Job [Full Book]</cite>
    </p>
  </section>
</main>
```

Source: [`Quincy's_Tips_for_Getting_a_Developer_Job.html`](<../../HTML/Semantic HTML Project/Quincy's Tips for Getting a Developer Job/Quincy's_Tips_for_Getting_a_Developer_Job.html>). Status: **HTML-only**.

### Example 2: Image, caption, and emphasis

```html
<figure>
  <img
    src="https://cdn.freecodecamp.org/curriculum/cat-photo-app/cats.jpg"
    alt="Two tabby kittens sleeping together on a couch."
  />
  <figcaption>Cats <strong>hate</strong> other cats.</figcaption>
</figure>
```

Source: [`Build_a_Cat_Photo_App.html`](<../../HTML/Basic HTML Project/Build a Cat Photo App/Build_a_Cat_Photo_App.html>). Status: **HTML-only**.

The image is inside a link in the first Cat Photos section, but the figure example above is not. A linked image needs alt text just as much as an unlinked one.

### Example 3: Contact details

```html
<footer>
  <section id="contact">
    <h2>Contact</h2>
    <address>
      <p>Phone: <a href="tel:5555555555">555-555-5555</a></p>
      <p>Email: <a href="mailto:fake@email.com">fake@email.com</a></p>
    </address>
  </section>
</footer>
```

Source: [`Mr._Whiskers'_Blog.html`](<../../HTML/Semantic HTML Project/Build_a_Cat_Blog_Page/Mr._Whiskers'_Blog.html>). Status: **HTML-only**.

### Example 4: Weak alt text

```html
<figure>
  <a href="https://www.freecodecamp.org/learn" target="_blank">
    <img src="https://cdn.freecodecamp.org/curriculum/labs/colosseo.jpg" alt="Picture1" />
  </a>
  <figcaption>Rome and Center Italy</figcaption>
</figure>
```

Source: [`Build_a_Travel_Agency_Page.html`](<../../HTML/Basic HTML Project/Build a Travel Agency Page/Build_a_Travel_Agency_Page.html>). Status: **HTML-only**.

A better alt value would describe the scene, for example "The Colosseum in Rome". That is a new improvement suggestion, not a change made to the repository file.

## F. Step-by-step explanation

1. **Write the page heading.** Start with one `<h1>` that names the page.
2. **Break the page into sections.** Give each section an `<h2>`.
3. **Write short paragraphs.** Keep one idea per paragraph and avoid using `<br>` to create spacing.
4. **Add emphasis only where it changes meaning.** Use `<em>` for stress and `<strong>` for importance.
5. **Choose the right quotation element.** Use `<q>` inside a sentence and `<blockquote>` for a longer passage.
6. **Name the source.** Add a `<cite>` element for the title of the work when the surrounding text does not already make it clear.
7. **Write link text that makes sense on its own.** "Read the freeCodeCamp curriculum" is better than "click here".
8. **Decide whether a new tab is necessary.** If it is, add `rel="noopener noreferrer"`.
9. **Write alt text before choosing the image.** Decide what the reader needs to know, then describe that.
10. **Use a figure when the image needs a visible caption.** Put the image and `<figcaption>` inside the same `<figure>`.
11. **Check the page without images.** Disable images in the browser and confirm that the alt text still communicates the important information.

## G. Repository implementations

| Implementation | Text and media features | Status | Source |
| --- | --- | --- | --- |
| Cat Photo App | Headings, paragraphs, `em`, `strong`, links, images, figures, captions | HTML-only | [Open](<../../HTML/Basic HTML Project/Build a Cat Photo App/Build_a_Cat_Photo_App.html>) |
| Quincy's Tips | `q`, `blockquote`, `cite`, section headings | HTML-only | [Open](<../../HTML/Semantic HTML Project/Quincy's Tips for Getting a Developer Job/Quincy's_Tips_for_Getting_a_Developer_Job.html>) |
| Cat Blog | Header, figure, articles, address, `tel:` and `mailto:` links | HTML-only | [Open](<../../HTML/Semantic HTML Project/Build_a_Cat_Blog_Page/Mr._Whiskers'_Blog.html>) |
| Travel Agency | Description metadata, figures, captions, new-tab links | HTML-only | [Open](<../../HTML/Basic HTML Project/Build a Travel Agency Page/Build_a_Travel_Agency_Page.html>) |
| Recipe Page | Heading hierarchy, unordered and ordered lists, image | HTML-only | [Open](<../../HTML/Basic HTML Project/Build a Cat Photo App/HW_Build_a_Recipe_Page.html>) |

The Travel Agency page is also a useful negative example: its captions are meaningful, but its alt text is not. Reading the page with images disabled shows the gap immediately.

## H. Additional challenges

These are new practice tasks for this course; they are not requirements from the original exercises.

1. Rewrite the three Travel Agency alt values so they describe the Colosseum, the Alps, and the sea without repeating the captions word for word.
2. Add `rel="noopener noreferrer"` to one `target="_blank"` link in a copy of a repository page and explain what changes.
3. Write a short page about a book you have read. Include one `<q>`, one `<blockquote>`, one `<cite>`, and one figure with a caption.
4. Create a decorative divider image and give it `alt=""`. Explain why an empty alt is correct there.
5. Find a link in the repository whose text would be unclear out of context. Rewrite the link text without changing the destination.
6. Add an email link and a telephone link to a practice page. Use fictional values, as the Cat Blog does.

## I. Common mistakes

- **Using headings for size.** Choose the heading level for structure, then use CSS to change its appearance.
- **Skipping heading levels.** A page that jumps from `<h1>` to `<h3>` has a confusing outline.
- **Using `<br>` for paragraph spacing.** Use separate `<p>` elements and CSS margins.
- **Writing "click here" as link text.** The link should describe its destination.
- **Opening every link in a new tab.** This surprises keyboard and screen-reader users. Use it when there is a reason.
- **Omitting `rel` on new-tab links.** Add `noopener noreferrer` for safety and consistency.
- **Using alt text as a file name.** `alt="Picture1"` does not tell the reader what the image shows.
- **Repeating the caption in the alt text.** The alt describes the image; the caption adds context.
- **Forgetting `alt` entirely.** The repository audit found no images without an `alt` attribute, but a missing attribute is still a common beginner error.
- **Putting a `<figcaption>` outside its `<figure>`.** The caption should be a child of the figure it describes.

## J. Summary

Text elements carry meaning, not just appearance. Headings create an outline, paragraphs group ideas, `<em>` and `<strong>` add emphasis, and quotation elements preserve the relationship between a quotation and its source. Links need clear text and, when they open a new tab, a safe `rel` value. Images need alt text that serves the reader, and figures connect an image to its visible caption.

The repository shows both good and weak examples. The Cat Photo App's alt text and captions are useful models. The Travel Agency alt values need improvement. Recognising both is part of learning to read HTML critically.

## K. Next module

Continue to [03. Lists and Tables](03-lists-and-tables.md) to learn how to group related items and how to build tables that remain understandable when they are read by assistive technology.
