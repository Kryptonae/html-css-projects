# Projects Guide

## About this guide

This guide profiles 16 projects from the repository that are large enough, or rich enough in concepts, to study as complete pages. They are not the only exercises here. The root [README](../../README.md#complete-exercise-and-project-directory) lists every HTML and CSS practice folder, and the [course map](../README.md) links each chapter.

The profiles are based on source inspection. No demo is deployed, no JavaScript is used, and there is no build step. To run a project, open its HTML file directly in a browser. Keep the CSS file in the same folder as the HTML file so the stylesheet link resolves.

The status labels are the same ones used in the course map:

| Label | Meaning |
| --- | --- |
| **Implemented** | The page and its stylesheet are complete enough to study and run. |
| **Implemented\*** | The page works, but the source has a documented caveat. |
| **Partial** | The main structure exists, but an important part is broken or incomplete. |
| **Link issue** | A stylesheet exists, but the HTML points to a different filename. |
| **Placeholder** | The page body or stylesheet is effectively empty. |
| **HTML-only** | A complete HTML exercise with no CSS by design. |

## Project index

| # | Project | Primary focus | Status |
| --- | --- | --- | --- |
| 1 | [Survey Form](#1-survey-form) | Forms, labels, input types, validation | HTML-only |
| 2 | [Tribute Page](#2-tribute-page) | Semantic page structure, figures, Flexbox | Implemented\* |
| 3 | [Quiz](#3-quiz) | Accessible forms, fieldsets, `sr-only`, reduced motion | Link issue |
| 4 | [Product Landing Page](#4-product-landing-page) | Grid areas, Flexbox, fixed header, responsive queries | Implemented\* |
| 5 | [Technical Documentation Page](#5-technical-documentation-page) | Two-column documentation layout, anchors, media queries | Implemented |
| 6 | [Practice Personal Portfolio](#6-practice-personal-portfolio) | Flexbox, fixed navigation, repeated cards, media query | Implemented\* |
| 7 | [Magazine](#7-magazine) | Grid, named tracks, nested layout, multi-column text | Implemented |
| 8 | [Newspaper Layout](#8-newspaper-layout) | `grid-template-areas`, named regions | Implemented |
| 9 | [Piano](#9-piano) | Media queries, floats, absolute positioning, pseudo-elements | Implemented |
| 10 | [City Skyline](#10-city-skyline) | Custom properties, gradients, day/night theme | Implemented |
| 11 | [Ferris Wheel](#11-ferris-wheel) | Keyframes, rotation, counter-rotation, `transform-origin` | Implemented |
| 12 | [Flappy Penguin](#12-flappy-penguin) | Layered CSS art, keyframes, gradients, variables | Implemented\* |
| 13 | [Cat Painting](#13-cat-painting) | Absolute positioning, border triangles, z-index | Implemented\* |
| 14 | [Rothko Painting](#14-rothko-painting) | Box model, borders, padding, blur and shadow | Implemented |
| 15 | [Balance Sheet](#15-balance-sheet) | Attribute selectors, tables, screen-reader utilities | Implemented\* |
| 16 | [Book Inventory App](#16-book-inventory-app) | Attribute selectors, status styling, table markup | Partial |

## 1. Survey Form

**Path:** [`HTML/Forms and Tables/CERTIFICATION_PROJECT_Build a Survey Form/Survey_Form.html`](<../../HTML/Forms and Tables/CERTIFICATION_PROJECT_Build a Survey Form/Survey_Form.html>)  
**Status:** HTML-only  
**Related chapters:** [Forms and Inputs](../html/04-forms-and-inputs.md), [Accessibility](../html/06-accessibility.md)

### What it demonstrates

A long single-page form with text, email, and number inputs, a select menu, radio buttons, a large checkbox group, a textarea, and a submit button. It is the fullest example of form markup in the HTML folder, and it shows how much structure a real survey needs before any CSS is added.

### How to study it

1. Read the form from top to bottom and list every control type.
2. Check each `<label for="...">` against the `id` of the control it describes.
3. Notice which fields are required and which have `min`/`max` limits.
4. Submit the form with empty fields and observe the browser's built-in validation.
5. Compare the markup with the styled Registration Form in the CSS track.

### Source notes

The page has no stylesheet, so it renders as a plain vertical document. That is the intended state of the exercise, not a missing file.

There is one broken label association: the role question uses `for="role"`, but the select uses `id="dropdown"`. The field still submits because its `name` is correct, but clicking the label does not focus the select and the accessible name is not connected. The radio group also has no `<fieldset>` or `<legend>`, even though the three options form one question. These are useful fixes to practise; the documentation does not change the file.

### Run it

Open `Survey_Form.html` in a browser. No stylesheet or server is required.

## 2. Tribute Page

**Path:** [`CSS/Accessibility/Build a Tribute Page/index.html`](<../../CSS/Accessibility/Build a Tribute Page/index.html>)  
**Status:** Implemented\*  
**Related chapters:** [CSS Fundamentals](../css/01-css-fundamentals.md), [Flexbox](../css/06-flexbox.md), [Semantic HTML](../html/05-semantic-html.md)

### What it demonstrates

A single-page biography with a title, a figure and caption, a long timeline, a quotation, and an external link. The layout is built with Flexbox: the image block and the timeline block are centred columns, and the timeline is constrained with `max-width`.

### How to study it

1. Inspect how `#main` creates the page card with margins, padding, and a border radius.
2. Follow the Flexbox rules on `#img-div` and `#tribute-info`.
3. Check the image's `max-width: 100%` and `height: auto` rules.
4. Read the heading outline and compare it with the visual hierarchy.
5. Resize the window and note that the layout has no media query; it relies on fluid widths instead.

### Source notes

The page is labelled **Implemented\*** for markup reasons, not because it fails to render. The timeline heading opens with `<h3>` but closes with `</h2>`. The quotation paragraphs are direct children of `<ul>`, which is invalid list structure. The external link uses `target="_blank"` without a `rel` value. There is no mobile media query; the narrow layout depends on the fluid image and text wrapping.

The image has alt text, but it is only the person's name. The caption carries the real context. Reading the page with images disabled shows the difference between a name and a description.

### Run it

Open `index.html` in a browser. The stylesheet is in the same folder.

## 3. Quiz

**Path:** [`CSS/Accessibility/Build a Quiz Webpage, Not started W/index.html`](<../../CSS/Accessibility/Build a Quiz Webpage, Not started W/index.html>)  
**Status:** Link issue  
**Related chapters:** [Accessibility](../html/06-accessibility.md), [Selectors and Specificity](../css/02-selectors-and-specificity.md), [Responsive Design](../css/08-responsive-design.md)

### What it demonstrates

An accessible quiz form with labelled student fields, grouped true/false questions, radio buttons inside labels, a select menu, a textarea, and a submit button. The stylesheet is a compact example of `sr-only` text, `min()`/`max()`, `aspect-ratio`, a fixed header, and a reduced-motion media query.

### How to study it

1. Read the HTML first and note the `role="region"` sections with `aria-labelledby`.
2. Inspect how each radio input sits inside its `<label>`.
3. Read the stylesheet's `sr-only` utility and the `prefers-reduced-motion` query.
4. Observe the `min()` and `max()` rules on the logo and heading.
5. Then open the page and notice that it loads without styles.

### Source notes

The folder name says "Not started", but both the HTML and CSS are substantial. The real defect is the stylesheet filename: the HTML requests `styles.css`, while the file on disk is `style.css`. That is why the status is **Link issue** rather than Implemented. Opening the page shows unstyled markup until the filename is corrected in a copy.

The quiz is a markup and CSS exercise. It does not grade answers, store results, or send a completed quiz anywhere; there is no JavaScript.

### Run it

Open `index.html` in a browser to see the link issue. To study the intended design, make a copy and change the `<link>` to `style.css`.

## 4. Product Landing Page

**Path:** [`CSS/CERTIFICATION PROJECTS/Build a Product Landing Page/index.html`](<../../CSS/CERTIFICATION PROJECTS/Build a Product Landing Page/index.html>)  
**Status:** Implemented\*  
**Related chapters:** [CSS Grid](../css/07-css-grid.md), [Flexbox](../css/06-flexbox.md), [Responsive Design](../css/08-responsive-design.md), [CSS Custom Properties](../css/09-css-custom-properties.md)

### What it demonstrates

A dark-themed product page with a fixed navigation header, an email capture form, feature rows, a video embed, pricing cards, and a footer. The page combines CSS Grid for the overall page areas with Flexbox for the header, feature rows, and cards. It also defines a full set of custom properties for its palette.

### How to study it

1. Read the `grid-template-areas` declaration on `.container` and match each named area to a section.
2. Inspect the fixed `#header`, then check what keeps the first section from hiding underneath it.
3. Follow the three media queries at 720px, 650px, and 550px.
4. Compare the feature rows and pricing cards: which use Grid and which use Flexbox?
5. Check the email form's label, input, and submit control.

### Source notes

The page has several source-level issues. The "Premium Materials" feature block appears three times, so the feature section repeats content instead of showing three different features. The pricing content is also duplicated. The email input has `type="email"` but no `required`, so an empty submission is allowed. The footer links are `href="#"` placeholders. There is a stray `>` after the closing `</html>` tag.

The page has no `<h1>`; the largest heading is an `<h2>`. That is a heading-outline problem even though the visual design is clear. The iframe does have a `title`, but it is the generic "YouTube video player"; a title that names the video would be more useful.

### Run it

Open `index.html` in a browser. The external video and image load from remote URLs.

## 5. Technical Documentation Page

**Path:** [`CSS/CERTIFICATION PROJECTS/Build a Technical Documentation Page/index.html`](<../../CSS/CERTIFICATION PROJECTS/Build a Technical Documentation Page/index.html>)  
**Status:** Implemented  
**Related chapters:** [Semantic HTML](../html/05-semantic-html.md), [Responsive Design](../css/08-responsive-design.md), [Colours and Typography](../css/03-colors-and-typography.md)

### What it demonstrates

A two-column documentation layout with a fixed sidebar navigation and a scrolling main article. Each navigation link targets a section by `id`, and each section begins with a matching heading. The stylesheet uses Flexbox for the page structure and two media queries to stack the sidebar above the content at 1024px and adjust code blocks at 640px.

### How to study it

1. List every `nav-link` and confirm that its `href` matches a section `id`.
2. Read the base layout: fixed sidebar width, scrolling main region, and top offset.
3. Follow the 1024px query and note which properties change.
4. Inspect the code-block styling and the `font` declaration.
5. Test the page at a narrow width and confirm that the navigation remains usable.

### Source notes

The `.code` rule contains `font: 1.2rem;`, which is an invalid `font` shorthand because it has no font family. The browser drops the declaration, so the code blocks inherit the surrounding font size. The 640px rule also sets `font-size` twice; the later value wins.

The layout is otherwise a strong example of a documentation page: one `h1`, consistent `h2` sections, a working in-page navigation, and a clear scrolling region. It does not use JavaScript for the navigation; the anchors do all the work.

### Run it

Open `index.html` in a browser. Scroll the main article and use the sidebar links to jump between sections.

## 6. Practice Personal Portfolio

**Path:** [`CSS/Animations/Build a Personal Portfolio/index.html`](<../../CSS/Animations/Build a Personal Portfolio/index.html>)  
**Status:** Implemented\*  
**Related chapters:** [Flexbox](../css/06-flexbox.md), [Display and Positioning](../css/05-display-and-positioning.md), [Transitions and Animations](../css/11-transitions-and-animations.md)

### What it demonstrates

A portfolio page with a fixed navigation bar, a full-height welcome section, a project-card grid built with Flexbox, a contact section with icon links, and a footer. The stylesheet uses flex wrapping, `gap`, fixed positioning, hover transitions, and a 768px media query. The page also loads Font Awesome from a CDN for its icons.

### How to study it

1. Inspect the fixed header and the `main { overflow: hidden; }` rule that contains its layout.
2. Read the card container's `flex-wrap`, `gap`, and centring rules.
3. Follow the contact-link transitions and the pseudo-element labels (`::after`) that spell out "Facebook", "GitHub", and so on.
4. Test the navigation links and confirm that each section has a matching `id`.
5. Resize to the 768px breakpoint and note which font sizes change.

### Source notes

This is a fake portfolio, and the footer says so. The page repeats the same "Tribute Page" card six times rather than showing six different projects. The contact links are `href="#"` placeholders, so none of the social or contact icons leads anywhere.

The markup has duplicate IDs: `navbar-link` appears three times and `profile-link` appears five times. IDs must be unique. The CSS targets these IDs, so the duplicate markup still looks correct, but the document is invalid and the anchors are ambiguous. Several `target="_blank"` links also lack a `rel` value. The icon links have no accessible text of their own; the `::after` labels are generated content, which is not a reliable accessible name.

The page is tracked directly in the main repository, not as a nested Git repository. Its three files are part of the same commit history as the rest of the practice work.

### Run it

Open `index.html` in a browser. The Font Awesome icons require a network connection; the layout and text work without them.

## 7. Magazine

**Path:** [`CSS/Grid/Build a Magazine/index.html`](<../../CSS/Grid/Build a Magazine/index.html>)  
**Status:** Implemented  
**Related chapters:** [CSS Grid](../css/07-css-grid.md), [Responsive Design](../css/08-responsive-design.md), [Pseudo-Classes and Pseudo-Elements](../css/10-pseudo-classes-and-elements.md)

### What it demonstrates

A magazine-style page with a full-width hero, a two-column heading area, a multi-column article body, an image gallery, and an author block. The page grid uses three columns and line-based placement; the text uses `column-width` for a print-like flow. Four media queries adapt the layout at 720px, 600px, 550px, and 420px.

### How to study it

1. Read the `main` grid and identify the three columns.
2. Notice how `.heading` and `.text` sit in the middle column while `.hero` spans `1 / -1`.
3. Inspect the nested `.heading` grid and the `.image-wrapper` grid.
4. Follow the responsive changes at each breakpoint.
5. Check the `::first-letter` and quote pseudo-elements.

### Source notes

The page is visually complete, but its social icon links use only Font Awesome `<i>` elements with no visible text and no `aria-label`. A screen reader has no reliable name to announce. The links also use `target="_blank"` with `rel="noreferrer"` only.

The HTML uses remote fonts and images from freeCodeCamp's CDN. Without a network connection, the layout still works but the typography and images fall back.

### Run it

Open `index.html` in a browser. A network connection is needed for the fonts, images, and social icons.

## 8. Newspaper Layout

**Path:** [`CSS/Grid/Design a Newspaper Layout/index.html`](<../../CSS/Grid/Design a Newspaper Layout/index.html>)  
**Status:** Implemented  
**Related chapters:** [CSS Grid](../css/07-css-grid.md), [Responsive Design](../css/08-responsive-design.md)

### What it demonstrates

A newspaper front page built with `grid-template-areas`. The layout has a title row, a feature article, a cover image, a secondary article, and three small article slots. The area names make the CSS read like a page diagram.

### How to study it

1. Draw the area grid from the `grid-template-areas` strings.
2. Match each child's `grid-area` to a name in the template.
3. Inspect the `grid-template-columns` and `grid-template-rows` definitions.
4. Change one area name in a copy and observe the layout break.
5. Test the page at a narrow width and note that it does not reflow.

### Source notes

The page has no media query. The three-column grid remains three columns on a phone, so the text becomes cramped and the cover image can dominate the layout. Adding a small-screen template that stacks the areas into one column is the natural next exercise.

The HTML is small and the structure is clear. The page is a good example of a layout that is complete at desktop size but not responsive.

### Run it

Open `index.html` in a browser. No external assets are required beyond the local stylesheet and the cover image URL.

## 9. Piano

**Path:** [`CSS/Responsive Design/Design a Piano/index.html`](<../../CSS/Responsive Design/Design a Piano/index.html>)  
**Status:** Implemented  
**Related chapters:** [Display and Positioning](../css/05-display-and-positioning.md), [Responsive Design](../css/08-responsive-design.md), [CSS Art](../css/12-css-art.md)

### What it demonstrates

A visual piano built from divs. The white keys float left inside a fixed-size keyboard, and each black key is a `::after` pseudo-element positioned over its white key. Two media queries shrink the piano and its keys at 768px and at the 769px–1199px range.

### How to study it

1. Inspect the `#piano` and `.keys` dimensions and the `overflow: hidden` that contains the floats.
2. Read `.key` and `.key.black--key::after` to see how the black keys are layered.
3. Follow the two media queries and note that every dependent width is adjusted, not just the outer container.
4. Resize the window and watch the proportions change.
5. Open the page with a keyboard and note that the piano is not playable.

### Source notes

The piano is a visual exercise, not an instrument. There is no audio, no JavaScript, and no keyboard interaction. The white keys use legacy floats rather than Flexbox or Grid, which makes the width calculations fragile. The logo image is decorative; it has alt text, but the page's meaning does not depend on it.

### Run it

Open `index.html` in a browser and resize the window to see the breakpoints.

## 10. City Skyline

**Path:** [`CSS/Variables/Build a City Skyline/index.html`](<../../CSS/Variables/Build a City Skyline/index.html>)  
**Status:** Implemented  
**Related chapters:** [CSS Custom Properties](../css/09-css-custom-properties.md), [CSS Art](../css/12-css-art.md), [Flexbox](../css/06-flexbox.md)

### What it demonstrates

A skyline drawn with stacked divs, gradients, border triangles, and flex containers. The colours come from custom properties on `:root`, and a `max-width: 1000px` media query switches the palette to a night scene. The result is a complete CSS illustration with no images.

### How to study it

1. Read the `:root` palette and list every building and window colour.
2. Find the rules that use `var(--building-color...)` and `var(--window-color...)`.
3. Inspect the `.sky` radial gradient and the repeating-linear-gradient windows.
4. Follow the day/night media query and note which properties change.
5. Resize across 1000px and watch the theme switch.

### Source notes

This is a pure CSS art page with no headings or text content. Its meaning is entirely visual, so it has no accessibility text alternative. That is acceptable for a decorative exercise, but it would be insufficient if the skyline conveyed information.

The layout uses `position: absolute` and `overflow: hidden` on the body. It is designed as a full-viewport illustration, not as a content page. There is no reduced-motion concern because nothing animates.

### Run it

Open `index.html` in a browser and resize the window across the 1000px breakpoint.

## 11. Ferris Wheel

**Path:** [`CSS/Animations/Build an Animated Ferris Wheel/index.html`](<../../CSS/Animations/Build an Animated Ferris Wheel/index.html>)  
**Status:** Implemented  
**Related chapters:** [Transitions and Animations](../css/11-transitions-and-animations.md), [Display and Positioning](../css/05-display-and-positioning.md)

### What it demonstrates

A Ferris wheel assembled from a circular wheel, six spokes, and six cabins. The wheel rotates with one `@keyframes` animation, while the cabins use an opposite rotation with a different timing function to stay upright as they travel around.

### How to study it

1. Read the `.wheel`, `.line`, and `.cabin` positioning rules.
2. Compare the `transform-origin` values: the spokes rotate around `0% 0%`, the cabins around `50% 0%`.
3. Read both `@keyframes` blocks and compare their directions and timing.
4. Change the cabin timing function in a copy and describe how the motion changes.
5. Note the absence of a reduced-motion rule.

### Source notes

The animation runs forever and does not respect `prefers-reduced-motion`. That is the main accessibility gap. The visual is otherwise self-contained and uses no images.

The wheel and cabins have different timing functions, so the counter-rotation is not a perfect cancellation at every instant. The effect still reads as upright cabins, but a perfectly matched timing function would be more precise.

### Run it

Open `index.html` in a browser. The animation starts automatically.

## 12. Flappy Penguin

**Path:** [`CSS/Animations/Build a Flappy Penguin/index.html`](<../../CSS/Animations/Build a Flappy Penguin/index.html>)  
**Status:** Implemented\*  
**Related chapters:** [CSS Art](../css/12-css-art.md), [Transitions and Animations](../css/11-transitions-and-animations.md), [CSS Custom Properties](../css/09-css-custom-properties.md)

### What it demonstrates

A layered penguin scene with mountains, a sun, a penguin body, a face, a beak, wings, feet, and a belly. The illustration uses gradients, border radii, absolute positioning, pseudo-elements, custom properties, and a waving-arm keyframe animation.

### How to study it

1. Start with the scene elements: `.left-mountain`, `.back-mountain`, and `.sun`.
2. Move to `.penguin`, `.penguin-head`, and the layered face parts.
3. Inspect the custom properties for the face, skin, and beak colours.
4. Read the `wave` keyframes and the arm's `transform-origin`.
5. Test the hover and active states on the penguin.

### Source notes

The HTML has two stylesheet links. The first requests `./styles.css`, which does not exist in the folder; the second requests the actual `style.css` and loads correctly. The stale request produces a failed network request but does not break the page. The stylesheet also has no reduced-motion rule for the waving animation and no media query.

The page is a visual illustration. It does not use images, and the empty divs are decorative. The stale link is the reason for the **Implemented\*** label.

### Run it

Open `index.html` in a browser. The missing `styles.css` request is visible in the developer tools network panel; the page still renders from `style.css`.

## 13. Cat Painting

**Path:** [`CSS/Positioning/Build a Cat Painting/index.html`](<../../CSS/Positioning/Build a Cat Painting/index.html>)  
**Status:** Implemented\*  
**Related chapters:** [Display and Positioning](../css/05-display-and-positioning.md), [CSS Art](../css/12-css-art.md)

### What it demonstrates

A cat's face drawn with CSS. The head is an absolutely positioned box centred with all four offsets and `margin: auto`. The ears, eyes, nose, mouth, and whiskers are layered children positioned relative to the head, with border triangles, gradients, transforms, and `z-index`.

### How to study it

1. Read `.cat-head` and explain how the four offsets plus `margin: auto` centre it.
2. Inspect the ear rules: transparent side borders and a coloured bottom border form triangles.
3. Follow the eye, nose, and mouth layers and note the `z-index` values.
4. Resize the window and note that the fixed pixel sizes do not scale.
5. Open the page on a narrow viewport and observe the missing viewport metadata.

### Source notes

The page has no viewport meta tag. On a phone, the browser is more likely to render a wide desktop layout and shrink it, which makes the fixed-size art small and hard to inspect. The art itself is complete. That is why the label is **Implemented\*** rather than Partial.

The page has no text content and no accessible description. It is decorative art, so that is acceptable here, but it would not be an accessible instructional diagram.

### Run it

Open `index.html` in a browser. Use the developer tools to inspect the absolute positioning and z-index layers.

## 14. Rothko Painting

**Path:** [`CSS/The Box Model/Design a Rothko Painting/index.html`](<../../CSS/The Box Model/Design a Rothko Painting/index.html>)  
**Status:** Implemented  
**Related chapters:** [Box Model and Units](../css/04-box-model-and-units.md), [CSS Art](../css/12-css-art.md)

### What it demonstrates

A framed abstract painting made from three blurred rectangles. The frame is a thick border plus padding, the canvas clips its children with `overflow: hidden`, and the colour fields use slight rotations, soft shadows, `border-radius`, and `filter: blur()`.

### How to study it

1. Calculate the frame's outer width with the default `content-box` model.
2. Inspect the `.canvas` dimensions and `overflow: hidden`.
3. Compare the three colour-field rules: width, height, margin, radius, rotation, and blur.
4. Change one blur value and note how the painting changes.
5. Add `box-sizing: border-box` to a copy and compare the frame size.

### Source notes

The page does not use a global reset, so the frame's declared width is the content width. The 50px border and 50px padding add to the outer size. That makes it a useful box-model example rather than a layout bug.

The painting is decorative and has no text alternative. The page has viewport metadata and no media query; the fixed 500px canvas does not scale down on a phone.

### Run it

Open `index.html` in a browser and inspect the frame with the box-model panel in developer tools.

## 15. Balance Sheet

**Path:** [`CSS/Attribute Selectors/Build a Balance Sheet/index.html`](<../../CSS/Attribute Selectors/Build a Balance Sheet/index.html>)  
**Status:** Implemented\*  
**Related chapters:** [Selectors and Specificity](../css/02-selectors-and-specificity.md), [Lists and Tables](../html/03-lists-and-tables.md), [Accessibility](../html/06-accessibility.md)

### What it demonstrates

A financial balance sheet built from tables with year columns and category rows. The stylesheet uses attribute selectors (`[class~="sr-only"]`, `tr[class="total"]`), structural pseudo-classes, gradients, and a screen-reader-only utility. The visual years row is hidden with `aria-hidden="true"` while the table carries its own screen-reader year headers.

### How to study it

1. Read the table structure: caption, `thead`, `tbody`, and the total rows.
2. Inspect the `span[class~="sr-only"]` utility and the `#years` visual duplicate.
3. Compare `tr[class="total"]` with the class selector `tr.total` used later.
4. Follow the flex layout on the heading and the gradient rules.
5. Check the table in a screen reader or the accessibility inspector.

### Source notes

The source has two defects. In the year header row, a `<td>` wraps several `<th>` elements, which is invalid table markup; the `<th>` cells should be direct children of the `<tr>`. There is also a malformed `linear-gradient` declaration where two gradients are concatenated without a comma, so the declaration is invalid and the intended row background does not render.

The screen-reader utility itself is a standard pattern. The page's attempt to avoid announcing the years twice is thoughtful, even though the wrapper markup needs correction.

### Run it

Open `index.html` in a browser. Compare the rendered table with the source and the accessibility tree.

## 16. Book Inventory App

**Path:** [`CSS/Attribute Selectors/Build a Book Inventory App [CERTIFICATE]/index.html`](<../../CSS/Attribute Selectors/Build a Book Inventory App [CERTIFICATE]/index.html>)  
**Status:** Partial  
**Related chapters:** [Selectors and Specificity](../css/02-selectors-and-specificity.md), [Lists and Tables](../html/03-lists-and-tables.md), [Accessibility](../html/06-accessibility.md)

### What it demonstrates

A reading tracker table with columns for title, author, category, status, and rating. The stylesheet uses attribute selectors to style status classes and a five-star rating built from nested spans. It is a compact example of data-driven styling with CSS only.

### How to study it

1. Read the table headers and the five data columns.
2. Inspect the `span[class~="read"]`, `span[class~="to-read"]`, and `span[class~="in-progress"]` rules.
3. Compare those selectors with the actual status spans in the HTML.
4. Follow the rating markup and its nested spans.
5. Check the end of the table for structural errors.

### Source notes

The page is **Partial** for two reasons. First, a `</tr>` is missing near the end of the table, so the last rows are not closed correctly. Second, the stylesheet targets `span[class~="read"]`, `span[class~="to-read"]`, and `span[class~="in-progress"]`, but the status cells use `class="status"`. The background gradients therefore do not reach the visible status text. The page still displays a table, but the intended status styling is incomplete.

The folder name includes `[CERTIFICATE]`, which is part of the original path. It does not mean this repository awards a certificate. It is simply the folder label used by the practice material.

### Run it

Open `index.html` in a browser and compare the status column with the selectors in `styles.css`.

## Suggested study orders

### For HTML fundamentals

1. Survey Form
2. Tribute Page
3. Technical Documentation Page
4. Balance Sheet
5. Book Inventory App

This order moves from form markup to page structure, then to tables and selectors.

### For layout

1. Technical Documentation Page
2. Product Landing Page
3. Practice Personal Portfolio
4. Magazine
5. Newspaper Layout
6. Piano

This order moves from a two-column Flexbox page to Grid areas, then to a responsive layout with floats and media queries.

### For CSS art and motion

1. Rothko Painting
2. Cat Painting
3. City Skyline
4. Ferris Wheel
5. Flappy Penguin

This order moves from simple boxes to layered shapes, then to animation.

## What these projects do not include

- No JavaScript or interactive behaviour.
- No form backend; the forms either have no action or post to a freeCodeCamp practice endpoint.
- No build step, package manifest, test suite, or deployment configuration.
- No local media assets beyond one image in the standalone portfolio. Most images, fonts, and videos load from remote URLs.
- No certificate is issued by this repository. The `[CERTIFICATE]` text in one folder name is part of the original practice path.

The value of the collection is the source itself: complete small pages that show how HTML structure and CSS layout decisions fit together. Read them, copy them, break them, and rebuild them.
