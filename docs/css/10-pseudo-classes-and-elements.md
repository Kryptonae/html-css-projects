# 10. Pseudo-Classes and Pseudo-Elements

## A. Introduction

Pseudo-classes select an element based on a state or position: hovered, focused, visited, checked, invalid, first in a list, targeted by a URL. Pseudo-elements select or create a part of an element: the first letter, the placeholder text, or a generated box before or after the content.

These selectors let CSS respond to interaction and structure without adding classes to every element. They also make it easy to create effects that are invisible to keyboard users or to generated content that assistive technology cannot see. The repository has several careful examples and several useful warnings.

> **Code conventions:** A code block followed by a **Source:** link is a repository example taken from that file; the excerpt may leave out unrelated markup, and the link opens the complete source. A block without a source link is a teaching example — either a generic syntax illustration or a shortened or adapted excerpt named in the surrounding prose. Section H contains new practice tasks, not requirements from the original freeCodeCamp exercises. The original HTML and CSS files are not modified by this course.

## B. Learning objectives

By the end of this chapter you should be able to:

- Style link states with `:link`, `:visited`, `:hover`, `:active`, and `:focus`.
- Use `:focus`, `:valid`, `:invalid`, and `:checked` for form feedback.
- Use `:target` to reveal a section linked from the same page.
- Use `:not()` to exclude elements from a rule.
- Use `:first-of-type`, `:last-of-type`, and `:nth-of-type()`.
- Create generated content with `::before` and `::after`.
- Style `::first-letter` and `::placeholder`.
- Avoid pseudo-element and generated-content accessibility traps.

## C. Core concepts

### Link states

```css
a:link {
  color: saddlebrown;
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

a:focus {
  outline: 2px solid blue;
}
```

- `:link` matches an unvisited link.
- `:visited` matches a visited link. Browsers restrict which properties can be styled for privacy.
- `:hover` matches while the pointer is over the element.
- `:active` matches while the element is being activated, usually during a mouse press.
- `:focus` matches when the element has keyboard or programmatic focus.

The order matters. A common mnemonic is **LVHA**: link, visited, hover, active. The To-Do List adds `:focus` and follows the same idea.

Hover is not a substitute for focus. A keyboard user never hovers. Always provide a focus style.

### Form states

```css
input:focus,
textarea:focus {
  border: 2px solid gold;
  outline: none;
}

input:invalid,
textarea:invalid,
select:invalid {
  border: 1px solid red;
}

input:valid,
textarea:valid,
select:valid {
  border: 2px solid green;
}
```

The Job Application Form uses these rules to give immediate visual feedback. There is a caveat: `:invalid` can match an empty required field before the user has interacted with it, which may make the form look wrong on first load. `:user-invalid` and `:user-valid` are newer alternatives with better timing, but browser support should be checked.

### :checked and custom controls

```css
.contact-method-radio-btn {
  appearance: none;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  border: 2px solid gray;
  vertical-align: bottom;
}

.contact-method-radio-btn::before {
  display: block;
  content: " ";
  width: 10px;
  height: 10px;
  border-radius: 50%;
  transform: translate(3px, 3px) scale(0);
  transition: all 0.3s ease-in;
}

.contact-method-radio-btn:checked::before {
  transform: translate(3px, 3px) scale(1);
  background-color: lightgreen;
}
```

`appearance: none` removes the browser's native radio button. The `::before` pseudo-element becomes the visible dot, and `:checked` scales it into view. The input remains a real radio button for keyboard and form submission.

### :target

The Greeting Card uses the URL fragment to show a section:

```css
section {
  display: none;
}

section:target {
  display: block;
}
```

When the visitor clicks a link to `#send`, the section with `id="send"` becomes the target and `:target` matches. This is a CSS-only interaction. It has no JavaScript and no server request.

The hidden sections are removed from the accessibility tree while `display: none` applies. That is acceptable here because the content is a confirmation message, but it would be a problem if the hidden section contained the page's only navigation.

### :not()

`:not()` excludes elements that match a selector:

```css
label:not(.contact-method) {
  display: block;
  margin: 10px 0;
}

input:not(.contact-method-radio-btn),
textarea {
  background-color: #ffffff1a;
  width: 95%;
  border: 1px solid gray;
  border-radius: 5px;
  padding: 10px;
}
```

The first rule makes almost every label a block, except the labels that use the `contact-method` class. The second styles text-like inputs and textareas, but not the custom radio buttons. `:not()` keeps the HTML class list smaller.

### Structural pseudo-classes

```css
h1 .flex span:first-of-type {
  font-size: 0.7em;
}

h1 .flex span:last-of-type {
  font-size: 1.2em;
}

tr.total td:nth-of-type(3) {
  border-bottom: 4px double #0a0a23;
  font-weight: bold;
}
```

- `:first-of-type` matches the first sibling of its element type.
- `:last-of-type` matches the last sibling of its element type.
- `:nth-of-type(3)` matches the third sibling of its element type.

These are not the same as `:first-child` or `:nth-child()`, which count all siblings regardless of type.

### Pseudo-elements

```css
h1::before {
  content: "🥳 ";
}

h1::after {
  content: " 🥳";
}

.text::first-letter {
  font-size: 2em;
  font-weight: bold;
}
```

- `::before` creates a generated box before the element's content.
- `::after` creates one after the content.
- `::first-letter` styles the first letter of a block.
- `::placeholder` styles placeholder text.
- `::selection` styles selected text.

Pseudo-elements use double colons in modern CSS. Single-colon forms such as `:before` still work for compatibility, but the double-colon form distinguishes pseudo-elements from pseudo-classes.

Generated content is not in the DOM. A screen reader may or may not announce it, so do not put essential information only in `content`. The Magazine uses quotes around a block quote:

```css
.quote::before {
  content: '" ';
}

.quote::after {
  content: ' "';
}
```

That is decorative punctuation. The quoted text itself is real content.

### Pseudo-elements and replaced elements

Pseudo-elements do not reliably work on replaced elements such as `<img>`, `<input>`, `<video>`, and `<iframe>`. A `::before` on an `<input>` is not a portable way to add an icon. Use a wrapper element or a background image instead.

## D. Syntax

```css
/* Pseudo-class */
a:hover { }
input:focus { }
li:nth-child(2) { }

/* Pseudo-element */
p::first-line { }
.quote::before { content: "“"; }
input::placeholder { color: gray; }

/* Functional pseudo-class */
:not(.excluded) { }
:nth-of-type(2) { }
```

## E. Code examples

### Example 1: A CSS-only card reveal

```css
section {
  margin: 20px auto;
  max-width: 600px;
  background-color: whitesmoke;
  padding: 20px;
  border-radius: 10px;
  display: none;
}

section:hover {
  transform: skewX(10deg);
}

section:target {
  display: block;
}
```

Source: [`CSS/Pseudo Classes and Elements/Design a Greeting Card/style.css`](<../../CSS/Pseudo%20Classes%20and%20Elements/Design%20a%20Greeting%20Card/style.css>). Status: **Implemented**.

The `section:hover` rule can only apply when the section is visible. The `:target` rule is the one that reveals it. The skew on hover is a separate visual effect.

### Example 2: A custom radio button

```css
.contact-method-radio-btn {
  appearance: none;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  border: 2px solid gray;
  vertical-align: bottom;
}

.contact-method-radio-btn::before {
  display: block;
  content: " ";
  width: 10px;
  height: 10px;
  border-radius: 50%;
  transform: translate(3px, 3px) scale(0);
  transition: all 0.3s ease-in;
}

.contact-method-radio-btn:checked::before {
  transform: translate(3px, 3px) scale(1);
  background-color: lightgreen;
}
```

Source: [`CSS/Pseudo Classes and Elements/Design a Parent Teacher Conference Form/style.css`](<../../CSS/Pseudo%20Classes%20and%20Elements/Design%20a%20Parent%20Teacher%20Conference%20Form/style.css>). Status: **Implemented**.

The input is still focusable and still submits a value. The custom dot is visual only. This is a good pattern as long as the focus state is also visible; the stylesheet does not define one for the radio, so a keyboard user may not see where focus is.

### Example 3: Validation states

```css
input:focus,
textarea:focus {
  border: 2px solid gold;
  outline: none;
}

input:invalid,
textarea:invalid,
select:invalid {
  border: 1px solid red;
}

input:valid,
textarea:valid,
select:valid {
  border: 2px solid green;
}
```

Source: [`CSS/Pseudo Classes and Elements/Build a Job Application Form/style.css`](<../../CSS/Pseudo%20Classes%20and%20Elements/Build%20a%20Job%20Application%20Form/style.css>). Status: **Implemented**.

The focus rule removes the native outline and replaces it with a gold border. That can work, but the border must remain visible against the background. The valid/invalid colours are not the only signal because the border style also changes, but text feedback would be clearer.

### Example 4: Link states

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

Source: [`CSS/Basic CSS/Build a Stylized To-Do List/style.css`](<../../CSS/Basic%20CSS/Build%20a%20Stylized%20To-Do%20List/style.css>). Status: **Implemented**.

This is a compact demonstration of all five states. The focus outline is the accessibility-critical rule.

### Example 5: First and last of type

```css
h1 .flex span:first-of-type {
  font-size: 0.7em;
}

h1 .flex span:last-of-type {
  font-size: 1.2em;
}

tr.total td:nth-of-type(3) {
  border-bottom: 4px double #0a0a23;
  font-weight: bold;
}
```

Source: [`CSS/Attribute Selectors/Build a Balance Sheet/styles.css`](<../../CSS/Attribute%20Selectors/Build%20a%20Balance%20Sheet/styles.css>). Status: **Implemented\***.

The first rule makes the company name smaller than the "Balance Sheet" label. The `:nth-of-type(3)` rule emphasizes the current year column. Structural selectors keep the HTML free of extra classes, but they depend on the element order remaining stable.

## F. Step-by-step explanation

1. **Decide whether you are selecting a state or a part.** Use a pseudo-class for state and a pseudo-element for a part.
2. **Provide all relevant link states.** At minimum, style `:focus` and `:hover`; do not rely on colour alone.
3. **Test with the keyboard.** Tab through the page and confirm that focus is visible.
4. **Use `:checked` on a real form control.** Do not hide the input and replace it with a div.
5. **Use `:target` for in-page reveals.** Make sure the hidden content is not the only way to access essential information.
6. **Use `:not()` to exclude exceptions.** Keep the selector readable.
7. **Use structural selectors carefully.** They break when the element order changes.
8. **Keep generated content decorative.** Put essential text in the HTML.
9. **Check pseudo-elements on replaced elements.** They may not render.
10. **Test in more than one browser.** Form-state support and `appearance` can vary.

## G. Repository implementations

| Implementation | Pseudo feature | Status | Source |
| --- | --- | --- | --- |
| Greeting Card | `:hover`, `:target`, `::before`, `::after`, link states | Implemented | [Open](<../../CSS/Pseudo Classes and Elements/Design a Greeting Card/index.html>) |
| Parent Teacher Form | `:not()`, `appearance: none`, `:checked`, `::before` | Implemented | [Open](<../../CSS/Pseudo Classes and Elements/Design a Parent Teacher Conference Form/index.html>) |
| Job Application Form | `:focus`, `:valid`, `:invalid`, `:not()` | Implemented | [Open](<../../CSS/Pseudo Classes and Elements/Build a Job Application Form/index.html>) |
| To-Do List | Five link states including `:focus` | Implemented | [Open](<../../CSS/Basic CSS/Build a Stylized To-Do List/index.html>) |
| Balance Sheet | `:first-of-type`, `:last-of-type`, `:nth-of-type()` | Implemented\* | [Open](<../../CSS/Attribute Selectors/Build a Balance Sheet/index.html>) |
| Magazine | `::first-letter`, `::before`, `::after` | Implemented | [Open](<../../CSS/Grid/Build a Magazine/index.html>) |
| Quiz Webpage | `:hover` navigation and a screen-reader utility | Link issue | [Open](<../../CSS/Accessibility/Build a Quiz Webpage, Not started W/index.html>) |

## H. Additional challenges

These are new practice tasks for this course; they are not requirements from the original exercises.

1. Add a visible `:focus` style to the Parent Teacher radio buttons.
2. Build a CSS-only tab interface with `:target`. Check whether the hidden panels are reachable by keyboard.
3. Create a custom checkbox with `appearance: none` and `:checked::before`.
4. Style a form with `:valid` and `:invalid`, then add text feedback so colour is not the only signal.
5. Use `:not()` to style all paragraphs except the first one.
6. Add a decorative `::before` to a heading. Confirm that the generated content is not the only place the information appears.
7. Use `:nth-of-type()` to stripe alternate table rows. Test what happens when a row is added.
8. Compare `:first-child` and `:first-of-type` on a container with mixed element types.

## I. Common mistakes

- **Styling `:hover` but not `:focus`.** Keyboard users lose the feedback.
- **Removing outlines without a replacement.** Focus becomes invisible.
- **Relying on colour alone for validation.** Add text or an icon.
- **Using `:invalid` before the user has interacted.** The form may look broken on load.
- **Hiding a real input and replacing it with a div.** The result may not be keyboard-accessible or submittable.
- **Putting essential content in `::before` or `::after`.** Generated content is not reliable for assistive technology.
- **Using `:first-child` when you mean `:first-of-type`.** They count different siblings.
- **Using a pseudo-element on an `<img>` or `<input>`.** It may not render.
- **Forgetting that `:visited` styles are restricted.** Some properties will not apply.
- **Assuming `:target` is persistent.** It changes when the URL fragment changes.

## J. Summary

Pseudo-classes style states and positions: links, focus, validation, checked controls, targets, and structural positions. Pseudo-elements style or generate parts: first letter, placeholder, and before/after boxes. They reduce the need for extra classes and enable CSS-only interactions.

The Greeting Card and Parent Teacher form show the creative side. The To-Do List and Job Application form show the accessibility-critical side: focus and validation must remain visible and understandable. Generated content should enhance real HTML, not replace it.

## K. Next module

Continue to [11. Transitions and Animations](11-transitions-and-animations.md) to move from state changes to smooth motion and keyframe animation.
