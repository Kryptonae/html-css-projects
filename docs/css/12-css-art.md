# 12. CSS Art

## A. Introduction

CSS art is the practice of drawing with layout primitives: boxes, borders, gradients, shadows, border radii, transforms, and pseudo-elements. It is not a separate CSS feature. It is a creative use of the features covered in the previous chapters.

The repository contains a cat, a Rothko-style painting, a city skyline, a Ferris wheel, and a penguin. These are useful exercises because they force you to think about positioning, stacking, colour, and the box model in a visual way. They are also a reminder that CSS art is usually decorative and that a real illustration may be better served by SVG.

> **Code conventions:** A code block followed by a **Source:** link is a repository example taken from that file; the excerpt may leave out unrelated markup, and the link opens the complete source. A block without a source link is a teaching example — either a generic syntax illustration or a shortened or adapted excerpt named in the surrounding prose. Section H contains new practice tasks, not requirements from the original freeCodeCamp exercises. The original HTML and CSS files are not modified by this course.

## B. Learning objectives

By the end of this chapter you should be able to:

- Draw simple shapes with `width`, `height`, `background`, and `border-radius`.
- Create triangles with transparent borders.
- Layer elements with absolute positioning and `z-index`.
- Use gradients to create shading, windows, and skies.
- Use `box-shadow`, `filter: blur()`, and `transform` for depth.
- Use pseudo-elements as extra shapes.
- Decide when CSS art is appropriate and when SVG is the better tool.
- Recognise the source-level limitations of the repository's art pages.

## C. Core concepts

### Everything is a box

A `<div>` with a background colour is a rectangle:

```css
.cat-head {
  width: 205px;
  height: 180px;
  background: linear-gradient(#5e5e5e 85%, #45454f 100%);
  border: 1px solid #000;
  border-radius: 46%;
}
```

`border-radius` turns the rectangle into an ellipse or a rounded shape. A percentage radius can create a circle or an oval depending on the element's dimensions.

### Triangles from borders

A zero-sized element with thick borders can create a triangle:

```css
.cat-left-ear {
  position: absolute;
  top: -26px;
  left: -31px;
  z-index: 1;
  border-top-left-radius: 90px;
  border-top-right-radius: 10px;
  transform: rotate(-45deg);
  border-left: 35px solid transparent;
  border-right: 35px solid transparent;
  border-bottom: 70px solid #5e5e5e;
}
```

The left and right borders are transparent. The bottom border is the visible triangle. Rotating it turns the triangle into an ear.

### Gradients as shading

A gradient can suggest light, shadow, or a curved surface:

```css
.cat-head {
  background: linear-gradient(#5e5e5e 85%, #45454f 100%);
}
```

The first colour covers 85% of the gradient, then blends into the darker colour. The result is a subtle shadow at the bottom of the head.

The City Skyline uses a radial gradient for the sky:

```css
.sky {
  background: radial-gradient(
    circle closest-corner at 15% 15%,
    #ffcf33,
    #ffcf33 20%,
    #ffff66 21%,
    #bbeeff 100%
  );
}
```

The repeated colour stops create a sun with a soft halo.

### Shadows and blur

```css
.one {
  box-shadow: 0 0 3px 3px #efb762;
  filter: blur(1px);
}
```

`box-shadow` adds a glow around the shape. `filter: blur()` softens the edge, mimicking paint. The Rothko canvas also applies `filter: blur(2px)` to the whole painting.

Blur can be expensive on large surfaces. Use it for small decorative areas, not for text or interactive controls.

### Layering

CSS art usually relies on absolute positioning and stacking:

```css
.cat-left-ear {
  position: absolute;
  z-index: 1;
}

.cat-head {
  position: absolute;
}
```

The ear sits above the head because it has a higher `z-index` within the same stacking context. A positioned parent creates a local coordinate system for its children.

### Pseudo-elements as shapes

The Piano's black keys are pseudo-elements:

```css
.key.black--key::after {
  background-color: #1d1e22;
  content: "";
  position: absolute;
  left: -18px;
  width: 32px;
  height: 100px;
  border-radius: 0 0 3px 3px;
}
```

The white key is the real element. The black key is generated content positioned over it. This keeps the HTML small, but it also means the black keys are not real elements in the DOM.

### CSS art versus SVG

The Heart Icon is an inline SVG:

```html
<svg width="24" height="24" viewBox="0 0 24 24" fill="red">
  <path d="M12 21s-6-4.35-9.33-8.22..." />
</svg>
```

SVG is usually better for icons and illustrations because:

- It scales without pixelation.
- The geometry is explicit.
- It can be styled with CSS.
- It can carry an accessible name with `<title>`.
- It does not require a stack of decorative divs.

CSS art is still useful for small decorative effects, loading animations, and experiments that need to respond to CSS state. For a complex illustration, SVG is easier to maintain.

### Accessibility of decorative art

Empty divs are ignored by screen readers, which is appropriate for decorative art. If the art conveys information, add a text alternative instead of relying on the shapes. The Cat Painting has no text content and no accessible description; that is fine if it is purely decorative, but it would be insufficient as an instructional diagram.

The Cat Painting also lacks the viewport meta tag, so it is flagged **Implemented\***. The art itself is complete; the mobile rendering is the caveat.

## D. Syntax

Circle:

```css
.circle {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  background: orange;
}
```

Triangle:

```css
.triangle {
  width: 0;
  height: 0;
  border-left: 50px solid transparent;
  border-right: 50px solid transparent;
  border-bottom: 100px solid teal;
}
```

Gradient:

```css
.shape {
  background: linear-gradient(45deg, #5e5e5e, #45454f);
}
```

Layer:

```css
.parent {
  position: relative;
}

.child {
  position: absolute;
  top: 10px;
  left: 20px;
  z-index: 1;
}
```

## E. Code examples

### Example 1: The cat head

```css
.cat-head {
  position: absolute;
  right: 0;
  left: 0;
  top: 0;
  bottom: 0;
  margin: auto;
  background: linear-gradient(#5e5e5e 85%, #45454f 100%);
  width: 205px;
  height: 180px;
  border: 1px solid #000;
  border-radius: 46%;
}
```

Source: [`CSS/Positioning/Build a Cat Painting/styles.css`](<../../CSS/Positioning/Build%20a%20Cat%20Painting/styles.css>). Status: **Implemented\***.

The cat head is centred with all four offsets set to `0` and `margin: auto`. It is the containing block for the ears, eyes, nose, mouth, and whiskers.

### Example 2: A border triangle

```css
.cat-nose {
  position: absolute;
  top: 108px;
  left: 85px;
  border-top-left-radius: 50%;
  border-bottom-right-radius: 50%;
  border-bottom-left-radius: 50%;
  transform: rotate(180deg);
  border-left: 15px solid transparent;
  border-right: 15px solid transparent;
  border-bottom: 20px solid #442c2c;
}
```

Source: [`CSS/Positioning/Build a Cat Painting/styles.css`](<../../CSS/Positioning/Build%20a%20Cat%20Painting/styles.css>). Status: **Implemented\***.

The nose is a triangle built from transparent side borders and a coloured bottom border. The asymmetric radius and the rotation soften it into a nose shape.

### Example 3: A Rothko-style canvas

```css
.canvas {
  width: 500px;
  height: 600px;
  background-color: #4d0f00;
  overflow: hidden;
  filter: blur(2px);
}

.one {
  width: 425px;
  height: 150px;
  background-color: #efb762;
  margin: 20px auto;
  box-shadow: 0 0 3px 3px #efb762;
  border-radius: 9px;
  transform: rotate(-0.6deg);
}

.two {
  width: 475px;
  height: 150px;
  background-color: #efb762;
  margin: 0 auto 20px;
  box-shadow: 0 0 3px 3px #8f0401;
  border-radius: 8px 10px;
  transform: rotate(0.4deg);
}

.three {
  width: 91%;
  height: 28%;
  background-color: #b20403;
  margin: auto;
  filter: blur(2px);
  box-shadow: 0 0 5px 5px #b20403;
  border-radius: 30px 25px 60px 12px;
  transform: rotate(-0.2deg);
}
```

Source: [`CSS/The Box Model/Design a Rothko Painting/style.css`](<../../CSS/The%20Box%20Model/Design%20a%20Rothko%20Painting/style.css>). Status: **Implemented**.

The painting is three blurred rectangles with slight rotations and soft shadows. The frame is a border and padding around the canvas. The effect comes from restrained colour and irregular edges, not from complex markup.

### Example 4: A city from gradients

```css
.sky {
  background: radial-gradient(
    circle closest-corner at 15% 15%,
    #ffcf33,
    #ffcf33 20%,
    #ffff66 21%,
    #bbeeff 100%
  );
}

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

Source: [`CSS/Variables/Build a City Skyline/style.css`](<../../CSS/Variables/Build%20a%20City%20Skyline/style.css>). Status: **Implemented**.

The skyline is built from gradients, border triangles, and variable colours. The repeating gradient creates rows of windows without adding a div for every window.

### Example 5: An inline SVG heart

```html
<svg width="24" height="24" viewBox="0 0 24 24" fill="red">
  <path
    d="M12 21s-6-4.35-9.33-8.22C-.5 7.39 3.24 1 8.4 4.28 10.08 5.32 12 7.5 12 7.5s1.92-2.18 3.6-3.22C20.76 1 24.5 7.39 21.33 12.78 18 16.65 12 21 12 21z"
  ></path>
</svg>
```

Source: [`HTML/Basic HTML Project/Build a Heart Icon/Heart_Icon.html`](<../../HTML/Basic%20HTML%20Project/Build%20a%20Heart%20Icon/Heart_Icon.html>). Status: **HTML-only**.

The heart is a single path in a 24×24 coordinate system. Compared with a CSS heart made from two circles and a rotated square, the SVG is smaller, sharper, and easier to scale.

## F. Step-by-step explanation

1. **Choose the simplest shape that works.** Rectangles and circles cover a lot of ground.
2. **Set up a positioned container.** The art should live inside a known coordinate system.
3. **Draw the largest shape first.** The head, canvas, or sky.
4. **Layer smaller shapes on top.** Use absolute positioning and `z-index`.
5. **Use gradients for shading.** A subtle gradient often looks better than a flat fill.
6. **Use border triangles for ears, beaks, roofs, and arrows.** Transparent side borders are the trick.
7. **Add blur and shadow sparingly.** They create depth but can look muddy.
8. **Keep the HTML minimal.** Use pseudo-elements or gradients instead of a div for every detail.
9. **Test at different sizes.** CSS art built with fixed pixels may not scale.
10. **Decide whether SVG would be better.** If the art is an icon or a complex illustration, use SVG.
11. **Hide decorative art from assistive technology when appropriate.** Empty divs are usually ignored, but check the accessibility tree.
12. **Document the limitation.** A missing viewport or a fixed-size canvas is worth knowing before reuse.

## G. Repository implementations

| Implementation | CSS art technique | Status | Source |
| --- | --- | --- | --- |
| Cat Painting | Absolute positioning, border triangles, radii, gradients, transforms | Implemented\* | [Open](<../../CSS/Positioning/Build a Cat Painting/index.html>) |
| Rothko Painting | Blurred rectangles, shadows, rotation, frame | Implemented | [Open](<../../CSS/The Box Model/Design a Rothko Painting/index.html>) |
| City Skyline | Gradients, border triangles, CSS variables, flex layout | Implemented | [Open](<../../CSS/Variables/Build a City Skyline/index.html>) |
| Ferris Wheel | Circles, lines, absolute positioning, animation | Implemented | [Open](<../../CSS/Animations/Build an Animated Ferris Wheel/index.html>) |
| Flappy Penguin | Gradients, border radii, absolute positioning, pseudo-elements | Implemented\* | [Open](<../../CSS/Animations/Build a Flappy Penguin/index.html>) |
| Heart Icon | Inline SVG comparison | HTML-only | [Open](<../../HTML/Basic HTML Project/Build a Heart Icon/Heart_Icon.html>) |

## H. Additional challenges

These are new practice tasks for this course; they are not requirements from the original exercises.

1. Draw a simple house with a rectangle, a border-triangle roof, and a gradient sky.
2. Recreate the Heart Icon with CSS shapes, then compare the code size and scaling with the SVG version.
3. Build a CSS moon with a circle, a box-shadow, and a radial gradient.
4. Make a three-layer landscape with a sky gradient, distant hills, and a foreground shape.
5. Add a subtle blur and shadow to a card illustration. Remove one at a time and describe the difference.
6. Build the same simple icon twice: once with CSS and once with SVG. Which is easier to make accessible?
7. Create a CSS art piece that uses only one HTML element and its pseudo-elements.
8. Test one art page at 320px and at 1440px. Record every element that overflows or distorts.

## I. Common mistakes

- **Using too many divs.** Gradients and pseudo-elements can replace many empty elements.
- **Positioning without a positioned parent.** The art escapes its container.
- **Forgetting `z-index`.** Layers appear in the wrong order.
- **Using fixed pixel sizes for everything.** The art may not scale on small screens.
- **Overusing blur.** It can be slow and make the image look muddy.
- **Forgetting `overflow: hidden`.** Shapes spill outside the canvas.
- **Relying on CSS art for essential information.** Use real text or SVG with an accessible name.
- **Assuming pseudo-elements work on replaced elements.** They do not reliably apply to images and inputs.
- **Missing viewport metadata.** The Cat Painting is the repository example.
- **Choosing CSS art when SVG is simpler.** Complex illustrations become brittle very quickly.

## J. Summary

CSS art uses the same properties as ordinary layout: boxes, borders, gradients, shadows, transforms, and positioning. Border triangles make ears and noses, gradients make skies and windows, and blur and shadow create depth. The result can be impressive, but it is still decoration and should be treated as such.

The Cat Painting is a layered portrait built almost entirely from absolute positioning. The Rothko Painting uses colour and blur. The City Skyline uses gradients and variables. The Heart Icon shows why SVG is often the better choice for an icon. CSS art is a useful way to master the box model and stacking, not a replacement for every image format.

## K. Next module

The CSS track ends here. Return to the [course map](../README.md) to choose a project from the [Projects Guide](../projects/projects-guide.md) and apply the chapters to a larger page.
