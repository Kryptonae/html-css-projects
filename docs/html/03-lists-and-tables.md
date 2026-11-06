# 03. Lists and Tables

## A. Introduction

Lists and tables organise information, but they organise different kinds of information. A list is a sequence or a set of related items. A table is a grid of data that only makes sense when a cell can be connected to its row and column headings.

Beginners often use tables to lay out a page or lists to imitate a table. Both shortcuts make the markup harder to read and harder to use with assistive technology. This chapter looks at the list and table elements in the repository, including examples where the structure is correct and one where a footer row is nested in the wrong place.

> **Code conventions:** A code block followed by a **Source:** link is a repository example taken from that file; the excerpt may leave out unrelated markup, and the link opens the complete source. A block without a source link is a teaching example — either a generic syntax illustration or a shortened or adapted excerpt named in the surrounding prose. Section H contains new practice tasks, not requirements from the original freeCodeCamp exercises. The original HTML and CSS files are not modified by this course.

## B. Learning objectives

By the end of this chapter you should be able to:

- Choose between `<ul>`, `<ol>`, and `<dl>`.
- Nest a list inside a list item without breaking the outer list.
- Build a table with `<caption>`, `<thead>`, `<tbody>`, and `<tfoot>`.
- Use `<th>` for headings and `<td>` for data cells.
- Connect header cells to data cells with `scope`.
- Use `colspan` and `rowspan` for cells that span columns or rows.
- Detect invalid table nesting and explain why it matters.
- Decide when a table is the right element and when it is not.

## C. Core concepts

### Unordered, ordered, and description lists

An unordered list is a set of items where order does not carry meaning:

```html
<ul>
  <li>catnip</li>
  <li>laser pointers</li>
  <li>lasagna</li>
</ul>
```

An ordered list is a sequence where the order matters:

```html
<ol>
  <li>flea treatment</li>
  <li>thunder</li>
  <li>other cats</li>
</ol>
```

A description list pairs terms with descriptions:

```html
<dl>
  <dt>Google Chrome</dt>
  <dd>A free web browser developed by Google and first released in 2008.</dd>

  <dt>Firefox</dt>
  <dd>A free web browser developed by the Mozilla Corporation and first created in 2004.</dd>
</dl>
```

The List of Major Web Browsers page uses exactly this pattern for five browsers. It is a good example of choosing `<dl>` instead of forcing term/description pairs into a bulleted list.

### Nested lists

A nested list belongs inside an `<li>`, not directly inside the parent `<ul>` or `<ol>`:

```html
<ul class="todo-list">
  <li class="item">
    <label for="gaming">Explore gaming keyboards</label>
    <ul class="sub-item">
      <li><a href="#" class="sub-item-link">Store link</a></li>
    </ul>
  </li>
</ul>
```

The outer list contains one item. That item contains a label and an inner list. The inner list is still part of the same item, which is why it sits before the closing `</li>`.

### Tables are for data

Use a table when the information has rows and columns that need to be compared. Do not use a table because you want two columns of page content; CSS Grid or Flexbox is the right tool for layout.

A table starts with a caption that describes the data:

```html
<table>
  <caption>Calculus Final Exam Grades</caption>
  <thead>
    <tr>
      <th>Last Name</th>
      <th>First Name</th>
      <th>Grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Davis</td>
      <td>Alex</td>
      <td>54</td>
    </tr>
  </tbody>
</table>
```

- `<caption>` gives the table a name.
- `<thead>` groups the header rows.
- `<tbody>` groups the data rows.
- `<tfoot>` groups summary or footer rows.
- `<tr>` is a table row.
- `<th>` is a header cell.
- `<td>` is a data cell.

The order of `<thead>`, `<tbody>`, and `<tfoot>` is not just cosmetic. Browsers and assistive technology use these groups to understand the table's structure.

### Header scope

A header cell can describe a column or a row. The `scope` attribute makes that relationship explicit:

```html
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
    <th scope="row">9:00 AM</th>
    <td>Keynote: Tech Future</td>
    <td>Intro to Web Dev</td>
    <td>UX for All</td>
  </tr>
</tbody>
```

`scope="col"` means the header describes its column. `scope="row"` means the header describes its row. The Tech Conference schedule uses both, so a screen reader can connect "CSS for Beginners" with the 10:00 AM row and the Track B column.

### Spanning cells

`colspan` makes a cell span multiple columns:

```html
<tr>
  <th scope="row">11:00 AM</th>
  <td colspan="3">Break</td>
</tr>
```

`rowspan` makes a cell span multiple rows. Use both attributes sparingly, because a complex table becomes difficult to follow on a small screen and in a screen reader.

### A footer row belongs outside the body

The Book Catalog page puts its total in a proper `<tfoot>` after `</tbody>`:

```html
<tbody>
  <!-- book rows -->
</tbody>

<tfoot>
  <tr>
    <td colspan="4">Total Books: 5</td>
  </tr>
</tfoot>
```

The Final Exams table does not:

```html
<tbody>
  <!-- grade rows -->
  <tfoot>
    <tr>
      <td colspan="2">Average Grade</td>
      <td>78.8</td>
    </tr>
  </tfoot>
</tbody>
```

The `<tfoot>` is inside `<tbody>`. That is invalid table structure. The footer should be a sibling of `<tbody>`, after it. The browser may repair the markup, but the source is still wrong and the document outline is less predictable.

## D. Syntax

Lists:

```html
<ul>
  <li>Item</li>
  <li>Item</li>
</ul>

<ol>
  <li>First step</li>
  <li>Second step</li>
</ol>

<dl>
  <dt>Term</dt>
  <dd>Description</dd>
</dl>
```

Table:

```html
<table>
  <caption>Table name</caption>
  <thead>
    <tr>
      <th scope="col">Column heading</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">Row heading</th>
      <td>Data</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td colspan="2">Summary</td>
    </tr>
  </tfoot>
</table>
```

## E. Code examples

### Example 1: Description list

```html
<h1>List of Major Web Browsers</h1>
<dl>
  <dt>Google Chrome</dt>
  <dd>This is a free web browser developed by Google and first released in 2008.</dd>

  <dt>Firefox</dt>
  <dd>This is a free web browser developed by the Mozilla Corporation and first created in 2004.</dd>

  <dt>Safari</dt>
  <dd>This browser was developed by Apple and is the default browser for iPhone, iPad and Mac devices.</dd>
</dl>
```

Source: [`List_of_Major_Web_Browsers.html`](<../../HTML/Semantic HTML Project/List of Major Web Browsers/List_of_Major_Web_Browsers.html>). Status: **HTML-only**.

### Example 2: A table with a header, body, and footer

```html
<table>
  <caption>Book Catalog</caption>

  <thead>
    <tr>
      <th>Title</th>
      <th>Author</th>
      <th>Genre</th>
      <th>Publication Year</th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>How to Learn to Code and Get a Developer Job</td>
      <td>Quincy Larson</td>
      <td>Learn To Code</td>
      <td>2024</td>
    </tr>
  </tbody>

  <tfoot>
    <tr>
      <td colspan="4">Total Books: 5</td>
    </tr>
  </tfoot>
</table>
```

Source: [`Book_Catalog.html`](<../../HTML/Forms and Tables/Build a Book Catalog Table/Book_Catalog.html>). Status: **HTML-only**.

Two content details in this file are worth noticing. The table has no `scope` attributes on its header cells, although they would improve the markup. The first and fourth titles also contain the literal text `U+002d` where a hyphen was probably intended. That is a content-level artefact in the source, not a table-structure rule.

### Example 3: Row and column headers

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

### Example 4: A list with nested actions

```html
<ul class="todo-list">
  <li class="item">
    <input type="checkbox" name="list" id="gaming" value="gaming" />
    <label for="gaming">Explore gaming keyboards</label>

    <ul class="sub-item">
      <li>
        <a href="#" target="_blank" class="sub-item-link">Store link</a>
      </li>
    </ul>
  </li>
</ul>
```

Source: [`CSS/Basic CSS/Build a Stylized To-Do List/index.html`](<../../CSS/Basic CSS/Build a Stylized To-Do List/index.html>). Status: **Implemented** as a CSS practice project.

The nested list gives each to-do item a related action. It also shows a common area to review: `href="#"` is a placeholder destination, not a working store link. The one item's `id` and `value` also contain a trailing space (`"Processor "`), which makes the label association fragile. These are useful details to notice when reading source code, not changes the documentation makes.

## F. Step-by-step explanation

### Building a list

1. **Decide whether order matters.** Use `<ol>` for steps or rankings, `<ul>` for a set, and `<dl>` for term/description pairs.
2. **Put every item in an `<li>`.** Text cannot sit directly inside `<ul>` or `<ol>`.
3. **Nest inside the item.** Put a sublist before the closing `</li>` of the item it belongs to.
4. **Keep link text meaningful.** A list of actions should say what each action does.
5. **Do not use a list for layout.** A list is a semantic group of items, not a row of boxes.

### Building a table

1. **Write the caption first.** State what the table contains.
2. **Create the header row.** Use `<th>` for each heading.
3. **Add `scope`.** Use `scope="col"` for column headings and `scope="row"` for row headings.
4. **Put data rows in `<tbody>`.** Use `<td>` for data and `<th scope="row">` for a row heading.
5. **Put summary rows in `<tfoot>`.** Close `<tbody>` first.
6. **Use `colspan` or `rowspan` only when necessary.** Check the total number of columns in every row.
7. **Read the table without CSS.** If the structure is unclear without borders and colour, the markup needs work.

## G. Repository implementations

| Implementation | What it demonstrates | Status | Source |
| --- | --- | --- | --- |
| List of Major Web Browsers | Description list with `<dt>` and `<dd>` | HTML-only | [Open](<../../HTML/Semantic HTML Project/List of Major Web Browsers/List_of_Major_Web_Browsers.html>) |
| Book Catalog | Caption, `thead`, `tbody`, `tfoot`, `colspan` | HTML-only | [Open](<../../HTML/Forms and Tables/Build a Book Catalog Table/Book_Catalog.html>) |
| Final Exams Table | Header/data rows with an invalid nested `tfoot` | HTML-only | [Open](<../../HTML/Forms and Tables/Build a Final Exams Table/Calculus_Final_Exams_Table.html>) |
| Tech Conference Schedule | `scope="col"`, `scope="row"`, `colspan` | HTML-only | [Open](<../../HTML/Accessibility/Build a Tech Conference Schedule Table/index.html>) |
| Stylized To-Do List | Nested lists with checkboxes and links | Implemented | [Open](<../../CSS/Basic CSS/Build a Stylized To-Do List/index.html>) |

## H. Additional challenges

These are new practice tasks for this course; they are not requirements from the original exercises.

1. Fix the Final Exams table by moving `<tfoot>` outside `<tbody>`. Compare the result in the browser's element inspector.
2. Add `scope="col"` to the Book Catalog header cells. Add a `scope="row"` header for the title column if you want a stronger relationship.
3. Build a three-day study schedule with a caption, column headers, row headers, and one `colspan` cell for a break.
4. Create a description list of five HTML elements and what they do. Use `<dt>` for the element name and `<dd>` for the explanation.
5. Write a nested to-do list with one sub-task per item. Then replace the `href="#"` placeholders with real destinations of your choice.
6. Build a comparison table for three CSS layout methods: normal flow, Flexbox, and Grid. Use one row per method and one column per comparison point.

## I. Common mistakes

- **Putting text directly inside `<ul>`.** Wrap each item in `<li>`.
- **Nesting a list as a direct child of `<ul>`.** Put the nested list inside an `<li>`.
- **Using a table for page layout.** Use CSS for layout and keep tables for data.
- **Forgetting the caption.** A caption gives the table a name and context.
- **Using `<td>` for every cell.** Header cells should use `<th>`.
- **Leaving `scope` out of a complex table.** Explicit scope makes header relationships clearer.
- **Putting `<tfoot>` inside `<tbody>`.** The footer is a sibling of the body, not a child.
- **Miscounting columns after `colspan`.** Every row must still describe the same grid.
- **Using empty links as buttons.** `href="#"` does not perform an action; use a real destination or a button with behaviour.
- **Assuming CSS will fix semantics.** Borders and colours do not create table relationships.

## J. Summary

Lists group related items. Use `<ul>` for unordered sets, `<ol>` for sequences, and `<dl>` for term/description pairs. Tables describe data in rows and columns. A useful table has a caption, clear header cells, correct grouping elements, and `scope` where relationships need to be explicit.

The repository contains a correct description list, a mostly correct book catalog, a well-labelled conference schedule, and a final-exams table with a structural error. Learning to spot the difference is more valuable than memorising the tags in isolation.

## K. Next module

Continue to [04. Forms and Inputs](04-forms-and-inputs.md) to learn how to collect information with labels, input types, fieldsets, and validation.
