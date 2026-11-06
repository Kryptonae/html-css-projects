# 06. Accessibility

## A. Introduction

Accessibility is the practice of making a page usable by people with different abilities, devices, and preferences. It is not a separate feature added at the end. It is a consequence of the structure, labels, contrast, focus behaviour, and wording you choose while building.

This chapter uses the repository's forms, tables, links, and animation styles to show both good patterns and gaps. The pages are small enough that you can inspect the source and test the result in a browser without any special tooling.

> **Code conventions:** A code block followed by a **Source:** link is a repository example taken from that file; the excerpt may leave out unrelated markup, and the link opens the complete source. A block without a source link is a teaching example — either a generic syntax illustration or a shortened or adapted excerpt named in the surrounding prose. Section H contains new practice tasks, not requirements from the original freeCodeCamp exercises. The original HTML and CSS files are not modified by this course.

## B. Learning objectives

By the end of this chapter you should be able to:

- Write alternative text that serves the reader.
- Connect every form control to an accessible label.
- Use table captions and `scope` to communicate header relationships.
- Explain how landmark elements help navigation.
- Keep keyboard focus visible and in a sensible order.
- Write link text that makes sense out of context.
- Use `aria-hidden` and screen-reader-only text without hiding important content.
- Respect `prefers-reduced-motion`.
- Check the repository for common accessibility gaps.

## C. Core concepts

### Start with semantics

The cheapest accessibility improvement is usually the correct element. A `<button>` is keyboard-operable and announced as a button. A clickable `<div>` is not. A `<nav>` is exposed as navigation. A page made entirely of divs may look correct and still be difficult to navigate.

The semantic patterns in [05. Semantic HTML](05-semantic-html.md) are therefore part of accessibility, not a separate topic.

### Alternative text

Every informative image needs a text alternative:

```html
<img
  src="https://cdn.freecodecamp.org/curriculum/cat-photo-app/relaxing-cat.jpg"
  alt="A cute orange cat lying on its back"
/>
```

The audit for this repository found 59 HTML pages and 0 images without an `alt` attribute. That is a good baseline, but the quality still varies. The Travel Agency page uses `alt="Picture1"`, which satisfies the attribute requirement but does not describe the image.

Decorative images should use an empty alt:

```html
<img src="divider.png" alt="" />
```

The empty value tells assistive technology to skip the image. Omitting `alt` is different: the browser may announce the file name.

### Labels and instructions

A visible label connected to an input is the most reliable way to name a control:

```html
<label for="email">Email address (required):</label>
<input type="email" name="email" id="email" required />
```

Placeholders are not labels. They disappear when the user types and may not be announced consistently. A field with only a placeholder has no persistent name.

The Survey Form has a broken association:

```html
<label for="role">Which option best describes your current role?</label>
<select name="role" id="dropdown">
```

The `for` value does not match the select's `id`. The label is visually present but not programmatically connected. Changing either value fixes it.

### Tables and header relationships

A data table needs a caption and clear headers:

```html
<table>
  <caption>Schedule by Track and Time</caption>
  <thead>
    <tr>
      <th scope="col">Time</th>
      <th scope="col">Track A</th>
      <th scope="col">Track B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">9:00 AM</th>
      <td>Keynote: Tech Future</td>
      <td>Intro to Web Dev</td>
    </tr>
  </tbody>
</table>
```

`scope="col"` and `scope="row"` make the header relationships explicit. The Tech Conference schedule is the strongest table example in the repository.

### Keyboard focus

Every interactive control must be reachable with Tab and operable with the keyboard. Focus must also be visible. The To-Do List stylesheet includes a clear focus indicator:

```css
a:focus {
  outline: 2px solid blue;
}
```

Removing an outline without providing a replacement is a common accessibility failure:

```css
/* Avoid this unless you add a visible alternative */
a:focus {
  outline: none;
}
```

The Job Application Form uses a different approach: focus changes the border:

```css
input:focus,
textarea:focus {
  border: 2px solid gold;
  outline: none;
}
```

A gold border can be a visible focus indicator, but it must have enough contrast against the background. Test it rather than assuming.

### Link text and new tabs

Link text should describe the destination:

- Good: "Read the Cat Photo App source"
- Weak: "Click here"
- Weak: "Read more" when several identical links go to different places

When a link opens a new tab, tell the user. The repository has 23 `target="_blank"` links. Seventeen have no `rel` attribute, and six use only `noreferrer`. A robust pattern is:

```html
<a href="https://example.com" target="_blank" rel="noopener noreferrer">
  Example site (opens in a new tab)
</a>
```

The parenthetical text is optional, but the `rel` values are a good default.

### Screen-reader-only text

Sometimes a visual design needs a short label while the accessible version needs more context. The Balance Sheet uses a screen-reader-only utility:

```css
span[class~="sr-only"] {
  border: 0 !important;
  clip: rect(1px, 1px, 1px, 1px) !important;
  clip-path: inset(50%) !important;
  height: 1px !important;
  width: 1px !important;
  position: absolute !important;
  overflow: hidden !important;
  white-space: nowrap !important;
  padding: 0 !important;
  margin: -1px !important;
}
```

The utility visually hides content without removing it from the accessibility tree. The page also hides the visible year row with `aria-hidden="true"`:

```html
<div id="years" aria-hidden="true">
  <span class="year">2019</span>
  <span class="year">2020</span>
  <span class="year">2021</span>
</div>
```

The table then contains its own screen-reader-only year headers. The intent is to avoid announcing the years twice. The source still has a structural problem: the year `<th>` elements are wrapped in a `<td>`, which is invalid table markup. A valid version would place the `<th>` cells directly inside the `<tr>`.

### Reduced motion

Animation can cause discomfort or distraction. The Quiz stylesheet respects the user's preference:

```css
@media (prefers-reduced-motion: no-preference) {
  * {
    scroll-behavior: smooth;
  }
}
```

Smooth scrolling is enabled only when the user has not asked for reduced motion. The same principle applies to larger animations: provide a reduced-motion path or keep essential content usable without the motion.

### Zoom and viewport metadata

The viewport metadata does not directly set a zoom limit:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

It tells the browser how to size the layout on a small screen. The repository audit found 57 of 59 pages with viewport metadata. The two missing pages are the Cat Painting and the Nutritional Label. On a phone, those pages are more likely to be rendered as a wide desktop layout and scaled down, which can make text harder to read.

Do not add `user-scalable=no` or `maximum-scale=1`; those restrictions make zoom harder.

### ARIA is a supplement, not a substitute

ARIA attributes can add names and states that HTML cannot express, but they do not create behaviour. A div with `role="button"` still needs keyboard handling. Prefer native elements first.

The `aria-hidden="true"` attribute is appropriate for content that is decorative or duplicated. It is not appropriate for focusable content, because a keyboard user could move focus to something the screen reader cannot announce.

## D. Syntax

Accessible form field:

```html
<label for="email">Email</label>
<input type="email" name="email" id="email" required />
```

Accessible image:

```html
<img src="cat.jpg" alt="A cat sleeping on a windowsill" />
```

Decorative image:

```html
<img src="divider.png" alt="" />
```

Accessible table header:

```html
<th scope="col">Column name</th>
<th scope="row">Row name</th>
```

Visible focus:

```css
a:focus-visible {
  outline: 3px solid #1b1b32;
  outline-offset: 3px;
}
```

Reduced motion:

```css
@media (prefers-reduced-motion: reduce) {
  * {
    animation-duration: 0.01ms;
    animation-iteration-count: 1;
    scroll-behavior: auto;
  }
}
```

## E. Code examples

### Example 1: A form with connected labels

```html
<label for="name">Full Name:</label>
<input type="text" name="name" id="name" required />

<label for="email">Email Address:</label>
<input type="email" name="email" id="email" required />

<label for="amount">Donation Amount ($):</label>
<input type="number" name="amount" id="amount" required />

<input type="checkbox" name="newsletter" id="newsletter" />
<label for="newsletter">Subscribe</label>
```

Source: [`HTML/Accessibility/Debug a Donation Form/index.html`](<../../HTML/Accessibility/Debug a Donation Form/index.html>). Status: **HTML-only**.

The form is minimal, and its labels are correctly connected. The checkbox label comes after the input, which is valid because `for` creates the association.

### Example 2: A table with explicit header scope

```html
<table>
  <caption>Schedule by Track and Time</caption>
  <thead>
    <tr>
      <th scope="col">Time</th>
      <th scope="col">Track A</th>
      <th scope="col">Track B</th>
      <th scope="col">Track C</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">10:00 AM</th>
      <td>Accessibility Deep Dive</td>
      <td>CSS for Beginners</td>
      <td>Inclusive Design Principles</td>
    </tr>
  </tbody>
</table>
```

Source: [`HTML/Accessibility/Build a Tech Conference Schedule Table/index.html`](<../../HTML/Accessibility/Build a Tech Conference Schedule Table/index.html>). Status: **HTML-only**.

### Example 3: Focus styles

```css
a:link {
  color: saddlebrown;
}

a:focus {
  outline: 2px solid blue;
}

a:visited {
  color: blueviolet;
}

a:hover {
  color: red;
}

a:active {
  color: green;
}
```

Source: [`CSS/Basic CSS/Build a Stylized To-Do List/style.css`](<../../CSS/Basic CSS/Build a Stylized To-Do List/style.css>). Status: **Implemented**.

The five link states are deliberately different. The focus rule is the accessibility-critical one because it shows keyboard users where they are.

### Example 4: Screen-reader-only utility

```css
span[class~="sr-only"] {
  border: 0 !important;
  clip: rect(1px, 1px, 1px, 1px) !important;
  clip-path: inset(50%) !important;
  height: 1px !important;
  width: 1px !important;
  position: absolute !important;
  overflow: hidden !important;
  white-space: nowrap !important;
  padding: 0 !important;
  margin: -1px !important;
}
```

Source: [`CSS/Attribute Selectors/Build a Balance Sheet/styles.css`](<../../CSS/Attribute Selectors/Build a Balance Sheet/styles.css>). Status: **Implemented\***.

The `!important` declarations are intentional here: the utility must override the page's other styles so the text remains hidden visually but available to assistive technology.

### Example 5: Social icons without accessible names

The Magazine page uses icon-only links:

```html
<a href="https://facebook.com" target="_blank" rel="noreferrer">
  <i class="fab fa-facebook-f"></i>
</a>
```

Source: [`CSS/Grid/Build a Magazine/index.html`](<../../CSS/Grid/Build a Magazine/index.html>). Status: **Implemented\***.

The link has no visible text and no `aria-label`, so a screen reader has no reliable name to announce. A better pattern would be:

```html
<a href="https://facebook.com" target="_blank" rel="noopener noreferrer" aria-label="Facebook">
  <i class="fab fa-facebook-f" aria-hidden="true"></i>
</a>
```

This is a new improvement suggestion, not a change to the repository file.

## F. Step-by-step explanation

### Auditing a page

1. **Read the headings only.** Does the outline make sense without the paragraphs?
2. **List the landmarks.** Can you jump to the main content?
3. **Tab through the page.** Is every interactive element reachable?
4. **Watch the focus indicator.** Can you always tell where focus is?
5. **Click every label.** Does the correct control receive focus?
6. **Submit the form empty.** Are the required fields enforced?
7. **Disable images.** Does the alt text still communicate the page?
8. **Zoom to 200%.** Does the content reflow without horizontal scrolling?
9. **Use a screen reader.** Check the reading order and the names of controls.
10. **Check motion.** Does the page respect a reduced-motion preference?
11. **Read the links out of context.** Does each link text describe its destination?
12. **Check new-tab links.** Do they include a safe `rel` value and a warning?

### Fixing a broken label

1. Find the `<label for="...">` value.
2. Find the control's `id`.
3. Make the values match exactly.
4. Test by clicking the label.
5. Confirm with the browser's accessibility inspector that the control has a name.

## G. Repository implementations

| Implementation | Accessibility feature | Status | Source |
| --- | --- | --- | --- |
| Donation Form | Connected labels and required fields | HTML-only | [Open](<../../HTML/Accessibility/Debug a Donation Form/index.html>) |
| Tech Conference Table | Caption, `scope`, `colspan` | HTML-only | [Open](<../../HTML/Accessibility/Build a Tech Conference Schedule Table/index.html>) |
| Cat Photo App | Descriptive alt text and figure captions | HTML-only | [Open](<../../HTML/Basic HTML Project/Build a Cat Photo App/Build_a_Cat_Photo_App.html>) |
| To-Do List | Visible focus and distinct link states | Implemented | [Open](<../../CSS/Basic CSS/Build a Stylized To-Do List/index.html>) |
| Balance Sheet | `sr-only` text and `aria-hidden` visual duplicate | Implemented\* | [Open](<../../CSS/Attribute Selectors/Build a Balance Sheet/index.html>) |
| Quiz Webpage | Reduced-motion media query and `sr-only` utility | Link issue | [Open](<../../CSS/Accessibility/Build a Quiz Webpage, Not started W/index.html>) |
| Magazine | Icon links with no accessible name | Implemented\* | [Open](<../../CSS/Grid/Build a Magazine/index.html>) |
| Cat Painting | Animation-free CSS art, but no viewport metadata | Implemented\* | [Open](<../../CSS/Positioning/Build a Cat Painting/index.html>) |

## H. Additional challenges

These are new practice tasks for this course; they are not requirements from the original exercises.

1. Add an `aria-label` to each icon-only social link in the Magazine. Hide the icon from assistive technology with `aria-hidden="true"`.
2. Add a skip link to the Event Hub that jumps to `<main>`. Make it visible only when focused.
3. Fix the Survey Form label association without changing the visible text.
4. Audit the Travel Agency alt text. Rewrite all three values so they describe the images.
5. Add `rel="noopener noreferrer"` to one `target="_blank"` link. Test that the destination still opens.
6. Zoom a repository page to 200% and note every element that overflows or becomes unreadable.
7. Add a reduced-motion rule to the Ferris Wheel page that stops the wheel and cabin animations.
8. Test the Hotel Feedback form with only the keyboard. Record the tab order and any focus traps or unreachable controls.

## I. Common mistakes

- **Using a placeholder instead of a label.** The placeholder disappears and may not be announced.
- **A label whose `for` does not match any `id`.** The label looks right but does nothing.
- **Removing focus outlines.** Keyboard users lose their place.
- **Using colour alone to communicate state.** Add text, an icon, or another cue.
- **Writing alt text that repeats the caption.** Describe the image, then let the caption add context.
- **Omitting alt on informative images.** A missing attribute is not the same as an empty one.
- **Hiding focusable content with `aria-hidden`.** The keyboard can still reach it, but the screen reader cannot announce it.
- **Using `target="_blank"` without warning or `rel`.** The user loses context and the new page gets a reference to the opener.
- **Blocking zoom with `user-scalable=no`.** People who need magnification cannot use it.
- **Animating without a reduced-motion path.** Motion can cause discomfort.
- **Assuming automated tools are enough.** They catch some issues, not all of them.

## J. Summary

Accessibility begins with structure and labels. Images need useful alt text, forms need connected labels, tables need captions and header scope, and links need descriptive text. Keyboard focus must be visible, new tabs should be handled safely, and motion should respect user preferences. ARIA can fill small gaps, but it cannot replace native semantics and behaviour.

The repository has a solid baseline: no images are missing `alt`, the donation form has connected labels, and the conference table has explicit scope. It also has gaps: the Survey Form label mismatch, icon-only social links, missing viewport metadata on two pages, and many new-tab links without `rel`. These are concrete places to practise.

## K. Next module

Continue to [07. Multimedia and SVG](07-multimedia-and-svg.md) to learn how video, audio, embedded frames, and inline SVG fit into a well-structured page.
