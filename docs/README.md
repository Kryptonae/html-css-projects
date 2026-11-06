# HTML & CSS Course Map

This folder contains the teaching material for the repository. The root [README](../README.md) is the learning portal; the pages here are the chapters you work through.

The course is topic-based, not day-based. You can follow the HTML track from start to finish, work through the CSS track, or jump directly to a topic you need to revise. Every chapter follows the same teaching pattern:

**Understand → Learn → See examples → Practise → Build → Revise**

## How to use the course

1. Read the chapter introduction and learning objectives.
2. Study the concept and syntax sections.
3. Read the repository examples with the linked source files open beside them.
4. Try the additional challenges in the chapter.
5. Open the linked exercises and projects to see the same ideas in a real page.
6. Use the chapter summary for revision, then continue to the next module.

A code block followed by a **Source:** link is a repository example taken from that file; the excerpt may leave out unrelated markup, and the link opens the complete source. A block without a source link is a teaching example: either a generic syntax illustration or a shortened or adapted excerpt named in the surrounding prose. Challenges in section H are new practice tasks, not requirements from the original freeCodeCamp exercises.

## Status labels

The repository is a learning archive, so not every folder is finished. These labels describe what the source files actually contain:

| Label | Meaning |
| --- | --- |
| **Implemented** | The page and its stylesheet (where one is expected) are complete enough to study and run. |
| **Implemented\*** | The page works, but the source has a documented caveat such as invalid markup, a stale link, duplicate IDs, or a missing viewport meta tag. |
| **Partial** | The main structure exists, but an important part is broken or incomplete. |
| **Link issue** | A stylesheet exists, but the HTML points to a different filename, so the page loads unstyled. |
| **Placeholder** | The page body or stylesheet is effectively empty. |
| **HTML-only** | A complete HTML exercise with no CSS by design. |

These are source-inspection labels, not visual quality scores. They tell you what to expect before you open a folder.

## HTML track

| Chapter | Focus | Start here |
| --- | --- | --- |
| [01. HTML Fundamentals](html/01-html-fundamentals.md) | Document structure, metadata, landmarks, nesting | Travel Agency, Cat Photo App |
| [02. Text, Links, and Images](html/02-text-links-and-images.md) | Headings, paragraphs, quotations, links, figures, alt text | Cat Photo App, Quincy's Tips, Cat Blog |
| [03. Lists and Tables](html/03-lists-and-tables.md) | `ul`, `ol`, `dl`, tables, captions, `scope`, spans | To-Do List, Tech Conference, Book Catalog |
| [04. Forms and Inputs](html/04-forms-and-inputs.md) | Labels, input types, fieldsets, validation, form structure | Hotel Feedback, Survey Form, Registration Form |
| [05. Semantic HTML](html/05-semantic-html.md) | `header`, `nav`, `main`, `section`, `article`, `footer` | Event Hub, Cat Blog, Technical Documentation |
| [06. Accessibility](html/06-accessibility.md) | Labels, alt text, table scope, ARIA, focus, link safety | Donation Form, Quiz, Balance Sheet |
| [07. Multimedia and SVG](html/07-multimedia-and-svg.md) | `video`, `audio`, `iframe`, inline SVG, image loading | Video Player, Music Player, Heart Icon |

## CSS track

| Chapter | Focus | Start here |
| --- | --- | --- |
| [01. CSS Fundamentals](css/01-css-fundamentals.md) | Linking CSS, rule syntax, cascade, inheritance, resets | Cafe Menu, Confidential Email |
| [02. Selectors and Specificity](css/02-selectors-and-specificity.md) | Type, class, ID, descendant, child, attribute, specificity | Balance Sheet, Registration Form |
| [03. Colours and Typography](css/03-colors-and-typography.md) | Colour formats, gradients, font stacks, type scales | Colored Markers, Newspaper Article |
| [04. Box Model and Units](css/04-box-model-and-units.md) | Content, padding, border, margin, `box-sizing`, units | Confidential Email, Event Flyer |
| [05. Display and Positioning](css/05-display-and-positioning.md) | Normal flow, `display`, `position`, `z-index`, floats | Cat Painting, Piano, Balance Sheet |
| [06. Flexbox](css/06-flexbox.md) | Axes, wrapping, alignment, growing and shrinking | Photo Gallery, Colorful Boxes |
| [07. CSS Grid](css/07-css-grid.md) | Tracks, `fr`, `minmax`, named areas, nested grids | Magazine, Newspaper Layout |
| [08. Responsive Design](css/08-responsive-design.md) | Fluid sizes, media queries, breakpoints, `min()`/`max()` | Piano, Product Landing Page |
| [09. CSS Custom Properties](css/09-css-custom-properties.md) | `--tokens`, `var()`, scoping, theme changes | City Skyline, Availability Table |
| [10. Pseudo-Classes and Pseudo-Elements](css/10-pseudo-classes-and-elements.md) | Link states, `:focus`, `:target`, `:checked`, `::before` | Greeting Card, Parent Teacher Form |
| [11. Transitions and Animations](css/11-transitions-and-animations.md) | `transition`, `transform`, `@keyframes`, reduced motion | Ferris Wheel, Flappy Penguin |
| [12. CSS Art](css/12-css-art.md) | Drawing with borders, gradients, shadows, and transforms | Cat Painting, Rothko Painting |

## Projects

The [Projects Guide](projects/projects-guide.md) profiles 16 larger or concept-rich projects. It explains what each one demonstrates, how to study it, and any source-level issues worth noticing.

For the complete list of every exercise and project, use the directory in the root [README](../README.md#complete-exercise-and-project-directory).

## A note on experimentation

You are encouraged to edit copies of these files, change values, break layouts, and fix them again. The original HTML and CSS files are preserved as learning records; the documentation does not modify them.
