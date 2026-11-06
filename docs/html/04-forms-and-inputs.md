# 04. Forms and Inputs

## A. Introduction

A form is how a web page asks the visitor for information. The HTML form elements define the fields, the labels, the groups, and the basic validation rules. A server or a client-side script handles the data after submission, but this repository has no JavaScript and no backend, so the forms are markup practice.

The most important beginner lesson is not "add an `<input>`". It is "make every field understandable and every control reachable". A label that is visually nearby but not programmatically connected, a required field without `required`, or a radio group with the wrong `name` can make an otherwise attractive form fail.

> **Code conventions:** A code block followed by a **Source:** link is a repository example taken from that file; the excerpt may leave out unrelated markup, and the link opens the complete source. A block without a source link is a teaching example — either a generic syntax illustration or a shortened or adapted excerpt named in the surrounding prose. Section H contains new practice tasks, not requirements from the original freeCodeCamp exercises. The original HTML and CSS files are not modified by this course.

## B. Learning objectives

By the end of this chapter you should be able to:

- Connect a `<label>` to an input with matching `for` and `id` values.
- Use text, email, number, radio, checkbox, select, textarea, and submit controls.
- Group related fields with `<fieldset>` and `<legend>`.
- Explain the difference between the `name` and `id` attributes.
- Apply `required`, `min`, `max`, `minlength`, `maxlength`, and `pattern`.
- Build a form that uses `action` and `method`.
- Identify broken label associations and missing validation in the repository.

## C. Core concepts

### The form element

```html
<form action="https://hotel-feedback.freecodecamp.org" method="POST">
  <!-- fields -->
</form>
```

- `action` is the URL that receives the submission.
- `method="POST"` sends the data in the request body. `method="get"` would append it to the URL.
- A submit button triggers the submission.

The action in the Hotel Feedback form points to a freeCodeCamp practice endpoint. The form is not connected to a real hotel system.

### Labels and the for/id relationship

A label should be connected to its control:

```html
<label for="full-name">Name (required):</label>
<input
  type="text"
  name="name"
  id="full-name"
  placeholder="e.g., John Doe"
  required
/>
```

The label's `for` value matches the input's `id`. Clicking the label focuses the input, and a screen reader announces the label with the field.

`name` is different from `id`:

- `id` identifies the element in the document and connects it to a label.
- `name` is the key sent with the form data.

An input can have both, and usually should:

```html
<input type="email" name="email" id="email" />
```

### Input types

The `type` attribute changes the control and the browser's validation behaviour:

```html
<input type="text" name="name" id="name" />
<input type="email" name="email" id="email" />
<input type="number" name="age" id="age" min="3" max="100" />
<input type="checkbox" name="choice" id="ads" value="ads" />
<input type="radio" name="hotel-stay" id="yes-option" value="yes" />
<input type="submit" value="Send" />
```

An email input does not guarantee that the address exists, but it does let the browser reject obviously malformed values. A number input with `min` and `max` can reject values outside the range.

### Radio buttons and checkboxes

Radio buttons are mutually exclusive when they share the same `name`:

```html
<input type="radio" name="hotel-stay" id="yes-option" value="yes" />
<label for="yes-option">Yes</label>
<input type="radio" name="hotel-stay" id="no-option" value="no" />
<label for="no-option">No</label>
```

Selecting "No" deselects "Yes" because both controls belong to the `hotel-stay` group.

Checkboxes allow more than one selection. They can share a `name` when the server expects an array of values, and each checkbox has its own `id`/`value` pair:

```html
<input type="checkbox" name="choice" id="ads" value="ads" />
<label for="ads">Social Media Ads</label>
<input type="checkbox" name="choice" id="location" value="location" />
<label for="location">Location</label>
```

### Fieldsets and legends

A `<fieldset>` groups related controls. Its `<legend>` gives the group a name:

```html
<fieldset>
  <legend>Was this your first time at our hotel?</legend>
  <!-- radio buttons -->
</fieldset>
```

The legend is especially useful for radio groups. A screen reader can announce the group name before reading the individual options.

### Select menus and textareas

A `<select>` provides a list of options:

```html
<label for="service">How was the service?</label>
<select name="service" id="service">
  <option value="poor">Poor</option>
  <option value="satisfactory">Satisfactory</option>
  <option value="good">Good</option>
  <option value="very-good">Very Good</option>
  <option value="excellent" selected>Excellent</option>
</select>
```

A `<textarea>` accepts multiple lines:

```html
<label for="comments">Other Comments?</label>
<textarea name="comments" id="comments" cols="30" rows="10"></textarea>
```

`cols` and `rows` set the visible size. CSS can override the size, but the textarea still needs a label.

### Validation attributes

Common built-in validation attributes:

```html
<input type="text" name="name" id="name" required minlength="2" maxlength="40" />
<input type="email" name="email" id="email" required />
<input type="number" name="age" id="age" min="3" max="100" />
```

- `required` blocks submission when the field is empty.
- `minlength` and `maxlength` limit text length.
- `min` and `max` limit numeric values.
- `pattern` accepts a regular expression for more specific text formats.

These rules run in the browser before submission. They do not replace server-side validation.

## D. Syntax

```html
<form action="/submit" method="post">
  <fieldset>
    <legend>Contact details</legend>

    <label for="name">Name</label>
    <input type="text" name="name" id="name" required />

    <label for="email">Email</label>
    <input type="email" name="email" id="email" required />

    <label for="age">Age (optional)</label>
    <input type="number" name="age" id="age" min="3" max="100" />

    <label for="comments">Comments</label>
    <textarea name="comments" id="comments" rows="5"></textarea>
  </fieldset>

  <button type="submit">Send</button>
</form>
```

A submit button can also be written as an input:

```html
<input type="submit" value="Send" />
```

Use `<button type="submit">` when the button contains HTML or when you want a clearer element. Always set `type` explicitly inside a form, because the default type of a `<button>` is `submit`.

## E. Code examples

### Example 1: A complete feedback form

This excerpt shows the label, input, fieldset, and validation pattern used by the Hotel Feedback form:

```html
<form action="https://hotel-feedback.freecodecamp.org" method="POST">
  <fieldset>
    <legend>Personal Information</legend>

    <label for="full-name">Name (required):</label>
    <input
      type="text"
      name="name"
      id="full-name"
      placeholder="e.g., John Doe"
      required
      size="20"
    />

    <label for="email">Email address (required):</label>
    <input
      type="email"
      name="email"
      id="email"
      required
      placeholder="example@email.com"
      size="20"
    />

    <label for="age">Age (optional):</label>
    <input type="number" name="age" id="age" min="3" max="100" />
  </fieldset>

  <fieldset>
    <legend>Was this your first time at our hotel?</legend>

    <input type="radio" name="hotel-stay" id="yes-option" value="yes" />
    <label for="yes-option">Yes</label>

    <input type="radio" name="hotel-stay" id="no-option" value="no" />
    <label for="no-option">No</label>
  </fieldset>

  <button type="submit">Submit</button>
</form>
```

Source: [`Hotel_Feedback_Form.html`](<../../HTML/Forms and Tables/Build a Hotel Feedback Form/Hotel_Feedback_Form.html>). Status: **HTML-only**.

The form also includes checkboxes for how the guest heard about the hotel, two select menus for ratings, and a comments textarea. It is the most complete form-lab example in the HTML folder.

### Example 2: A minimal required-field form

```html
<form>
  <label for="name">Full Name:</label>
  <input type="text" name="name" id="name" required />

  <label for="email">Email Address:</label>
  <input type="email" name="email" id="email" required />

  <label for="amount">Donation Amount ($):</label>
  <input type="number" name="amount" id="amount" required />

  <input type="checkbox" name="newsletter" id="newsletter" />
  <label for="newsletter">Subscribe</label>

  <input type="submit" value="Send" />
</form>
```

Source: [`HTML/Accessibility/Debug a Donation Form/index.html`](<../../HTML/Accessibility/Debug a Donation Form/index.html>). Status: **HTML-only**.

This form is short and every label is connected to a control. It has no `action` or `method`, so it is a markup exercise rather than a working donation flow.

### Example 3: A long survey

```html
<label for="name" id="name-label">Name</label>
<input
  type="text"
  id="name"
  name="name"
  placeholder="Enter your name"
  required
  size="20"
/>

<label for="role">Which option best describes your current role?</label>
<select name="role" id="dropdown">
  <option value="select-current-role" disabled selected>Select current role</option>
  <option value="student">Student</option>
  <option value="full-time-job">Full Time Job</option>
</select>
```

Source: [`Survey_Form.html`](<../../HTML/Forms and Tables/CERTIFICATION_PROJECT_Build a Survey Form/Survey_Form.html>). Status: **HTML-only**.

Notice the mismatch: the label says `for="role"`, but the select uses `id="dropdown"`. The label is not connected to the select. The `name` is correct, so the data would still submit, but the accessible label relationship is broken. This is exactly the kind of issue that reading the source reveals.

### Example 4: Missing required validation

```html
<label for="email">Handcrafted, home-made masterpieces</label>
<input
  type="email"
  name="email"
  id="email"
  placeholder="Enter your email address"
/>
<input type="submit" value="GET STARTED" id="submit" />
```

Source: [`CSS/CERTIFICATION PROJECTS/Build a Product Landing Page/index.html`](<../../CSS/CERTIFICATION PROJECTS/Build a Product Landing Page/index.html>). Status: **Implemented\*** as a CSS project.

The input has `type="email"`, but it does not have `required`. The browser will validate the format only if the visitor types something. An empty submission is allowed. The same page also uses a placeholder as the only hint about the field's purpose, and its label text describes the product rather than the email address. These are source-level observations, not changes made to the file.

## F. Step-by-step explanation

1. **Start with the purpose.** Decide what information the form needs and which fields are optional.
2. **Add the form element.** Set `action` and `method` if the form has a real destination.
3. **Group related controls.** Use `<fieldset>` and a `<legend>` for personal details, preferences, or ratings.
4. **Write the label first.** Connect it to the control with matching `for` and `id` values.
5. **Choose the input type.** Use `email` for email addresses, `number` for numeric values, and `checkbox` or `radio` for choices.
6. **Add a `name`.** The `name` is the key that the submitted data uses.
7. **Add validation where it helps.** Mark required fields and set reasonable ranges. Do not mark every field required just because you can.
8. **Group radio buttons with one `name`.** Give each option a unique `id` and a meaningful `value`.
9. **Add a submit control.** Use `<button type="submit">` or `<input type="submit">`.
10. **Test with the keyboard.** Tab through the form and confirm that every control receives focus in a sensible order.
11. **Test with an empty submission.** Confirm that required fields block submission and that error messages appear.
12. **Test the labels.** Click each label and confirm that the correct control receives focus.

## G. Repository implementations

| Implementation | Form features | Status | Source |
| --- | --- | --- | --- |
| Hotel Feedback Form | Fieldsets, legends, labels, text/email/number inputs, radios, checkboxes, selects, textarea | HTML-only | [Open](<../../HTML/Forms and Tables/Build a Hotel Feedback Form/Hotel_Feedback_Form.html>) |
| Survey Form | Large form with fieldsets, selects, radios, checkboxes, textarea | HTML-only | [Open](<../../HTML/Forms and Tables/CERTIFICATION_PROJECT_Build a Survey Form/Survey_Form.html>) |
| Donation Form | Minimal required fields and a newsletter checkbox | HTML-only | [Open](<../../HTML/Accessibility/Debug a Donation Form/index.html>) |
| Registration Form | HTML form paired with a full stylesheet | Implemented | [Open](<../../CSS/Styling Forms/Design a Registration Form/index.html>) |
| Product Landing Page | Email capture form with a missing `required` attribute | Implemented\* | [Open](<../../CSS/CERTIFICATION PROJECTS/Build a Product Landing Page/index.html>) |
| Contact Form | Complete form markup with an empty stylesheet | Placeholder | [Open](<../../CSS/Styling Forms/Design a Contact Form/index.html>) |

The Contact Form is a placeholder because its `style.css` is empty. The HTML form itself is present, so you can still study its markup.

## H. Additional challenges

These are new practice tasks for this course; they are not requirements from the original exercises.

1. Fix the Survey Form label by changing `for="role"` to `for="dropdown"`, or change the select's `id` to `role`. Explain which change keeps the existing CSS working.
2. Add `required` and a clear label to the Product Landing Page email field. Do not change the visual design.
3. Build a three-field form: name, email, and a radio group for contact preference. Use one fieldset and one legend.
4. Add `minlength="2"` and `maxlength="40"` to a name field. Test empty, short, and long values.
5. Create a checkbox group for three interests. Give each checkbox its own `id` and `value`, but use the same `name`.
6. Build a form that uses a `<select>` with a disabled placeholder option and a `selected` default option.
7. Test the Hotel Feedback form with the keyboard only. Note the tab order and any control that is difficult to reach.

## I. Common mistakes

- **A label that is not connected to its input.** The `for` value and the input's `id` must match exactly.
- **Using `name` where `id` is needed.** `name` submits data; `id` connects labels and anchors.
- **Reusing an `id`.** IDs must be unique in a document.
- **Different `name` values for one radio group.** The browser then treats them as separate groups.
- **Using a placeholder instead of a label.** Placeholders disappear when the user types and are not a reliable label.
- **Forgetting `required` on a field that must be filled.** The browser cannot enforce a rule that is not declared.
- **Marking every field required.** Optional fields should remain optional.
- **Using `type="text"` for an email address.** `type="email"` enables built-in format validation and the right mobile keyboard.
- **Forgetting `type` on a `<button>` inside a form.** The default is `submit`, which may submit when you intended a different action.
- **Assuming browser validation is enough.** Server-side validation is still necessary for any real application.
- **Leaving a form without an action.** That is fine for practice, but it does not submit anywhere.

## J. Summary

Forms collect information through controls. A label must be connected to its control, a control needs a `name` for submission, and related controls should be grouped with `<fieldset>` and `<legend>`. Input types provide the right keyboard and basic validation, while `required`, `min`, `max`, and similar attributes express rules in the markup.

The repository contains a strong example in the Hotel Feedback form and a useful broken association in the Survey Form. The Product Landing Page shows why `type="email"` alone is not the same as requiring an email address. Reading these details is the difference between copying a form and understanding it.

## K. Next module

Continue to [05. Semantic HTML](05-semantic-html.md) to learn how landmarks and sectioning elements give a page a meaningful outline.
