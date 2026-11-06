# 11. Transitions and Animations

## A. Introduction

A transition smooths a change between two states. An animation plays a sequence of states defined with `@keyframes`. Both are built on the same idea: a property changes over time.

The repository uses transitions for hover effects and state changes, and keyframe animations for a Ferris wheel, a moon orbit, and a waving penguin. These examples are visually impressive, but they also show the importance of `transform-origin`, timing, and reduced-motion support.

> **Code conventions:** A code block followed by a **Source:** link is a repository example taken from that file; the excerpt may leave out unrelated markup, and the link opens the complete source. A block without a source link is a teaching example — either a generic syntax illustration or a shortened or adapted excerpt named in the surrounding prose. Section H contains new practice tasks, not requirements from the original freeCodeCamp exercises. The original HTML and CSS files are not modified by this course.

## B. Learning objectives

By the end of this chapter you should be able to:

- Write a `transition` shorthand and its longhand properties.
- Animate `transform` without causing layout shifts.
- Define `@keyframes` with percentage stops.
- Apply an animation with duration, timing, iteration, and direction.
- Use `transform-origin` to control rotation.
- Explain how counter-rotation keeps Ferris wheel cabins upright.
- Add a `prefers-reduced-motion` fallback.
- Identify invalid animation declarations in the repository.

## C. Core concepts

### Transitions

A transition needs a starting value, an ending value, and a duration:

```css
.pricing-card {
  transform: scale(1);
  transition: transform 0.3s ease-in-out;
}

.pricing-card:hover {
  transform: scale(1.05);
}
```

The longhand form is:

```css
transition-property: transform;
transition-duration: 0.3s;
transition-timing-function: ease-in-out;
transition-delay: 0s;
```

You can transition more than one property:

```css
.card {
  transition: transform 0.3s, background-color 0.3s ease;
}
```

Not every property is cheap to animate. `transform` and `opacity` are usually smoother than properties that trigger layout, such as `width`, `height`, `top`, or `left`.

### Transforms

```css
transform: rotate(45deg);
transform: scale(1.05);
transform: translateX(20px);
transform: skewX(10deg);
```

Transforms do not affect the normal flow. A scaled card may visually overlap its neighbours without changing their layout positions. That is useful for hover effects, but it can also cause clipping or overlap.

### Keyframes

```css
@keyframes wheel {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
```

The `0%` and `100%` stops are the start and end. You can add intermediate stops:

```css
@keyframes cabins {
  0% {
    transform: rotate(0deg);
  }
  25% {
    background-color: yellow;
  }
  50% {
    background-color: purple;
  }
  75% {
    background-color: yellow;
  }
  100% {
    transform: rotate(-360deg);
  }
}
```

Properties not mentioned at a stop are interpolated from the surrounding stops.

### The animation shorthand

```css
.wheel {
  animation: wheel 10s linear infinite;
}
```

The values are:

- `wheel` — the keyframe name.
- `10s` — duration.
- `linear` — timing function.
- `infinite` — iteration count.

The longhand properties include `animation-name`, `animation-duration`, `animation-timing-function`, `animation-delay`, `animation-iteration-count`, `animation-direction`, `animation-fill-mode`, and `animation-play-state`.

### transform-origin

`transform-origin` sets the point around which a transform is applied:

```css
.line {
  transform-origin: 0% 0%;
}
```

The Ferris wheel's spokes rotate around their top-left corner, which is the centre of the wheel. The cabins use:

```css
.cabin {
  transform-origin: 50% 0%;
}
```

They rotate around their top centre, which is where they attach to the wheel.

### Counter-rotation

The wheel rotates clockwise:

```css
@keyframes wheel {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}
```

The cabins rotate in the opposite direction:

```css
@keyframes cabins {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(-360deg); }
}
```

Because the cabin animation has the same duration and timing, the two rotations cancel visually and the cabins stay upright while travelling around the wheel. This is a classic animation technique.

### Motion and accessibility

Some people experience dizziness, nausea, or distraction from motion. Provide a reduced-motion path:

```css
@media (prefers-reduced-motion: reduce) {
  .wheel,
  .cabin {
    animation: none;
  }
}
```

The repository's animation pages do not include a reduced-motion rule. The Quiz stylesheet does use `prefers-reduced-motion` for smooth scrolling, which is a good model. Adding a similar rule to the Ferris Wheel, Moon Orbit, and Penguin would be a meaningful improvement.

### An invalid declaration

The Moon Orbit keyframes contain:

```css
@keyframes orbit {
  0% {
    transform: rotate(0deg);
    translate: (-50%, -50%)
  }
  100% {
    transform: rotate(360deg);
    translate: (-50%, -50%)
  }
}
```

The `translate` property expects lengths, not a parenthesised pair. The parentheses make the declaration invalid, so the browser ignores it. The orbit still rotates because the `transform` declaration is valid, but the intended centring translation is lost. A valid version would be:

```css
translate: -50% -50%;
```

or the translation could be included in the `transform`:

```css
transform: translate(-50%, -50%) rotate(0deg);
```

That is a new correction suggestion, not a change made to the repository.

## D. Syntax

Transition:

```css
.button {
  transition: background-color 0.3s ease, transform 0.2s ease;
}

.button:hover {
  background-color: #3b3b4f;
  transform: translateY(-2px);
}
```

Keyframes:

```css
@keyframes fade-in {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.card {
  animation: fade-in 0.5s ease-out both;
}
```

Reduced motion:

```css
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```

## E. Code examples

### Example 1: The Ferris wheel

```css
.wheel {
  border: 2px solid black;
  border-radius: 50%;
  margin-left: 50px;
  position: absolute;
  height: 55vw;
  width: 55vw;
  max-width: 500px;
  max-height: 500px;
  animation: wheel 10s linear infinite;
}

.line {
  background-color: black;
  width: 50%;
  height: 2px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform-origin: 0% 0%;
}

.cabin {
  background-color: red;
  width: 20%;
  height: 20%;
  position: absolute;
  border: 2px solid;
  transform-origin: 50% 0%;
  animation: cabins 10s ease-in-out infinite;
}
```

Source: [`CSS/Animations/Build an Animated Ferris Wheel/style.css`](<../../CSS/Animations/Build%20an%20Animated%20Ferris%20Wheel/style.css>). Status: **Implemented**.

The wheel and cabins share a duration of 10 seconds. The wheel uses `linear` timing; the cabins use `ease-in-out`. Because the timing functions differ, the counter-rotation is not perfectly cancelled at every moment, but the visual effect is still a rotating wheel with upright cabins.

### Example 2: The moon orbit

```css
.orbit {
  width: 200px;
  height: 200px;
  position: absolute;
  transform: translate(-50%, -50%);
  animation: orbit 5s linear infinite;
}

.moon {
  position: absolute;
  width: 30px;
  height: 30px;
  border: 1px solid;
  left: 100%;
  border-radius: 50%;
  background-color: white;
}

@keyframes orbit {
  0% {
    transform: rotate(0deg);
    translate: (-50%, -50%);
  }
  100% {
    transform: rotate(360deg);
    translate: (-50%, -50%);
  }
}
```

Source: [`CSS/Animations/Build a Moon Orbit/style.css`](<../../CSS/Animations/Build%20a%20Moon%20Orbit/style.css>). Status: **Implemented\***.

The static `.orbit` rule has a valid `transform: translate(-50%, -50%)`, but the keyframes replace `transform` with a rotation. The invalid `translate` lines cannot preserve the centring. This is a subtle and useful debugging example.

### Example 3: A waving penguin

```css
.arm.left {
  top: 35%;
  left: 5%;
  transform-origin: top left;
  transform: rotate(130deg) scaleX(-1);
  animation: 3s linear infinite wave;
}

@keyframes wave {
  10% {
    transform: rotate(110deg) scaleX(-1);
  }
  20% {
    transform: rotate(130deg) scaleX(-1);
  }
  30% {
    transform: rotate(110deg) scaleX(-1);
  }
  40% {
    transform: rotate(130deg) scaleX(-1);
  }
}
```

Source: [`CSS/Animations/Build a Flappy Penguin/style.css`](<../../CSS/Animations/Build%20a%20Flappy%20Penguin/style.css>). Status: **Implemented\***.

The animation shorthand is written as `animation: 3s linear infinite wave;`. The order of values in the shorthand is flexible as long as the duration and name are identifiable. The arm rocks between two rotations, creating a wave.

### Example 4: A hover transition

```css
.card {
  background-color: white;
  max-width: 500px;
  padding: 40px;
  margin: 0 auto;
  border-radius: 10px;
  box-shadow: 0 4px 8px gray;
  transition: transform 0.3s, background-color 0.3s ease;
}

.card:hover {
  background-color: khaki;
  transform: scale(1.1);
}
```

Source: [`CSS/Pseudo Classes and Elements/Design a Greeting Card/style.css`](<../../CSS/Pseudo%20Classes%20and%20Elements/Design%20a%20Greeting%20Card/style.css>). Status: **Implemented**.

The card grows and changes colour on hover. Because the transition is on the base `.card` rule, it applies both when entering and leaving the hover state.

### Example 5: A pricing card transition

```css
.pricing-card {
  transform: scale(1);
  transition: transform 0.3s ease-in-out;
}

.pricing-card:hover {
  transform: scale(1.05);
}
```

Source: [`CSS/Flexbox/Design a Pricing Plans Layout Page/style.css`](<../../CSS/Flexbox/Design%20a%20Pricing%20Plans%20Layout%20Page/style.css>). Status: **Implemented**.

This is a restrained transition: one property, a short duration, and a small scale change. It does not move the surrounding layout because transforms do not affect flow.

## F. Step-by-step explanation

1. **Decide what should change.** A hover colour, a card lift, a loading spinner, or a decorative loop.
2. **Start with the end state.** Write the `:hover`, `:focus`, or keyframe value first.
3. **Add the transition to the base state.** This ensures it runs both ways.
4. **Keep the duration short for interactions.** 150–300ms is usually enough.
5. **Prefer `transform` and `opacity`.** They are cheaper than layout properties.
6. **Use `@keyframes` for multi-step sequences.** A transition only goes from A to B.
7. **Set `transform-origin` deliberately.** The default centre is not always what you want.
8. **Test the animation at different speeds.** A slow animation may look broken; a fast one may be unreadable.
9. **Add a reduced-motion rule.** Stop or shorten non-essential motion.
10. **Check the final state.** Use `animation-fill-mode` if the element must retain the last keyframe.
11. **Avoid infinite animation on essential content.** It can distract and drain battery.

## G. Repository implementations

| Implementation | Motion feature | Status | Source |
| --- | --- | --- | --- |
| Ferris Wheel | Rotation, counter-rotation, transform-origin, colour keyframes | Implemented | [Open](<../../CSS/Animations/Build an Animated Ferris Wheel/index.html>) |
| Moon Orbit | Orbiting moon, invalid `translate` keyframes | Implemented\* | [Open](<../../CSS/Animations/Build a Moon Orbit/index.html>) |
| Flappy Penguin | Waving arm, hover/active scale, keyframes | Implemented\* | [Open](<../../CSS/Animations/Build a Flappy Penguin/index.html>) |
| Greeting Card | Hover transition on card and links | Implemented | [Open](<../../CSS/Pseudo Classes and Elements/Design a Greeting Card/index.html>) |
| Pricing Plans | Hover scale transition | Implemented | [Open](<../../CSS/Flexbox/Design a Pricing Plans Layout Page/index.html>) |
| Product Landing Page | Hover transitions on links and buttons | Implemented\* | [Open](<../../CSS/CERTIFICATION PROJECTS/Build a Product Landing Page/index.html>) |
| Quiz Webpage | Reduced-motion smooth scrolling | Link issue | [Open](<../../CSS/Accessibility/Build a Quiz Webpage, Not started W/index.html>) |

## H. Additional challenges

These are new practice tasks for this course; they are not requirements from the original exercises.

1. Add a `prefers-reduced-motion: reduce` rule to the Ferris Wheel that stops both animations.
2. Fix the Moon Orbit keyframes by using `translate: -50% -50%;` or by combining the translation and rotation in `transform`.
3. Build a button that lifts 2px on hover and returns smoothly.
4. Create a loading spinner with a single `@keyframes` rotation and `animation: spin 1s linear infinite`.
5. Animate a card fading in with `opacity` and `translateY`. Use `animation-fill-mode: both`.
6. Change the Ferris Wheel's timing function and describe how the motion changes.
7. Build a three-step keyframe animation with different background colours at 0%, 50%, and 100%.
8. Compare a transition on `width` with a transition on `transform: scaleX()`. Which is smoother?

## I. Common mistakes

- **Putting the transition on the hover state only.** The reverse animation may not run.
- **Animating layout properties.** `width`, `height`, and `top` can cause jank.
- **Forgetting `transform-origin`.** The element rotates around the wrong point.
- **Using an invalid value inside keyframes.** The declaration is dropped, as the Moon Orbit shows.
- **Making animations too long or too fast.** Timing is part of the design.
- **Using infinite animation for essential content.** It can distract and consume resources.
- **Forgetting reduced-motion support.** Motion can cause discomfort.
- **Assuming `animation-fill-mode` is the default.** Without it, styles may snap back after the animation.
- **Animating everything.** Restraint makes the important motion noticeable.
- **Testing only in one browser.** Timing and shorthand parsing can vary.

## J. Summary

Transitions smooth a change between two states. Keyframe animations play a defined sequence. `transform` and `opacity` are the safest properties to animate, and `transform-origin` determines the pivot point. Counter-rotation can keep a child upright while its parent rotates.

The Ferris Wheel is the strongest example of coordinated motion. The Penguin shows a short, looping gesture. The Moon Orbit contains an invalid declaration that is worth learning to spot. The repository's animation pages would benefit from reduced-motion rules, which makes accessibility the natural next concern after motion.

## K. Next module

Continue to [12. CSS Art](12-css-art.md) to see how borders, gradients, shadows, transforms, and pseudo-elements can be used as drawing tools.
