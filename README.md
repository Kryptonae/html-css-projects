# HTML & CSS Learning Course

A topic-based beginner course built on this repository's 59 practice pages. The teaching material is in [`docs/`](docs/README.md); the original HTML and CSS exercises stay where they are, so every chapter can point to a real file you can open, inspect, and change.

There is no JavaScript, package manager, build step, or deployed demo. Everything runs directly in a browser.

## Table of contents

1. [Introduction](#introduction)
2. [Who this course is for](#who-this-course-is-for)
3. [Prerequisites](#prerequisites)
4. [Learning path](#learning-path)
5. [Repository at a glance](#repository-at-a-glance)
6. [HTML roadmap](#html-roadmap)
7. [CSS roadmap](#css-roadmap)
8. [Module index](#module-index)
9. [Project collection](#project-collection)
10. [Complete exercise and project directory](#complete-exercise-and-project-directory)
11. [How to run the pages](#how-to-run-the-pages)
12. [Skills practised](#skills-practised)
13. [Known gaps and source notes](#known-gaps-and-source-notes)
14. [Future goals](#future-goals)
15. [Acknowledgements](#acknowledgements)
16. [License](#license)

## Introduction

This repository began as a personal archive of freeCodeCamp Responsive Web Design practice. It has been reorganised into a course you can follow from the beginning or use for revision.

The material moves through two tracks:

- **HTML:** document structure, text, links, images, lists, tables, forms, semantic regions, accessibility, and multimedia.
- **CSS:** the cascade, selectors, colour and typography, the box model, display and positioning, Flexbox, Grid, responsive design, custom properties, pseudo-classes, transitions, animations, and CSS art.

Each chapter follows the same teaching pattern:

**Understand → Learn → See examples → Practise → Build → Revise**

Every chapter has an introduction, learning objectives, core concepts, syntax, repository examples, a step-by-step explanation, a table of real implementations, new practice challenges, common mistakes, a summary, and a link to the next module.

A code block followed by a **Source:** link is a repository example taken from that file; the excerpt may leave out unrelated markup, and the link opens the complete source. A block without a source link is a teaching example: either a generic syntax illustration or a shortened or adapted excerpt named in the surrounding prose. The new challenges are practice tasks added by this course; they are not requirements from the original freeCodeCamp exercises.

> **A note on status:** this is a learning archive, not a claim of mastery or certification. Some folders are unfinished. The status labels describe what the source files contain, not how polished the result looks.

## Who this course is for

- **Beginners** who have started HTML and CSS and want a structured path through the fundamentals.
- **Self-learners** who completed isolated exercises and want to connect the concepts.
- **Revision learners** who know the syntax but want to revisit the box model, Flexbox, Grid, or accessibility.
- **Instructors and study groups** who want small, readable pages to demonstrate a specific idea.

The course assumes you are comfortable using a computer and editing a text file. It does not assume prior JavaScript, frameworks, or build-tool experience.

## Prerequisites

| Requirement | Why it is needed |
| --- | --- |
| A modern browser | To open the HTML files and use the developer tools. |
| A text editor | To read and edit the source. Any plain-text editor works. |
| A file manager | To navigate folders whose names contain spaces, apostrophes, or brackets. |
| An internet connection for some pages | Many images, fonts, audio files, videos, and icons load from remote URLs. |
| No installation or build step | There is no `package.json`, bundler, compiler, or test runner. |

Basic familiarity with files and folders helps, but the HTML track starts from the document skeleton.

## Learning path

### If you are new to HTML and CSS

1. Read the [course map](docs/README.md) and the status legend.
2. Work through the seven HTML chapters in order: [01](docs/html/01-html-fundamentals.md) to [07](docs/html/07-multimedia-and-svg.md).
3. Work through the twelve CSS chapters in order: [01](docs/css/01-css-fundamentals.md) to [12](docs/css/12-css-art.md).
4. Pick a project from the [Projects Guide](docs/projects/projects-guide.md) and read its related chapters again with the source open.
5. Use the complete directory below to revisit any exercise.

### If you already know the basics

- Use the [HTML roadmap](#html-roadmap) and [CSS roadmap](#css-roadmap) to find the stage you need.
- Jump to a chapter from the [module index](#module-index).
- Start with the repository implementations in each chapter; they link directly to the source files.

### If you prefer learning by building

1. Choose a project from the [project collection](#project-collection).
2. Open the project's HTML and CSS side by side.
3. Follow the "How to study it" steps in the [Projects Guide](docs/projects/projects-guide.md).
4. Use the related chapter links when a property or pattern is unfamiliar.
5. Try the chapter challenges on a copy of the project, not the original file.

### Suggested pace

There is no required schedule. A comfortable pace is one HTML chapter and one CSS chapter per week, with the exercises used as revision. The chapters are independent enough that you can reorder them, but the CSS track assumes the earlier chapters' vocabulary.

## Repository at a glance

| Item | Count | Notes |
| --- | ---: | --- |
| HTML pages | **59** | 21 HTML exercises, 37 CSS project pages, 1 standalone portfolio page |
| CSS stylesheets | **38** | 37 exercise stylesheets, 1 portfolio stylesheet |
| Topic folders | **20** | 4 under `HTML/`, 16 under `CSS/` |
| Practice and project folders | **58** | 20 HTML exercise folders, 37 CSS project folders, 1 portfolio folder |
| HTML-only exercises | **21** | Deliberately have no local stylesheet |
| CSS projects | **37** | 33 implemented, 1 partial, 1 link issue, 2 placeholders |
| Implemented with caveats | **8** | Counted inside the 33 implemented projects |
| Local image assets | **1** | A portrait in `Personal Portfolio/` |
| JavaScript files | **0** | No scripts and no inline event handlers |
| Build system or dependencies | **None** | No package manifest, lockfile, bundler, or transpiler |
| Automated tests or linting | **None** | No test framework or formatter configuration |
| License | **None declared** | See [License](#license) |

### What "implemented" means here

| Label | Meaning |
| --- | --- |
| **Implemented** | The page and its stylesheet are complete enough to study and run. |
| **Implemented\*** | The page works, but the source has a documented caveat. |
| **Partial** | The main structure exists, but an important part is broken or incomplete. |
| **Link issue** | A stylesheet exists, but the HTML points to a different filename. |
| **Placeholder** | The page body or stylesheet is effectively empty. |
| **HTML-only** | A complete HTML exercise with no CSS by design. |

These are source-inspection labels. No automated accessibility audit, visual regression test, or browser-matrix test was performed.

### Repository structure

```text
.
├── README.md                  <- this learning portal
├── docs/
│   ├── README.md              <- course map and status legend
│   ├── html/                  <- seven HTML chapters
│   ├── css/                   <- twelve CSS chapters
│   └── projects/              <- sixteen project profiles
├── HTML/                      <- 21 HTML exercises in 20 folders
│   ├── Accessibility/
│   ├── Basic HTML Project/
│   ├── Forms and Tables/
│   └── Semantic HTML Project/
├── CSS/                       <- 37 CSS projects in 37 folders
│   ├── Basic CSS/
│   ├── The Box Model/
│   ├── Flexbox/
│   ├── Grid/
│   ├── Responsive Design/
│   └── ...                    <- 11 more topic folders
└── Personal Portfolio/        <- standalone portfolio page
```

## HTML roadmap

The HTML track builds from a single document skeleton to complete pages with forms, tables, and media.

| Stage | Chapters | What you learn | Repository practice |
| --- | --- | --- | --- |
| 1. Structure | [01](docs/html/01-html-fundamentals.md) | Doctype, `html`, `head`, `body`, metadata, landmarks, nesting | Travel Agency, Cat Photo App, Bookstore |
| 2. Content | [02](docs/html/02-text-links-and-images.md) | Headings, paragraphs, quotations, links, images, figures, alt text | Cat Photo App, Quincy's Tips, Cat Blog, Travel Agency |
| 3. Grouping data | [03](docs/html/03-lists-and-tables.md) | `ul`, `ol`, `dl`, tables, captions, `scope`, `colspan`, `rowspan` | Book Catalog, Tech Conference, Final Exams |
| 4. Collecting input | [04](docs/html/04-forms-and-inputs.md) | Labels, input types, fieldsets, selects, textareas, validation | Hotel Feedback, Survey Form, Donation Form |
| 5. Meaningful pages | [05](docs/html/05-semantic-html.md), [06](docs/html/06-accessibility.md) | `header`, `nav`, `main`, `section`, `article`, `footer`, focus, ARIA, table scope | Event Hub, Cat Blog, Coding Journey, Balance Sheet |
| 6. Media and graphics | [07](docs/html/07-multimedia-and-svg.md) | Video, audio, iframes, inline SVG, media fallbacks | Video Player, Music Player, Video Compilation, Heart Icon |

### HTML track outcomes

By the end of the HTML track you should be able to:

- Write a valid document skeleton and a sensible heading outline.
- Choose semantic elements instead of generic containers when meaning matters.
- Build accessible links, images, figures, tables, and forms.
- Recognise invalid table and form markup in a page you did not write.
- Explain how labels, captions, alt text, and landmarks reach assistive technology.

## CSS roadmap

The CSS track moves from the cascade and selectors to layout, adaptation, interaction, and drawing.

| Stage | Chapters | What you learn | Repository practice |
| --- | --- | --- | --- |
| 1. Foundations | [01](docs/css/01-css-fundamentals.md), [02](docs/css/02-selectors-and-specificity.md), [03](docs/css/03-colors-and-typography.md) | Stylesheet links, cascade, inheritance, selectors, specificity, colour, type | Cafe Menu, Confidential Email, Colored Markers, Newspaper Article |
| 2. Boxes and flow | [04](docs/css/04-box-model-and-units.md), [05](docs/css/05-display-and-positioning.md) | Padding, borders, margins, `box-sizing`, units, display, position, z-index, floats | Confidential Email, Event Flyer, Cat Painting, Piano |
| 3. Layout | [06](docs/css/06-flexbox.md), [07](docs/css/07-css-grid.md) | Axes, wrapping, alignment, growth, tracks, `fr`, `minmax()`, named areas | Photo Gallery, Colorful Boxes, Pricing Plans, Magazine, Newspaper Layout |
| 4. Adaptation | [08](docs/css/08-responsive-design.md), [09](docs/css/09-css-custom-properties.md) | Viewport metadata, fluid sizes, media queries, tokens, theming | Piano, Product Landing, Technical Documentation, City Skyline |
| 5. Interaction | [10](docs/css/10-pseudo-classes-and-elements.md), [11](docs/css/11-transitions-and-animations.md) | Link and form states, `:target`, `::before`, `::after`, transitions, keyframes | To-Do List, Greeting Card, Parent Teacher Form, Ferris Wheel, Flappy Penguin |
| 6. Drawing | [12](docs/css/12-css-art.md) | Borders, gradients, shadows, blur, transforms, stacking, CSS versus SVG | Cat Painting, Rothko Painting, City Skyline, Heart Icon |

### CSS track outcomes

By the end of the CSS track you should be able to:

- Explain why a declaration wins or loses in the cascade.
- Calculate the size of a box with and without `border-box`.
- Choose between normal flow, positioning, Flexbox, and Grid.
- Build a responsive layout with fluid sizes and content-driven breakpoints.
- Reuse values with custom properties and change a theme without rewriting components.
- Style interaction states and add motion that respects user preferences.
- Read a CSS illustration and explain how its layers are built.

## Module index

The [course map](docs/README.md) is the short version of this section. The table below lists every chapter and one good place to start.

### HTML modules

| Module | Focus | Start with |
| --- | --- | --- |
| [01. HTML Fundamentals](docs/html/01-html-fundamentals.md) | Document skeleton, metadata, landmarks, nesting | [Travel Agency](<HTML/Basic HTML Project/Build a Travel Agency Page/Build_a_Travel_Agency_Page.html>) |
| [02. Text, Links, and Images](docs/html/02-text-links-and-images.md) | Headings, emphasis, quotations, links, alt text, figures | [Cat Photo App](<HTML/Basic HTML Project/Build a Cat Photo App/Build_a_Cat_Photo_App.html>) |
| [03. Lists and Tables](docs/html/03-lists-and-tables.md) | List types, nesting, table sections, `scope`, spans | [Tech Conference Schedule](<HTML/Accessibility/Build a Tech Conference Schedule Table/index.html>) |
| [04. Forms and Inputs](docs/html/04-forms-and-inputs.md) | Labels, input types, fieldsets, validation | [Hotel Feedback Form](<HTML/Forms and Tables/Build a Hotel Feedback Form/Hotel_Feedback_Form.html>) |
| [05. Semantic HTML](docs/html/05-semantic-html.md) | Landmarks, sections, articles, headings, `address` | [Event Hub](<HTML/Semantic HTML Project/Build an Event Hub/Event_Hub.html>) |
| [06. Accessibility](docs/html/06-accessibility.md) | Alt text, labels, table scope, focus, ARIA, reduced motion | [Donation Form](<HTML/Accessibility/Debug a Donation Form/index.html>) |
| [07. Multimedia and SVG](docs/html/07-multimedia-and-svg.md) | Video, audio, iframes, inline SVG, media fallbacks | [Video Player](<HTML/Basic HTML Project/Build an HTML Video Player/HTML_Video_Player.html>) |

### CSS modules

| Module | Focus | Start with |
| --- | --- | --- |
| [01. CSS Fundamentals](docs/css/01-css-fundamentals.md) | Stylesheet links, rule anatomy, cascade, inheritance, resets | [Cafe Menu](<CSS/Basic CSS/Design a Cafe Menu/index.html>) |
| [02. Selectors and Specificity](docs/css/02-selectors-and-specificity.md) | Type, class, ID, descendant, child, attribute selectors | [Balance Sheet](<CSS/Attribute Selectors/Build a Balance Sheet/index.html>) |
| [03. Colours and Typography](docs/css/03-colors-and-typography.md) | Colour formats, gradients, font stacks, type scales | [Colored Markers](<CSS/Colors/Build a Set of Colored Markers/index.html>) |
| [04. Box Model and Units](docs/css/04-box-model-and-units.md) | Content, padding, border, margin, `box-sizing`, units | [Confidential Email](<CSS/The Box Model/Build a Confidential Email Page/index.html>) |
| [05. Display and Positioning](docs/css/05-display-and-positioning.md) | Normal flow, `display`, `position`, `z-index`, floats | [Cat Painting](<CSS/Positioning/Build a Cat Painting/index.html>) |
| [06. Flexbox](docs/css/06-flexbox.md) | Axes, wrapping, alignment, growth, ordering | [Photo Gallery](<CSS/Flexbox/Build a Flexbox Photo Gallery/index.html>) |
| [07. CSS Grid](docs/css/07-css-grid.md) | Tracks, `fr`, `minmax()`, line placement, named areas | [Magazine](<CSS/Grid/Build a Magazine/index.html>) |
| [08. Responsive Design](docs/css/08-responsive-design.md) | Viewport metadata, fluid sizes, media queries, breakpoints | [Piano](<CSS/Responsive Design/Design a Piano/index.html>) |
| [09. CSS Custom Properties](docs/css/09-css-custom-properties.md) | `--tokens`, `var()`, scoping, fallbacks, themes | [City Skyline](<CSS/Variables/Build a City Skyline/index.html>) |
| [10. Pseudo-Classes and Pseudo-Elements](docs/css/10-pseudo-classes-and-elements.md) | Link states, focus, validation, `:target`, generated content | [Greeting Card](<CSS/Pseudo Classes and Elements/Design a Greeting Card/index.html>) |
| [11. Transitions and Animations](docs/css/11-transitions-and-animations.md) | Transitions, transforms, keyframes, reduced motion | [Ferris Wheel](<CSS/Animations/Build an Animated Ferris Wheel/index.html>) |
| [12. CSS Art](docs/css/12-css-art.md) | Borders, gradients, shadows, blur, transforms, stacking | [Rothko Painting](<CSS/The Box Model/Design a Rothko Painting/index.html>) |

## Project collection

The [Projects Guide](docs/projects/projects-guide.md) profiles 16 larger or concept-rich pages. Each profile covers the path, status, concepts, study steps, source-level notes, related chapters, and how to run it.

| Project | Main focus | Status |
| --- | --- | --- |
| [Survey Form](docs/projects/projects-guide.md#1-survey-form) | Form controls, labels, native validation | HTML-only |
| [Tribute Page](docs/projects/projects-guide.md#2-tribute-page) | Figure, timeline, Flexbox, fluid image | Implemented\* |
| [Quiz](docs/projects/projects-guide.md#3-quiz) | Accessible form regions, `sr-only`, reduced motion | Link issue |
| [Product Landing Page](docs/projects/projects-guide.md#4-product-landing-page) | Grid areas, fixed header, responsive queries, tokens | Implemented\* |
| [Technical Documentation Page](docs/projects/projects-guide.md#5-technical-documentation-page) | Fixed sidebar, scrolling article, anchors | Implemented |
| [Practice Personal Portfolio](docs/projects/projects-guide.md#6-practice-personal-portfolio) | Fixed nav, Flexbox cards, contact icons | Implemented\* |
| [Magazine](docs/projects/projects-guide.md#7-magazine) | Grid placement, nested grids, multi-column text | Implemented |
| [Newspaper Layout](docs/projects/projects-guide.md#8-newspaper-layout) | Named grid areas | Implemented |
| [Piano](docs/projects/projects-guide.md#9-piano) | Media queries, floats, pseudo-element keys | Implemented |
| [City Skyline](docs/projects/projects-guide.md#10-city-skyline) | Custom properties, gradients, day/night theme | Implemented |
| [Ferris Wheel](docs/projects/projects-guide.md#11-ferris-wheel) | Keyframes, rotation, counter-rotation | Implemented |
| [Flappy Penguin](docs/projects/projects-guide.md#12-flappy-penguin) | Layered CSS art, gradients, keyframe wave | Implemented\* |
| [Cat Painting](docs/projects/projects-guide.md#13-cat-painting) | Absolute positioning, border triangles, z-index | Implemented\* |
| [Rothko Painting](docs/projects/projects-guide.md#14-rothko-painting) | Box model, blur, shadow, rotation | Implemented |
| [Balance Sheet](docs/projects/projects-guide.md#15-balance-sheet) | Attribute selectors, table structure, `sr-only` | Implemented\* |
| [Book Inventory App](docs/projects/projects-guide.md#16-book-inventory-app) | Attribute selectors, status styling, table markup | Partial |

## Complete exercise and project directory

All 59 pages are listed below. Links go directly to the HTML file. Unless a row says otherwise, the page is an HTML-only exercise or an implemented CSS project with a local stylesheet.

### HTML exercises (21 pages in 20 folders)

| Exercise | Main practice focus | Status |
| --- | --- | --- |
| [Tech Conference Schedule Table](<HTML/Accessibility/Build a Tech Conference Schedule Table/index.html>) | Caption, `scope`, `colspan`, accessible table structure | HTML-only |
| [Coding Journey Blog Page](<HTML/Accessibility/Debug a Coding Journey Blog Page/index.html>) | Header, nav, articles, footer, internal anchors, `mailto:` | HTML-only |
| [Donation Form](<HTML/Accessibility/Debug a Donation Form/index.html>) | Labels, required fields, text, email, number, checkbox | HTML-only |
| [Bookstore Page](<HTML/Basic HTML Project/Build a Bookstore Page/bookstore_page.html>) | Headings, cards, buttons, simple page flow | HTML-only |
| [Cat Photo App](<HTML/Basic HTML Project/Build a Cat Photo App/Build_a_Cat_Photo_App.html>) | Sections, images, links, lists, figures, footer | HTML-only |
| [Recipe Page](<HTML/Basic HTML Project/Build a Cat Photo App/HW_Build_a_Recipe_Page.html>) | Headings, ingredient and instruction lists, image | HTML-only |
| [Heart Icon](<HTML/Basic HTML Project/Build a Heart Icon/Heart_Icon.html>) | Inline SVG, `viewBox`, `path`, `fill` | HTML-only |
| [Travel Agency Page](<HTML/Basic HTML Project/Build a Travel Agency Page/Build_a_Travel_Agency_Page.html>) | Meta description, figures, linked images, external links | HTML-only |
| [Video Compilation Page](<HTML/Basic HTML Project/Build a Video Compilation Page/Video_Compilation_Page.html>) | Three YouTube iframes, `allow`, `referrerpolicy` | HTML-only |
| [Video Display Using iframe](<HTML/Basic HTML Project/Build a Video Display Using iframe/Display Videos_in_an_iframe.html>) | Standalone iframe attributes | HTML-only |
| [Audio and Video Player](<HTML/Basic HTML Project/Build an HTML Audio and Video Player/Build an HTML Audio_and_Video_Player.html>) | Native `<video>`, nested `<source>`, native `<audio>` | HTML-only |
| [Music Player](<HTML/Basic HTML Project/Build an HTML Music Player/HTML_Music_Player.html>) | Three audio elements with controls and loop | HTML-only |
| [Video Player](<HTML/Basic HTML Project/Build an HTML Video Player/HTML_Video_Player.html>) | Four source formats, poster, controls, loop, muted | HTML-only |
| [Book Catalog Table](<HTML/Forms and Tables/Build a Book Catalog Table/Book_Catalog.html>) | Caption, `thead`, `tbody`, `tfoot`, total row | HTML-only |
| [Final Exams Table](<HTML/Forms and Tables/Build a Final Exams Table/Calculus_Final_Exams_Table.html>) | Table sections and average-grade footer | HTML-only |
| [Hotel Feedback Form](<HTML/Forms and Tables/Build a Hotel Feedback Form/Hotel_Feedback_Form.html>) | Fieldsets, legends, labels, radios, checkboxes, selects, textarea | HTML-only |
| [Survey Form](<HTML/Forms and Tables/CERTIFICATION_PROJECT_Build a Survey Form/Survey_Form.html>) | Long form, labels, required fields, radios, checkboxes, textarea | HTML-only |
| [Event Hub](<HTML/Semantic HTML Project/Build an Event Hub/Event_Hub.html>) | Semantic regions, internal navigation, event articles | HTML-only |
| [Cat Blog Page](<HTML/Semantic HTML Project/Build_a_Cat_Blog_Page/Mr._Whiskers'_Blog.html>) | Header, nav, articles, figure, footer, address | HTML-only |
| [List of Major Web Browsers](<HTML/Semantic HTML Project/List of Major Web Browsers/List_of_Major_Web_Browsers.html>) | Description list (`dl`, `dt`, `dd`) | HTML-only |
| [Quincy's Tips for Getting a Developer Job](<HTML/Semantic HTML Project/Quincy's Tips for Getting a Developer Job/Quincy's_Tips_for_Getting_a_Developer_Job.html>) | Semantic sections, `q`, `blockquote`, `cite` | HTML-only |

The Recipe Page uses placeholder ingredient text, and the Cat Blog uses lorem-ipsum post bodies. The Final Exams table nests `<tfoot>` inside `<tbody>`, and the Survey Form has a label/select ID mismatch. These are documented source notes, not changes made to the files.

### CSS projects (37 pages in 37 folders)

| Project | Main practice focus | Status |
| --- | --- | --- |
| [Event Flyer Page](<CSS/Absolute and Relative Units/Build an Event Flyer Page/index.html>) | `vw`, percentages, `calc()`, Flexbox columns | Implemented |
| [Accessibility Quiz](<CSS/Accessibility/Build a Quiz Webpage, Not started W/index.html>) | ARIA regions, labels, `.sr-only`, reduced motion | Link issue |
| [Tribute Page](<CSS/Accessibility/Build a Tribute Page/index.html>) | Figure, timeline, Flexbox, fluid image | Implemented\* |
| [Flappy Penguin](<CSS/Animations/Build a Flappy Penguin/index.html>) | CSS art, variables, gradients, keyframe wave | Implemented\* |
| [Moon Orbit](<CSS/Animations/Build a Moon Orbit/index.html>) | Flex centring, absolute positioning, orbit keyframes | Implemented\* |
| [Practice Personal Portfolio](<CSS/Animations/Build a Personal Portfolio/index.html>) | Fixed navigation, hero, Flexbox cards, media query | Implemented\* |
| [Animated Ferris Wheel](<CSS/Animations/Build an Animated Ferris Wheel/index.html>) | Rotation, `:nth-of-type()` spokes, counter-rotating cabins | Implemented |
| [Balance Sheet](<CSS/Attribute Selectors/Build a Balance Sheet/index.html>) | Attribute selectors, tables, screen-reader utility | Implemented\* |
| [Book Inventory App](<CSS/Attribute Selectors/Build a Book Inventory App [CERTIFICATE]/index.html>) | Attribute selectors for reading-status states | Partial |
| [Stylized To-Do List](<CSS/Basic CSS/Build a Stylized To-Do List/index.html>) | Card spacing, nested lists, link states, checkboxes | Implemented |
| [Blog Post Card](<CSS/Basic CSS/Design a Blog Post Card/index.html>) | Card composition, image corners, hover state | Implemented |
| [Business Card](<CSS/Basic CSS/Design a Business Card/index.html>) | Centred card, typography, borders, horizontal rules | Implemented |
| [Cafe Menu](<CSS/Basic CSS/Design a Cafe Menu/index.html>) | Background image, max-width container, inline-block rows, link states | Implemented |
| [Product Landing Page](<CSS/CERTIFICATION PROJECTS/Build a Product Landing Page/index.html>) | Grid areas, fixed header, form, video, pricing cards, variables | Implemented\* |
| [Technical Documentation Page](<CSS/CERTIFICATION PROJECTS/Build a Technical Documentation Page/index.html>) | Fixed sidebar, scrolling article, anchors, breakpoints | Implemented |
| [Colored Markers](<CSS/Colors/Build a Set of Colored Markers/index.html>) | `rgb()`, `hsl()`, alpha colours, gradients, shadows | Implemented |
| [Colored Boxes](<CSS/Colors/Design a Set of Colored Boxes/index.html>) | Hex, `rgb()`, named colours, `hsl()`, Flexbox wrapping | Implemented |
| [Flexbox Photo Gallery](<CSS/Flexbox/Build a Flexbox Photo Gallery/index.html>) | Wrap, centring, gaps, `object-fit`, `::after` spacer | Implemented |
| [Playing Cards](<CSS/Flexbox/Build a Page of Playing Cards, Not started [Certification Project]/index.html>) | Nested Flexbox, card faces, transforms, wrapping | Implemented |
| [Pricing Plans Layout](<CSS/Flexbox/Design a Pricing Plans Layout Page/index.html>) | `order`, `flex-grow`, wrapping, hover scaling | Implemented |
| [Colorful Boxes](<CSS/Flexbox/Design a Set of Colorful Boxes/index.html>) | `flex-grow`, `flex-shrink`, `order`, `align-content` | Implemented |
| [Magazine](<CSS/Grid/Build a Magazine/index.html>) | Grid, `minmax()`, nested grids, columns, typography, breakpoints | Implemented |
| [Newspaper Layout](<CSS/Grid/Design a Newspaper Layout/index.html>) | Named grid areas, explicit columns and rows | Implemented |
| [Cat Painting](<CSS/Positioning/Build a Cat Painting/index.html>) | Absolute positioning, border triangles, gradients, z-index | Implemented\* |
| [House Painting](<CSS/Positioning/Build a House Painting/index.html>) | Intended positioning and CSS-art practice | Placeholder |
| [Job Application Form](<CSS/Pseudo Classes and Elements/Build a Job Application Form/index.html>) | `:focus`, `:valid`, `:invalid`, `:not()`, form sizing | Implemented |
| [Greeting Card](<CSS/Pseudo Classes and Elements/Design a Greeting Card/index.html>) | Link states, `::before`/`::after`, `:target`, transitions | Implemented |
| [Parent Teacher Conference Form](<CSS/Pseudo Classes and Elements/Design a Parent Teacher Conference Form/index.html>) | `appearance: none`, custom radios, `:checked` | Implemented |
| [Piano](<CSS/Responsive Design/Design a Piano/index.html>) | Floats, positioning, pseudo-element keys, media queries | Implemented |
| [Contact Form](<CSS/Styling Forms/Design a Contact Form/index.html>) | Complete form HTML; stylesheet is empty | Placeholder |
| [Registration Form](<CSS/Styling Forms/Design a Registration Form/index.html>) | Attribute selectors, fieldsets, responsive width | Implemented |
| [Confidential Email Page](<CSS/The Box Model/Build a Confidential Email Page/index.html>) | Box model, shadow, absolute stamps, rotation, blur | Implemented |
| [Rothko Painting](<CSS/The Box Model/Design a Rothko Painting/index.html>) | Box model, borders, padding, blur, transforms | Implemented |
| [Newspaper Article](<CSS/Typography/Build a Newspaper Article/index.html>) | `rem`/`em`, font stacks, uppercase, line height, first letter | Implemented |
| [Nutritional Label](<CSS/Typography/Build a Nutritional Label/index.html>) | Web fonts, Flexbox rows, `:not()`, dense typography | Implemented\* |
| [City Skyline](<CSS/Variables/Build a City Skyline/index.html>) | Custom properties, gradients, Flexbox, day/night theme | Implemented |
| [Availability Table](<CSS/Variables/Build an Availability Table/index.html>) | Custom properties, table styling, `rowspan`, legend | Implemented |

The 33 implemented projects include the 8 marked **Implemented\***. The other four are one partial project, one stylesheet-link issue, and two placeholders.

### Standalone portfolio (1 page)

| Page | Main practice focus | Status |
| --- | --- | --- |
| [Personal Portfolio](<Personal Portfolio/index.html>) | Grid `auto-fit`, Flexbox, custom properties, responsive cards | Implemented |

The portfolio is tracked directly in the main repository, not as a nested Git repository or submodule. It has no media query; it relies on `auto-fit` Grid tracks and Flexbox wrapping. It contains a portrait image and contact-style details that appear personal. Do not republish or reuse that folder without reviewing and redacting it first.

## How to run the pages

1. Open the repository folder in your file manager.
2. Navigate to an exercise folder.
3. Open its `.html` file in a browser. Double-clicking usually works.
4. Keep the HTML file and its stylesheet in the same folder so the `<link>` resolves.
5. Use the browser's developer tools to inspect the DOM, the CSS cascade, and the box model.

There is no root `index.html`. The links in this README and in `docs/` are the navigation system. A local server is optional; it is useful if your browser restricts local file access, but no server-side code is required.

Remote images, fonts, icons, audio, and videos need an internet connection. If an asset fails to load, the page structure and local CSS still apply. Some pages use `file://`-friendly remote URLs; others use YouTube embeds, which require a network connection.

## Skills practised

### HTML

- Document structure, metadata, language, and viewport settings.
- Heading hierarchy and semantic text elements.
- Links, internal anchors, `mailto:`, and `tel:`.
- Images, alternative text, figures, and captions.
- Ordered, unordered, description, and nested lists.
- Data tables with captions, sections, `scope`, `colspan`, and `rowspan`.
- Forms with labels, fieldsets, legends, input types, selects, textareas, and native validation.
- Semantic landmarks: `header`, `nav`, `main`, `section`, `article`, `footer`, and `address`.
- Accessibility basics: focus, table scope, `sr-only` text, `aria-hidden`, and reduced-motion preferences.
- Native video, audio, iframes, and inline SVG.

### CSS

- External stylesheets, rule anatomy, cascade, inheritance, and resets.
- Type, class, ID, descendant, child, attribute, and pseudo-class selectors.
- Specificity, source order, and deliberate `!important` use.
- Named, hex, `rgb()`/`rgba()`, and `hsl()`/`hsla()` colours.
- Linear, radial, and repeating gradients.
- Font stacks, type scales, line height, letter spacing, and text effects.
- The box model, `box-sizing`, `max-width`, `overflow`, borders, and shadows.
- Units: `px`, `%`, `rem`, `em`, `vw`, `vh`, and `calc()`.
- Normal flow, `display`, `position`, `z-index`, and floats.
- Flexbox axes, wrapping, alignment, growth, shrinking, and ordering.
- Grid tracks, `fr`, `minmax()`, `repeat()`, named areas, and nested grids.
- Viewport metadata, media queries, fluid images, `min()`, `max()`, and `aspect-ratio`.
- Custom properties, scoping, fallbacks, and theme switching.
- Pseudo-classes and pseudo-elements, including `:target`, `:checked`, `:valid`, `:invalid`, `::before`, and `::after`.
- Transitions, transforms, keyframes, `transform-origin`, and reduced-motion considerations.
- CSS art with borders, gradients, shadows, blur, and stacking.

### General practice

- Reading source files critically instead of trusting folder names.
- Comparing folder names with the actual implementation status.
- Documenting caveats without modifying the original exercise.
- Writing relative links to files whose names contain spaces, apostrophes, and brackets.
- Explaining code in plain language.

## Known gaps and source notes

### Non-implemented projects

| Project | Issue |
| --- | --- |
| [Quiz](<CSS/Accessibility/Build a Quiz Webpage, Not started W/index.html>) | The HTML requests `styles.css`, but the stylesheet is named `style.css`. The page loads unstyled. |
| [Book Inventory App](<CSS/Attribute Selectors/Build a Book Inventory App [CERTIFICATE]/index.html>) | A `</tr>` is missing near the end of the table, and the status selectors target classes that the status spans do not use. |
| [House Painting](<CSS/Positioning/Build a House Painting/index.html>) | The body is empty and the stylesheet is empty. There is no house to study yet. |
| [Contact Form](<CSS/Styling Forms/Design a Contact Form/index.html>) | The form markup is complete, but `style.css` is empty. |

### Implemented with caveats

- **Tribute Page:** the timeline opens with `<h3>` and closes with `</h2>`; `<p>` elements sit directly inside `<ul>`; the new-tab link has no `rel`.
- **Product Landing Page:** the feature and pricing content is duplicated, a stray `>` follows `</html>`, the footer links are placeholders, the email input is not `required`, and the page has no `<h1>`.
- **Practice Personal Portfolio:** `id="navbar-link"` appears three times and `id="profile-link"` appears five times; six identical project cards are repeated; contact links are placeholders.
- **Flappy Penguin:** the HTML requests a missing `./styles.css` before loading the valid `style.css`.
- **Cat Painting:** the page has no viewport metadata.
- **Nutritional Label:** the page has no viewport metadata.
- **Balance Sheet:** a `<td>` wraps several `<th>` cells, which is invalid table markup; one `linear-gradient` declaration is malformed.
- **Moon Orbit:** the keyframes contain invalid `translate: (-50%, -50%)` declarations. The rotation still runs, but the intended translation is lost.

### Repository-wide observations

- **Images:** 0 images are missing an `alt` attribute across all 59 pages. Alt quality still varies; the Travel Agency page uses values such as "Picture1".
- **Viewport metadata:** 57 of 59 pages include it. Cat Painting and Nutritional Label do not.
- **New-tab links:** 23 links use `target="_blank"`. Seventeen have no `rel` attribute, and six use only `noreferrer`.
- **Duplicate IDs:** the practice portfolio is the only page with duplicate IDs.
- **Scripts:** there are 0 JavaScript files and 0 inline event handlers.
- **Assets:** most images, fonts, icons, audio, and video come from remote services. The only local image is the portrait in `Personal Portfolio/`.
- **Build and testing:** there is no package manifest, build system, test suite, CI configuration, or formatter configuration.
- **License:** no license file is present. Do not assume the repository is open source for reuse.
- **Privacy:** `Personal Portfolio/` contains a portrait and contact-style details that look personal. The values are intentionally not reproduced in this documentation. Review and redact that folder before publishing or reusing it.

## Future goals

These are learning goals, not promises about the current state:

- Complete the House Painting and Contact Form exercises.
- Fix the Quiz stylesheet filename and the Book Inventory table structure and selectors.
- Correct the invalid table markup and gradient in the Balance Sheet.
- Add the viewport meta tag to the Cat Painting and Nutritional Label.
- Add `rel="noopener noreferrer"` to new-tab links that lack a `rel`.
- Add reduced-motion rules to the animation projects.
- Add a mobile breakpoint to the Newspaper Layout and review the standalone portfolio's narrow-screen behaviour.
- Continue adding small, readable practice pages that demonstrate one concept at a time.
- Keep the documentation's status labels and file paths accurate as the repository grows.

## Acknowledgements

- **[freeCodeCamp](https://www.freecodecamp.org/)** for the Responsive Web Design curriculum and the practice-project briefs that shaped these exercises. The original exercise files remain the work of their authors and are used here as learning records.
- **[MDN Web Docs](https://developer.mozilla.org/)** for the HTML, CSS, and accessibility reference material that supports the explanations.
- **Asabeneh Yetayeh's [30 Days of JavaScript](https://github.com/Asabeneh/30-Days-Of-JavaScript)** for inspiration for the teaching philosophy: short chapters, objectives, examples, exercises, and a clear next step. No content, wording, layout, or branding from that project is copied here.
- **Google Fonts, Font Awesome, freeCodeCamp's CDN, and YouTube** for assets used by individual practice pages.

## License

No license file is included in this repository, so no reuse license is granted by default. The practice pages may reference third-party assets and project briefs with their own terms. If you want to reuse the documentation or code, add an explicit license and review the third-party material first.
