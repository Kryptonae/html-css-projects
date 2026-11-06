# 05. Semantic HTML

## A. Introduction

Semantic HTML means choosing elements that describe what the content is, not just how it should look. A `<div>` is a generic container with no meaning. A `<nav>` says "this is navigation". A `<main>` says "this is the primary content". That meaning is available to browsers, search engines, screen readers, and the next person who reads the source.

The repository has several pages built around landmarks and articles. It also has pages that are mostly `<div>` containers. Comparing them shows why semantic elements are worth the extra thought.

> **Code conventions:** A code block followed by a **Source:** link is a repository example taken from that file; the excerpt may leave out unrelated markup, and the link opens the complete source. A block without a source link is a teaching example — either a generic syntax illustration or a shortened or adapted excerpt named in the surrounding prose. Section H contains new practice tasks, not requirements from the original freeCodeCamp exercises. The original HTML and CSS files are not modified by this course.

## B. Learning objectives

By the end of this chapter you should be able to:

- Choose between `<div>` and a semantic landmark.
- Use `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, and `<footer>`.
- Write section headings that describe their sections.
- Explain when a `<section>` is appropriate and when a `<div>` is enough.
- Recognise an article as a self-contained unit.
- Use `<address>` for contact information.
- Identify missing or misleading semantics in a page.
- Describe how landmarks help keyboard and screen-reader users.

## C. Core concepts

### Divs are not wrong

A `<div>` is a generic block container. It is the right element when you need a styling hook or a grouping element with no semantic meaning:

```html
<div class="card-container">
  <div class="card" id="sally-adventure-book">
    <h2>Sally's SciFi Adventure</h2>
    <p>This is an epic story of Sally and her dog Rex as they navigate through other worlds.</p>
  </div>
</div>
```

The Bookstore page uses divs because the cards are generic containers. A card could be an `<article>` if each one were a self-contained composition, but in this simple page the div is defensible.

The problem starts when every part of a page is a div, including navigation, the main content, and the footer. Then the source contains no information about the page's structure.

### The major landmarks

| Element | Meaning | Typical use |
| --- | --- | --- |
| `<header>` | Introductory content for a page or section | Site title, logo, introductory text, navigation |
| `<nav>` | Major navigation links | A menu of page sections or related pages |
| `<main>` | The primary content of the document | The one region a visitor came to read |
| `<section>` | A thematic grouping with a heading | "Upcoming Events", "Past Events" |
| `<article>` | A self-contained composition | A blog post, a news story, a forum post |
| `<footer>` | Closing content for a page or section | Copyright, contact details, related links |
| `<aside>` | Content tangential to the main content | Sidebars, pull quotes, related links |

`<header>` and `<footer>` can appear inside `<article>` or `<section>` as well as at the top and bottom of the page. Their meaning depends on their parent.

### A page outline

The Event Hub is a compact semantic page:

```html
<body>
  <header>
    <h1>Event Hub</h1>
    <nav>
      <ul>
        <li><a href="#upcoming-events">Upcoming Events</a></li>
        <li><a href="#past-events">Past Events</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <section id="upcoming-events">
      <h2>Upcoming Events</h2>
      <article>
        <h3>AI & Machine Learning Conference 2024</h3>
        <p>Join us for a deep dive into the latest advancements...</p>
      </article>
    </section>

    <section id="past-events">
      <h2>Past Events</h2>
      <article>
        <h3>Cybersecurity Summit 2024</h3>
        <p>An event focusing on the latest trends and threats in cybersecurity.</p>
      </article>
    </section>
  </main>
</body>
```

The structure reads like a table of contents:

- Event Hub
  - Upcoming Events
    - AI & Machine Learning Conference 2024
    - Web Development Bootcamp
  - Past Events
    - Cybersecurity Summit 2024
    - Blockchain Expo 2024

The headings create the outline. The landmarks group the content.

### Sections need a reason and a heading

A `<section>` is a thematic group. It should normally have a heading that names the theme:

```html
<section id="about">
  <h2>About</h2>
  <p>Hi there! I'm Jane Doe, a passionate writer...</p>
</section>
```

If you only need a wrapper for styling, use a `<div>`. If the content is a self-contained item that could be syndicated or reused, consider `<article>`.

### Articles are independent units

An article should make sense on its own. A blog post is the classic example. In the Cat Blog, each post is an article with its own `<h3>`:

```html
<article>
  <h3>Mr. Whiskers' First Day Home</h3>
  <p>Lorem ipsum dolor sit amet consectetur adipisicing elit...</p>
</article>
```

The three articles are inside the "Posts" section. The page's `<h1>` names the blog, the `<h2>` names the section, and each `<h3>` names one post.

### Navigation is for navigation

Use `<nav>` for a group of major navigation links, not for every group of links on the page. A single link to a source is not a navigation landmark. The Event Hub's two section links and the Cat Blog's three section links are reasonable uses of `<nav>` because they are the page's main navigation.

### Contact information

`<address>` is for contact information for the nearest article or page author:

```html
<address>
  <p>Phone: <a href="tel:5555555555">555-555-5555</a></p>
  <p>Email: <a href="mailto:fake@email.com">fake@email.com</a></p>
</address>
```

It is not a generic address block for a street address in a fictional story, and it is not a replacement for a postal address in every context. In the Cat Blog it is used correctly for the blog's contact details.

### Headings are part of semantics

A semantic page still needs a sensible heading outline. The Coding Journey Blog demonstrates the pattern:

```html
<header>
  <h1>Welcome to Camperbot's Blog</h1>
  <nav>
    <h2>Navigation</h2>
    <ul>
      <li><a href="#post1">My Journey</a></li>
      <li><a href="#post2">Accessibility</a></li>
      <li><a href="#post3">Next Steps</a></li>
    </ul>
  </nav>
</header>
```

Using an `<h2>` inside `<nav>` labels the navigation region. Each article then begins with its own `<h2>`, and subsections use `<h3>`. The outline stays consistent.

## D. Syntax

```html
<header>
  <h1>Site title</h1>
  <nav>
    <ul>
      <li><a href="#section">Section</a></li>
    </ul>
  </nav>
</header>

<main>
  <section id="section">
    <h2>Section title</h2>
    <article>
      <h3>Article title</h3>
      <p>Article content.</p>
    </article>
  </section>
</main>

<footer>
  <p>Footer content.</p>
</footer>
```

A generic container for styling:

```html
<div class="card">
  <!-- content -->
</div>
```

## E. Code examples

### Example 1: Event Hub

```html
<header>
  <h1>Event Hub</h1>
  <nav>
    <ul>
      <li><a href="#upcoming-events">Upcoming Events</a></li>
      <li><a href="#past-events">Past Events</a></li>
    </ul>
  </nav>
</header>

<main>
  <section id="upcoming-events">
    <h2>Upcoming Events</h2>

    <article>
      <h3>AI & Machine Learning Conference 2024</h3>
      <p>Join us for a deep dive into the latest advancements in artificial intelligence and machine learning.</p>
      <p>Date: August 10, 2024</p>
    </article>
  </section>
</main>
```

Source: [`Event_Hub.html`](<../../HTML/Semantic HTML Project/Build an Event Hub/Event_Hub.html>). Status: **HTML-only**.

### Example 2: Blog structure

```html
<header>
  <h1>Welcome to Mr. Whiskers' Blog Page!</h1>
  <figure>
    <img src="https://cdn.freecodecamp.org/curriculum/css-photo-gallery/1.jpg" alt="a cat in the garden" />
    <figcaption>Mr. Whiskers in the Garden</figcaption>
  </figure>
  <nav>
    <ul>
      <li><a href="#about">About</a></li>
      <li><a href="#posts">Posts</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
  </nav>
</header>

<main>
  <section id="about">
    <h2>About</h2>
    <p>Hi there! I'm Jane Doe, a passionate writer...</p>
  </section>

  <section id="posts">
    <h2>Posts</h2>
    <article>
      <h3>Mr. Whiskers' First Day Home</h3>
      <p>Lorem ipsum dolor sit amet consectetur adipisicing elit...</p>
    </article>
  </section>
</main>

<footer>
  <section id="contact">
    <h2>Contact</h2>
    <address>
      <p>Email: <a href="mailto:fake@email.com">fake@email.com</a></p>
    </address>
  </section>
</footer>
```

Source: [`Mr._Whiskers'_Blog.html`](<../../HTML/Semantic HTML Project/Build_a_Cat_Blog_Page/Mr._Whiskers'_Blog.html>). Status: **HTML-only**.

The footer contains a section with its own heading and contact information. That is valid: the footer is a closing region, and the section gives the contact content a name.

### Example 3: A documentation layout

The Technical Documentation page uses a header containing a navigation list and a main article region:

```html
<header>
  <nav id="navbar">
    <h1>JS Documentation</h1>
    <ul>
      <li><a href="#Introduction" class="nav-link">Introduction</a></li>
      <li><a href="#Variables" class="nav-link">Variables</a></li>
    </ul>
  </nav>
</header>

<main id="main-doc">
  <section class="main-section" id="Introduction">
    <h2>Introduction</h2>
    <p>JavaScript is a cross-platform, object-oriented scripting language...</p>
  </section>
</main>
```

Source: [`CSS/CERTIFICATION PROJECTS/Build a Technical Documentation Page/index.html`](<../../CSS/CERTIFICATION PROJECTS/Build a Technical Documentation Page/index.html>). Status: **Implemented**.

The page is a good example of a documentation outline: each named section has a heading and an `id` that the navigation links target. It is styled as a two-column layout in the CSS track.

### Example 4: Mostly generic containers

The Bookstore page uses headings and paragraphs, but its product cards are divs:

```html
<div class="card-container">
  <div class="card" id="sally-adventure-book">
    <h2>Sally's SciFi Adventure</h2>
    <p>This is an epic story of Sally and her dog Rex...</p>
    <button class="btn">Buy Now</button>
  </div>
</div>
```

Source: [`bookstore_page.html`](<../../HTML/Basic HTML Project/Build a Bookstore Page/bookstore_page.html>). Status: **HTML-only**.

That is acceptable for a small practice page. The exercise in this chapter is to decide when a card becomes an article and when a container is simply a container.

## F. Step-by-step explanation

1. **Identify the page's primary content.** Wrap it in one `<main>`.
2. **Identify the introductory region.** Put the page title and main navigation in a `<header>`.
3. **Mark the navigation.** Use `<nav>` around the main link list, not around every link.
4. **Break the main content into themes.** Use `<section>` for each theme and give each one a heading.
5. **Ask whether a block is independent.** If it could be published or reused on its own, use `<article>`.
6. **Use `<div>` for styling-only wrappers.** If the element has no better meaning, a div is honest.
7. **Add a footer for closing information.** Use `<footer>` for copyright, contact details, or related links.
8. **Check the heading outline.** Read only the headings and confirm that they tell the page's story.
9. **Check the landmarks.** Use the browser's accessibility inspector or a screen reader to list the landmarks.
10. **Remove unnecessary wrappers.** Every extra div adds noise to the source.

## G. Repository implementations

| Implementation | Semantic features | Status | Source |
| --- | --- | --- | --- |
| Event Hub | Header, nav, main, sections, articles, heading hierarchy | HTML-only | [Open](<../../HTML/Semantic HTML Project/Build an Event Hub/Event_Hub.html>) |
| Cat Blog | Header, figure, nav, main, sections, articles, footer, address | HTML-only | [Open](<../../HTML/Semantic HTML Project/Build_a_Cat_Blog_Page/Mr._Whiskers'_Blog.html>) |
| Coding Journey Blog | Header, nav with a labelled heading, articles, footer | HTML-only | [Open](<../../HTML/Accessibility/Debug a Coding Journey Blog Page/index.html>) |
| Technical Documentation | Header, nav, main, sectioned documentation, anchored headings | Implemented | [Open](<../../CSS/CERTIFICATION PROJECTS/Build a Technical Documentation Page/index.html>) |
| Quincy's Tips | Main, sections, block quotations, citations | HTML-only | [Open](<../../HTML/Semantic HTML Project/Quincy's Tips for Getting a Developer Job/Quincy's_Tips_for_Getting_a_Developer_Job.html>) |
| Bookstore | Headings and generic card containers | HTML-only | [Open](<../../HTML/Basic HTML Project/Build a Bookstore Page/bookstore_page.html>) |

## H. Additional challenges

These are new practice tasks for this course; they are not requirements from the original exercises.

1. Take the Bookstore page and decide whether each card should be a `<div>`, `<section>`, or `<article>`. Write one sentence explaining each choice.
2. Add a `<header>` and `<footer>` to a page that currently has neither. Keep the visible content unchanged.
3. Write a page with three articles. Give each article its own `<header>` with an `<h2>`, and use one `<main>` for the collection.
4. Create a navigation list that jumps to three sections. Add `id` values to the sections and test the links.
5. Remove every `<div>` from the Event Hub and replace it with the most specific semantic element. Is anything left as a div?
6. Use the browser's accessibility tools to inspect the landmarks on the Cat Blog. List every landmark and its accessible name.
7. Find a page in the repository where a `<section>` has no heading. Decide whether it should become a `<div>` or gain a heading.

## I. Common mistakes

- **Using a div for navigation.** A nav is more than a styling wrapper.
- **Using `<nav>` for every link group.** Reserve it for major navigation.
- **Using multiple `<main>` elements.** There should normally be one primary content region.
- **Using `<section>` without a heading.** A section is a named theme; if it has no name, a div may be more accurate.
- **Using `<article>` for unrelated content.** An article should stand on its own.
- **Skipping heading levels.** The outline should not jump from `<h1>` to `<h3>`.
- **Putting the page title outside `<header>` when a header is used.** The header is the natural home for introductory content.
- **Believing semantic elements automatically style themselves.** Most of the visual work still belongs in CSS.
- **Adding ARIA roles to elements that already have the right semantics.** A `<nav>` already exposes navigation semantics.

## J. Summary

Semantic HTML gives the page a meaningful outline. `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, and `<footer>` describe the job of each region. `<div>` remains useful for styling-only wrappers, but it should not be the default answer for everything.

The Event Hub and Cat Blog show a clear landmark structure. The Technical Documentation page shows how sections and anchors support a long document. The Bookstore shows where generic containers are acceptable. The skill is choosing the simplest element that tells the truth about the content.

## K. Next module

Continue to [06. Accessibility](06-accessibility.md) to turn semantic structure into an experience that works with keyboards, screen readers, zoom, and reduced-motion preferences.
