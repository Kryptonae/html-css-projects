# 09. CSS Custom Properties

## A. Introduction

A CSS custom property is a named value that you can reuse throughout a stylesheet. It is often called a CSS variable, although it is more powerful than a simple find-and-replace: it participates in the cascade, it inherits, and it can be changed in a media query or on a single component.

Custom properties are ideal for colour palettes, spacing scales, font stacks, and theme changes. The City Skyline uses them to switch from a daytime palette to a night palette. The Availability Table uses them for a six-step colour scale and reusable border styles.

> **Code conventions:** A code block followed by a **Source:** link is a repository example taken from that file; the excerpt may leave out unrelated markup, and the link opens the complete source. A block without a source link is a teaching example — either a generic syntax illustration or a shortened or adapted excerpt named in the surrounding prose. Section H contains new practice tasks, not requirements from the original freeCodeCamp exercises. The original HTML and CSS files are not modified by this course.

## B. Learning objectives

By the end of this chapter you should be able to:

- Declare a custom property with the `--` prefix.
- Read it with `var()`.
- Scope a property to `:root` or to a component.
- Provide a fallback value.
- Change a theme by redefining properties in a media query.
- Use custom properties inside gradients and shorthand values.
- Avoid the common syntax and scoping mistakes.

## C. Core concepts

### Declaring and using a custom property

```css
:root {
  --building-color1: #aa80ff;
  --window-color1: #bb99ff;
}

.bb1-window {
  background: linear-gradient(var(--building-color1), var(--window-color1));
}
```

- `--building-color1` is the property name. The double hyphen is required.
- `#aa80ff` is its value.
- `var(--building-color1)` substitutes the value.
- `:root` is the `<html>` element, so a property declared there is available to the whole document through inheritance.

Custom property names are case-sensitive. `--brand-color` and `--Brand-Color` are different properties.

### Scope and inheritance

A custom property declared on an element is available to that element and its descendants:

```css
.card {
  --card-padding: 1.5rem;
}

.card-content {
  padding: var(--card-padding);
}
```

The property does not leak to elements outside `.card`. This makes component-level tokens possible:

```css
.pricing-card {
  --card-accent: #e0a800;
}

.pricing-card.featured {
  --card-accent: #00f0ff;
}
```

### Fallbacks

`var()` accepts a fallback after a comma:

```css
color: var(--text-color, black);
```

If `--text-color` is not defined, the browser uses `black`. A fallback can itself contain a `var()`:

```css
color: var(--text-color, var(--default-text, black));
```

### Changing a theme

The City Skyline defines a daytime palette in `:root` and replaces it inside a media query:

```css
:root {
  --building-color1: #aa80ff;
  --building-color2: #66cc99;
  --building-color3: #cc6699;
  --building-color4: #538cc6;

  --window-color1: #bb99ff;
  --window-color2: #8cd9b3;
  --window-color3: #d98cb3;
  --window-color4: #8cb3d9;
}

@media (max-width: 1000px) {
  :root {
    --building-color1: #000;
    --building-color2: #000;
    --building-color3: #000;
    --building-color4: #000;

    --window-color1: #777;
    --window-color2: #777;
    --window-color3: #777;
    --window-color4: #777;
  }

  .sky {
    background: radial-gradient(
      closest-corner circle at 15% 15%,
      #ccc,
      #ccc 20%,
      #445 21%,
      #223 100%
    );
  }
}
```

Below 1000px, the buildings become black and the windows grey. Every rule that references the variables updates automatically. This is a theme change implemented entirely in CSS.

### Reusable border values

The Availability Table defines complete border declarations:

```css
:root {
  --solid-border: 1px solid black;
  --dashed-border: 1px dashed black;
}

.half {
  border-bottom: var(--dashed-border);
}

.sharp {
  border-bottom: var(--solid-border);
}
```

A custom property can hold a shorthand value, not just a single colour. This keeps related border styles consistent.

### Variables in gradients

```css
#legend-gradient {
  width: 75%;
  background-image: linear-gradient(
    to right,
    var(--color0) 0% 16%,
    var(--color1) 16% 33%,
    var(--color2) 33% 49%,
    var(--color3) 49% 66%,
    var(--color4) 66% 83%,
    var(--color5) 83% 100%
  );
  border: 2px solid black;
}
```

The six colour stops come from six custom properties. Changing one property in `:root` changes both the table cells and the legend.

### Variables cannot be used everywhere

A custom property is resolved at computed-value time. It cannot be used in a media query condition:

```css
/* Invalid: media queries cannot read custom properties this way */
@media (min-width: var(--breakpoint)) {
  /* ... */
}
```

Use a literal value in the query, or use a preprocessor if you need that kind of abstraction.

## D. Syntax

```css
:root {
  --color-primary: #1b1b32;
  --space-sm: 0.5rem;
  --space-md: 1rem;
  --font-body: "Open Sans", Arial, sans-serif;
}

.button {
  background-color: var(--color-primary);
  padding: var(--space-sm) var(--space-md);
  font-family: var(--font-body);
}

.button:hover {
  background-color: var(--color-primary-hover, #3b3b4f);
}
```

## E. Code examples

### Example 1: The City Skyline palette

```css
:root {
  --building-color1: #aa80ff;
  --building-color2: #66cc99;
  --building-color3: #cc6699;
  --building-color4: #538cc6;

  --window-color1: #bb99ff;
  --window-color2: #8cd9b3;
  --window-color3: #d98cb3;
  --window-color4: #8cb3d9;
}
```

Source: [`CSS/Variables/Build a City Skyline/style.css`](<../../CSS/Variables/Build a City Skyline/style.css>). Status: **Implemented**.

The names describe the role of each colour rather than the colour itself. `--building-color1` can become black at night without changing every rule that uses it.

### Example 2: Using a variable in a gradient

```css
.bb2b {
  width: 100%;
  height: 100%;
  background: repeating-linear-gradient(
    var(--building-color2),
    var(--building-color2) 6%,
    var(--window-color2) 6%,
    var(--window-color2) 9%
  );
}
```

Source: [`CSS/Variables/Build a City Skyline/style.css`](<../../CSS/Variables/Build a City Skyline/style.css>). Status: **Implemented**.

The repeating gradient creates the stripes of windows. The two stops before 6% use the building colour, and the two stops from 6% to 9% use the window colour.

### Example 3: A colour scale for data

```css
:root {
  --color0: #ffffff;
  --color1: #cdfecd;
  --color2: #9cfd9c;
  --color3: #51fb51;
  --color4: #05c705;
  --color5: #037d03;

  --solid-border: 1px solid black;
  --dashed-border: 1px dashed black;
}

.available-0 { background-color: var(--color0); }
.available-1 { background-color: var(--color1); }
.available-2 { background-color: var(--color2); }
.available-3 { background-color: var(--color3); }
.available-4 { background-color: var(--color4); }
.available-5 { background-color: var(--color5); }
```

Source: [`CSS/Variables/Build an Availability Table/styles.css`](<../../CSS/Variables/Build an Availability Table/styles.css>). Status: **Implemented**.

The numeric names make the scale easy to generate and compare. They are less descriptive than role-based names, so comments or a naming convention would help in a larger project.

### Example 4: A dark theme

```css
:root {
  --bg-color: #0d0e15;
  --bg-color-secondary: #252531;
  --text-primary: #ffffff;
  --text-secondary: #a0a5c0;
  --text-tertiary: orangered;
  --accent-cyan: #00f0ff;
  --accent-pink: #ff007f;
}

body {
  background-color: var(--bg-color);
  color: var(--text-primary);
}
```

Source: [`CSS/CERTIFICATION PROJECTS/Build a Product Landing Page/style.css`](<../../CSS/CERTIFICATION%20PROJECTS/Build%20a%20Product%20Landing%20Page/style.css>). Status: **Implemented\***.

The landing page has a single dark palette. To add a light theme, you could redefine these properties under a class or a `prefers-color-scheme` query without rewriting every component.

### Example 5: Component-level variables

```css
:root {
  --penguin-face: white;
  --penguin-picorna: orange;
  --penguin-skin: gray;
}

.face {
  background-color: var(--penguin-face);
}

.beak {
  background-color: var(--penguin-picorna);
}
```

Source: [`CSS/Animations/Build a Flappy Penguin/style.css`](<../../CSS/Animations/Build a Flappy Penguin/style.css>). Status: **Implemented\***.

The variables describe the parts of the penguin. A seasonal variant could change the skin and beak colours in one place.

## F. Step-by-step explanation

1. **Find repeated values.** Colours, spacing, border styles, and font stacks are good candidates.
2. **Name by role.** Prefer `--color-accent` over `--pink`.
3. **Declare global tokens on `:root`.** Use `:root` for values that apply to the whole page.
4. **Declare component tokens on the component.** Use a local property when the value should not leak.
5. **Reference values with `var()`.** Check the spelling and the double hyphen.
6. **Add a fallback when the property might be absent.** This is useful for reusable components.
7. **Change themes by redefining properties.** Do not duplicate every rule.
8. **Test without the variable.** A fallback should keep the component usable.
9. **Check the computed value in the inspector.** The Styles panel shows the resolved value.
10. **Do not use variables in media-query conditions.** Use literal breakpoints.

## G. Repository implementations

| Implementation | Custom-property use | Status | Source |
| --- | --- | --- | --- |
| City Skyline | Day/night palette switched in a media query | Implemented | [Open](<../../CSS/Variables/Build a City Skyline/index.html>) |
| Availability Table | Six-step colour scale and reusable border values | Implemented | [Open](<../../CSS/Variables/Build an Availability Table/index.html>) |
| Product Landing Page | Full dark-theme token set | Implemented\* | [Open](<../../CSS/CERTIFICATION PROJECTS/Build a Product Landing Page/index.html>) |
| Flappy Penguin | Component-level penguin colours | Implemented\* | [Open](<../../CSS/Animations/Build a Flappy Penguin/index.html>) |
| Magazine | `html { font-size: 62.5%; }` as a sizing base, not a variable | Implemented | [Open](<../../CSS/Grid/Build a Magazine/index.html>) |

## H. Additional challenges

These are new practice tasks for this course; they are not requirements from the original exercises.

1. Create a palette of five custom properties and use them in a card, a button, and a heading.
2. Add a `prefers-color-scheme: dark` block that redefines your palette.
3. Move a component's spacing values into local custom properties on the component.
4. Add fallbacks to three `var()` calls and test by removing the declarations.
5. Change the City Skyline's night breakpoint from 1000px to 700px and observe the result.
6. Build a data table with a five-step colour scale driven by variables.
7. Use a custom property for a complete `box-shadow` and reuse it on two elements.
8. Try to use a custom property in a media query. Record the error and explain why it cannot work.

## I. Common mistakes

- **Forgetting the `--` prefix.** `var(brand-color)` is not a custom property.
- **Using a custom property before it is defined in the cascade.** The value may be invalid at computed-value time.
- **Assuming custom properties are global.** They inherit, but they can also be scoped to a component.
- **Using a property name with a typo.** `var(--brand-colour)` does not match `--brand-color`.
- **Expecting case-insensitivity.** Custom property names are case-sensitive.
- **Using a variable in a media-query condition.** It is not allowed.
- **Overusing variables for one-off values.** A variable should earn its name.
- **Naming by appearance instead of role.** A colour name becomes misleading after a theme change.
- **Forgetting that fallbacks are optional but useful.** A missing property can make a declaration invalid.
- **Changing a variable without checking every consumer.** A single token can affect many components.

## J. Summary

Custom properties store named values that participate in the cascade and inherit through the tree. `:root` is the usual home for global tokens; a component can define its own local tokens. `var()` reads a property and can provide a fallback. Redefining properties in a media query is a clean way to implement a theme change.

The City Skyline's day/night palette is the strongest example. The Availability Table shows variables in data visualisation and shorthand borders. The Product Landing and Penguin pages show theme and component tokens. Used with restraint, custom properties make a stylesheet easier to change without making it harder to read.

## K. Next module

Continue to [10. Pseudo-Classes and Pseudo-Elements](10-pseudo-classes-and-elements.md) to style states, targets, form validation, and generated content.
