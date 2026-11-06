# 02. Selectors and Specificity

## A. Introduction

A CSS rule only works if its selector matches the element you intended. Selectors range from broad (`p`) to precise (`.menu .item p.price`), and the browser uses specificity to decide which rule wins when several match.

This chapter builds a selector vocabulary and then connects it to the cascade. The Balance Sheet is a useful case study because it uses attribute selectors for both a screen-reader utility and table styling. The Registration Form shows the common `input[type="submit"]` pattern. Neither example relies on JavaScript.

> **Code conventions:** A code block followed by a **Source:** link is a repository example taken from that file; the excerpt may leave out unrelated markup, and the link opens the complete source. A block without a source link is a teaching example — either a generic syntax illustration or a shortened or adapted excerpt named in the surrounding prose. Section H contains new practice tasks, not requirements from the original freeCodeCamp exercises. The original HTML and CSS files are not modified by this course.

## B. Learning objectives

By the end of this chapter you should be able to:

- Use type, class, ID, universal, descendant, child, grouping, and attribute selectors.
- Calculate a selector's specificity in the `(id, class, type)` format.
- Predict which of two matching rules wins.
- Explain when an ID selector is appropriate and when a class is better.
- Use attribute selectors such as `[type="submit"]` and `[class~="read"]`.
- Recognise intentional and accidental `!important` usage.
- Read a stylesheet and identify the selector strategy behind it.

## C. Core concepts

### Type selectors

A type selector targets an element name:

```css
body {
  background-color: lightgray;
}

h1 {
  text-align: center;
}
```

Type selectors are broad. They are useful for base styles and resets.

### Class selectors

A class selector starts with a dot:

```css
.menu {
  width: 80%;
  background-color: burlywood;
}
```

It matches every element with `class="menu"`. Classes are the default choice for reusable component styles because one element can have several classes and a class can be reused many times.

### ID selectors

An ID selector starts with `#`:

```css
#email {
  padding: 50px;
  margin: 50px auto;
  width: 500px;
}
```

It matches the element with `id="email"`. IDs must be unique in a document. They are useful for one-off landmarks and for anchor targets. Because they are highly specific, using them for ordinary styling can make later overrides difficult.

### Universal selector

The universal selector matches every element:

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
```

It has zero specificity, but because it matches everything it is often used in resets. A more targeted reset is:

```css
*,
*::before,
*::after {
  box-sizing: border-box;
}
```

### Grouping selectors

A comma groups selectors that share declarations:

```css
h1,
h2,
p {
  text-align: center;
}
```

Each selector in the list is matched independently. The rule is equivalent to three separate rules with the same declarations.

### Descendant and child selectors

A descendant selector uses a space:

```css
.item p {
  font-size: 18px;
}
```

It matches any `<p>` inside an element with `class="item"`, at any depth.

A child selector uses `>`:

```css
nav > ul {
  display: flex;
}
```

It matches only a `<ul>` that is a direct child of `<nav>`. The Quiz stylesheet uses this pattern for its navigation.

### Attribute selectors

Attribute selectors match elements based on attributes:

```css
input[type="submit"] {
  display: block;
  width: 60%;
}

span[class~="sr-only"] {
  position: absolute;
}

tr[class="total"] {
  border-bottom: 4px double #0a0a23;
  font-weight: bold;
}

#years span[class] {
  font-weight: bold;
}
```

- `[type="submit"]` matches an exact attribute value.
- `[class~="sr-only"]` matches a whitespace-separated word in the class list. It is useful when an element has several classes.
- `[class="total"]` matches the complete class attribute exactly. It will not match `class="total current"`.
- `[class]` matches any element that has a `class` attribute, regardless of its value.

The Balance Sheet uses `span[class~="sr-only"]` because the utility may be combined with another class. It uses `tr[class="total"]` and `th[class="total"]` for exact class matches. The mix is intentional but worth noticing: changing the class list on a total row could stop the exact selector from matching.

### Specificity

Specificity is usually written as three numbers:

| Selector type | Example | Specificity |
| --- | --- | --- |
| ID | `#email` | `(1, 0, 0)` |
| Class, attribute, pseudo-class | `.menu`, `[type="submit"]`, `:hover` | `(0, 1, 0)` |
| Type, pseudo-element | `p`, `::before` | `(0, 0, 1)` |
| Universal | `*` | `(0, 0, 0)` |

The universal selector and combinators such as `>` and a space do not add specificity. The comma does not add specificity either; each selector in a group is evaluated separately.

Compare:

```css
p {
  color: black;
}

.menu p {
  color: brown;
}

#email p {
  color: red;
}
```

For a paragraph inside both `.menu` and `#email`, the ID rule wins: `(1, 0, 1)` is more specific than `(0, 1, 1)` and `(0, 0, 1)`.

### Source order

If two rules have the same specificity, the later one wins:

```css
.card {
  background-color: white;
}

.card {
  background-color: whitesmoke;
}
```

The card is whitesmoke. If the order is reversed, it is white. When debugging, check the order as well as the specificity.

### !important

`!important` raises a declaration above normal declarations:

```css
span[class~="sr-only"] {
  border: 0 !important;
  clip: rect(1px, 1px, 1px, 1px) !important;
  height: 1px !important;
  width: 1px !important;
}
```

The Balance Sheet repeats `!important` on the utility because it must override other styles. In ordinary component code, `!important` often hides a selector problem. Use it deliberately, not as a default fix.

### Inline styles

A `style=""` attribute has higher priority than an external stylesheet rule, but it can still be overridden by `!important`. The repository uses external stylesheets and does not rely on inline styles for its main layouts.

## D. Syntax

```css
/* Type */
p { }

/* Class */
.card { }

/* ID */
#email { }

/* Universal */
* { }

/* Group */
h1, h2, p { }

/* Descendant */
.item p { }

/* Child */
nav > ul { }

/* Attribute */
input[type="submit"] { }
span[class~="read"] { }
```

## E. Code examples

### Example 1: The screen-reader utility selector

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

The `~=` operator matches `sr-only` as one word in the class list. This works even if an element later becomes `class="sr-only year"`.

### Example 2: Exact class attribute matching

```css
tr[class="total"] {
  border-bottom: 4px double #0a0a23;
  font-weight: bold;
}

th[class="total"] {
  border-bottom: 4px double #0a0a23;
  font-weight: bold;
}

tr.total td:nth-of-type(3) {
  border-bottom: 4px double #0a0a23;
  font-weight: bold;
}
```

Source: [`CSS/Attribute Selectors/Build a Balance Sheet/styles.css`](<../../CSS/Attribute Selectors/Build a Balance Sheet/styles.css>). Status: **Implemented\***.

`tr[class="total"]` and `tr.total` both target the same class, but they are not identical selectors. The attribute form requires the class attribute to be exactly `"total"`. The class form is usually more flexible because it still matches when another class is added.

### Example 3: Attribute selector on a form control

```css
input[type="submit"] {
  display: block;
  width: 60%;
  margin: 1em auto;
  height: 2em;
  font-size: 1.1rem;
  background-color: #3b3b4f;
  border-color: white;
  min-width: 300px;
}
```

Source: [`CSS/Styling Forms/Design a Registration Form/style.css`](<../../CSS/Styling Forms/Design a Registration Form/style.css>). Status: **Implemented**.

This rule targets only submit inputs, not text, email, or file inputs. It is more precise than styling every `<input>`.

### Example 4: A descendant selector in a card list

```css
.item p {
  display: inline-block;
  margin-top: 5px;
  margin-bottom: 5px;
  font-size: 18px;
}
```

Source: [`CSS/Basic CSS/Design a Cafe Menu/style.css`](<../../CSS/Basic CSS/Design a Cafe Menu/style.css>). Status: **Implemented**.

Only paragraphs inside an element with `class="item"` are affected. The heading rules and footer rules are outside that scope.

### Example 5: A child selector in navigation

```css
nav > ul {
  display: flex;
  justify-content: space-evenly;
  flex-wrap: wrap;
  align-items: center;
  padding-inline-start: 0;
  margin-block: 0;
  height: 100%;
}
```

Source: [`CSS/Accessibility/Build a Quiz Webpage, Not started W/style.css`](<../../CSS/Accessibility/Build a Quiz Webpage, Not started W/style.css>). Status: **Link issue**. The stylesheet exists, but the HTML requests `styles.css` instead of `style.css`, so this rule does not load when the page is opened.

## F. Step-by-step explanation

1. **Start broad.** Use type selectors for base styles.
2. **Add reusable classes.** Give components a class rather than an ID.
3. **Narrow with context.** Use a descendant selector when a rule should apply only inside a component.
4. **Use a child selector when depth matters.** It prevents rules from leaking into nested structures.
5. **Use attribute selectors for states and input types.** They keep the HTML class list shorter.
6. **Keep specificity low.** A flat class-based stylesheet is easier to override later.
7. **Calculate specificity when a rule loses.** Write the three numbers for each conflicting selector.
8. **Check source order.** If the numbers are equal, the later declaration wins.
9. **Avoid `!important` unless the rule genuinely must win.** Prefer a better selector.
10. **Test with the inspector.** It shows the winning declaration and the overridden ones.

## G. Repository implementations

| Implementation | Selector feature | Status | Source |
| --- | --- | --- | --- |
| Cafe Menu | Class selectors, grouped selectors, descendant selector | Implemented | [Open](<../../CSS/Basic CSS/Design a Cafe Menu/index.html>) |
| Balance Sheet | `[class~="..."]`, exact class attributes, `:nth-of-type` | Implemented\* | [Open](<../../CSS/Attribute Selectors/Build a Balance Sheet/index.html>) |
| Registration Form | `input[type="submit"]`, `input[type="file"]`, `:last-of-type` | Implemented | [Open](<../../CSS/Styling Forms/Design a Registration Form/index.html>) |
| To-Do List | Class selectors plus link pseudo-classes | Implemented | [Open](<../../CSS/Basic CSS/Build a Stylized To-Do List/index.html>) |
| Book Inventory App | Attribute selectors for classes and status styling | Partial | [Open](<../../CSS/Attribute Selectors/Build a Book Inventory App [CERTIFICATE]/index.html>) |
| Quiz Webpage | Child combinators in navigation | Link issue | [Open](<../../CSS/Accessibility/Build a Quiz Webpage, Not started W/index.html>) |

The Book Inventory stylesheet targets `span[class~="read"]`, `span[class~="to-read"]`, and `span[class~="in-progress"]`, but the status spans in the HTML use `class="status"`. Those selectors do not match the visible status text. The page also has a missing `</tr>` near the end of the table. That is why it is labelled **Partial** rather than fully implemented.

## H. Additional challenges

These are new practice tasks for this course; they are not requirements from the original exercises.

1. Write three selectors for the same paragraph: a type selector, a class selector, and an ID selector. Predict the winner before testing.
2. Change `tr[class="total"]` to `tr.total` in a copy of the Balance Sheet. Add a second class to the total row and observe which version still matches.
3. Build a form with text, email, and submit inputs. Style only the submit input with an attribute selector.
4. Create a navigation list with a nested submenu. Use `>` to style only the top-level items.
5. Write a selector with specificity `(0, 2, 1)` and another with `(0, 1, 3)`. Which wins?
6. Find a rule in the repository that uses `!important`. Decide whether it is justified.
7. Use the browser inspector to find one rule that is being overridden. Identify the winning selector and its specificity.
8. Fix the Book Inventory status selectors by changing the HTML class names to match the CSS, or by changing the CSS to target `.status`. Explain the trade-off.

## I. Common mistakes

- **Using an ID when a class would do.** IDs are hard to reuse and hard to override.
- **Reusing an ID.** IDs must be unique.
- **Thinking a comma creates one selector with combined specificity.** Each selector in a group is evaluated separately.
- **Confusing `[class="total"]` with `.total`.** The attribute form requires an exact attribute value.
- **Forgetting that `~=` matches a word, not a substring.** `[class~="read"]` does not match `"to-read"`.
- **Assuming the last rule always wins.** Specificity may override order.
- **Using `!important` everywhere.** It makes future overrides harder.
- **Styling with deeply nested selectors.** They are brittle and highly specific.
- **Forgetting that a stylesheet link can point to the wrong filename.** The Quiz project is the repository example.
- **Expecting CSS to fix broken HTML.** A missing closing tag can change the tree and therefore the selector matches.

## J. Summary

Selectors choose elements. Type selectors are broad, classes are reusable, IDs are unique and highly specific, and attribute selectors target values and states. Descendant and child combinators add structural precision. Specificity decides conflicts, with IDs beating classes and classes beating type selectors; source order breaks ties.

The Balance Sheet demonstrates attribute selectors and intentional `!important` usage. The Registration Form shows a clean input-type selector. The Book Inventory App shows what happens when selectors and markup drift apart. The next step is to use selectors to control colour, type, and spacing.

## K. Next module

Continue to [03. Colours and Typography](03-colors-and-typography.md) to apply colour formats, gradients, font stacks, and type scales.
