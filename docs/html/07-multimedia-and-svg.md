# 07. Multimedia and SVG

## A. Introduction

HTML can embed video, audio, other pages, and vector graphics. Each medium has its own element, its own attributes, and its own accessibility questions. A video without controls is a moving image the visitor cannot pause. An iframe without a title is an unnamed region. An inline SVG without a name may be invisible to a screen reader.

This chapter examines the media pages in the repository. Most of them are short exercises that load assets from the freeCodeCamp CDN, so they are useful for learning the markup without needing local media files.

> **Code conventions:** A code block followed by a **Source:** link is a repository example taken from that file; the excerpt may leave out unrelated markup, and the link opens the complete source. A block without a source link is a teaching example — either a generic syntax illustration or a shortened or adapted excerpt named in the surrounding prose. Section H contains new practice tasks, not requirements from the original freeCodeCamp exercises. The original HTML and CSS files are not modified by this course.

## B. Learning objectives

By the end of this chapter you should be able to:

- Add a video with `controls`, `poster`, `loop`, and multiple `<source>` elements.
- Add an audio player with `controls`.
- Explain what `type` does on a `<source>` element.
- Embed another page with `<iframe>` and give it a meaningful `title`.
- Use `allow`, `referrerpolicy`, and `allowfullscreen` on an embedded video.
- Write inline SVG with `viewBox`, `<path>`, and `fill`.
- Decide whether an SVG is informative or decorative.
- Identify obsolete or fragile media attributes in the repository.

## C. Core concepts

### Video

A video element can declare its sources directly or with child `<source>` elements:

```html
<video controls width="640" poster="poster.jpg">
  <source src="movie.mp4" type="video/mp4" />
  <source src="movie.webm" type="video/webm" />
  Your browser does not support the video element.
</video>
```

- `controls` shows the browser's play, pause, volume, and fullscreen controls.
- `poster` shows an image before playback starts.
- `width` sets the display width in CSS pixels.
- `loop` restarts the video when it ends.
- `muted` starts with sound off.
- `<source>` lets the browser choose the first format it supports.
- `type` is a MIME type hint, such as `video/mp4` or `video/webm`.
- Text between the tags is fallback content for browsers that cannot render the element.

The Video Player page provides four formats:

```html
<video width="640" loop controls muted poster="...">
  <source src="...mp4" type="video/mp4" />
  <source src="...webm" type="video/webm" />
  <source src="...ogg" type="video/ogg" />
  <source src="...mov" type="video/quicktime" />
</video>
```

The browser tries the sources in order and uses the first one it can play. The fallback text is missing here, which is a small robustness gap rather than a broken video.

### Audio

Audio uses the same source model:

```html
<audio src="song.mp3" controls loop></audio>
```

The Music Player page repeats this pattern for three tracks:

```html
<h2>Can't Stay Down</h2>
<p>Artist: Quincy Larson</p>
<audio src="https://cdn.freecodecamp.org/curriculum/js-music-player/can't-stay-down.mp3" loop controls></audio>
```

The apostrophe in the file name is inside an attribute value, so it does not break the HTML. The browser requests the URL exactly as written.

### Iframes

An iframe embeds another browsing context:

```html
<iframe
  width="560"
  height="315"
  src="https://www.youtube.com/embed/GDGejH3SDNQ"
  title="YouTube video player"
  frameborder="0"
  allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
  referrerpolicy="strict-origin-when-cross-origin"
  allowfullscreen
></iframe>
```

- `src` is the page being embedded.
- `title` gives the frame an accessible name. "YouTube video player" is generic; a title such as "HTML crash course video" is more useful.
- `allow` grants specific browser features to the embedded page.
- `referrerpolicy` controls how much referrer information is sent.
- `allowfullscreen` lets the embedded video enter fullscreen.
- `frameborder` is obsolete. Use CSS `border: 0` instead.

The Video Compilation page embeds three YouTube videos and gives each one the same generic title. The iframe exercise embeds a single video without a title at all.

### Inline SVG

SVG is an XML-based vector image format. It can be written directly in HTML:

```html
<svg width="24" height="24" viewBox="0 0 24 24" fill="red">
  <path d="M12 21s-6-4.35-9.33-8.22C-.5 7.39 3.24 1 8.4 4.28..." />
</svg>
```

- `viewBox` defines the internal coordinate system.
- `width` and `height` set the rendered size.
- `fill` sets the default fill colour.
- `<path>` draws a shape using the path data in `d`.

The Heart Icon page is a single inline SVG. It uses `viewBox="0 0 24 24"` and a heart-shaped path. Because the SVG is the only content, its meaning depends on context: if it is a decorative heart, it can be hidden from assistive technology; if it conveys "favourite", it needs an accessible name.

A named SVG can use a `<title>` element:

```html
<svg viewBox="0 0 24 24" role="img" aria-labelledby="heart-title">
  <title id="heart-title">Favourite</title>
  <path d="..." />
</svg>
```

A decorative SVG can use `aria-hidden="true"` and `focusable="false"`:

```html
<svg viewBox="0 0 24 24" aria-hidden="true" focusable="false">
  <path d="..." />
</svg>
```

### Images, video, and performance

The repository also uses remote images. The Magazine page adds `loading="lazy"` to its hero image so the browser can defer loading until the image is near the viewport. For media, avoid autoplaying with sound, provide a poster image, and keep file sizes reasonable. These are production concerns; the practice pages are intentionally small.

## D. Syntax

Video:

```html
<video controls width="640" poster="poster.jpg">
  <source src="movie.mp4" type="video/mp4" />
  <source src="movie.webm" type="video/webm" />
  Your browser does not support the video element.
</video>
```

Audio:

```html
<audio controls>
  <source src="song.mp3" type="audio/mpeg" />
  Your browser does not support the audio element.
</audio>
```

Iframe:

```html
<iframe
  src="https://example.com/embed"
  title="Description of the embedded content"
  width="560"
  height="315"
  allowfullscreen
></iframe>
```

Inline SVG:

```html
<svg viewBox="0 0 24 24" width="24" height="24" aria-hidden="true" focusable="false">
  <path d="..." />
</svg>
```

## E. Code examples

### Example 1: Multiple video formats

```html
<video
  width="640"
  loop
  controls
  muted
  poster="https://cdn.freecodecamp.org/curriculum/labs/past-event2.jpg"
>
  <source
    src="https://cdn.freecodecamp.org/curriculum/labs/what-is-the-map-method-and-how-does-it-work.mp4"
    type="video/mp4"
  />
  <source
    src="https://cdn.freecodecamp.org/curriculum/labs/mapmethod.webm"
    type="video/webm"
  />
  <source
    src="https://cdn.freecodecamp.org/curriculum/labs/mapmethod.ogg"
    type="video/ogg"
  />
  <source
    src="https://cdn.freecodecamp.org/curriculum/labs/mapmethod.mov"
    type="video/quicktime"
  />
</video>
```

Source: [`HTML_Video_Player.html`](<../../HTML/Basic HTML Project/Build an HTML Video Player/HTML_Video_Player.html>). Status: **HTML-only**.

The `controls` and `muted` attributes are a sensible combination: the video is silent by default but the visitor can unmute it. There is no `autoplay`, so the page does not start playing on its own.

### Example 2: Video and audio on one page

```html
<section>
  <h2>What is the map method and how does it work?</h2>
  <video src="" controls width="640">
    <source
      src="https://cdn.freecodecamp.org/curriculum/labs/what-is-the-map-method-and-how-does-it-work.mp4"
      type="video/mp4"
    />
  </video>
</section>

<section>
  <h2>Sailing Away</h2>
  <audio
    src="https://cdn.freecodecamp.org/curriculum/js-music-player/sailing-away.mp3"
    controls
    loop
  ></audio>
</section>
```

Source: [`Build an HTML Audio_and_Video_Player.html`](<../../HTML/Basic HTML Project/Build an HTML Audio and Video Player/Build an HTML Audio_and_Video_Player.html>). Status: **HTML-only**.

The video element has an empty `src=""` attribute as well as a nested `<source>`. That empty value is worth avoiding: it can cause the browser to request the current page as a media resource before trying the child source. A cleaner version removes `src=""` from the `<video>` and keeps only the `<source>` children.

### Example 3: An audio playlist

```html
<h2>Cruising for a Musing</h2>
<p>Artist: Quincy Larson</p>
<audio
  src="https://cdn.freecodecamp.org/curriculum/js-music-player/cruising-for-a-musing.mp3"
  loop
  controls
></audio>
```

Source: [`HTML_Music_Player.html`](<../../HTML/Basic HTML Project/Build an HTML Music Player/HTML_Music_Player.html>). Status: **HTML-only**.

Each track is a separate `<audio>` element with its own heading and artist line. There is no playlist logic because there is no JavaScript.

### Example 4: Embedded YouTube video

```html
<iframe
  width="560"
  height="315"
  src="https://www.youtube.com/embed/GDGejH3SDNQ?si=vOILPu7cxkUJzQ83"
  title="YouTube video player"
  frameborder="0"
  allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
  referrerpolicy="strict-origin-when-cross-origin"
  allowfullscreen
></iframe>
```

Source: [`Video_Compilation_Page.html`](<../../HTML/Basic HTML Project/Build a Video Compilation Page/Video_Compilation_Page.html>). Status: **HTML-only**.

The same title is used for all three videos. A more descriptive title would help a screen-reader user distinguish "HTML", "CSS", and "JavaScript" embeds. The `frameborder` attribute is obsolete, though browsers still tolerate it.

### Example 5: Inline SVG heart

```html
<svg width="24" height="24" viewBox="0 0 24 24" fill="red">
  <path
    d="M12 21s-6-4.35-9.33-8.22C-.5 7.39 3.24 1 8.4 4.28 10.08 5.32 12 7.5 12 7.5s1.92-2.18 3.6-3.22C20.76 1 24.5 7.39 21.33 12.78 18 16.65 12 21 12 21z"
    width="24"
  ></path>
</svg>
```

Source: [`Heart_Icon.html`](<../../HTML/Basic HTML Project/Build a Heart Icon/Heart_Icon.html>). Status: **HTML-only**.

The `width` attribute on `<path>` has no effect; the path's geometry comes from `d`, and the SVG's `viewBox` and outer `width`/`height` control the rendered size. This is a small teaching detail, not a rendering failure.

## F. Step-by-step explanation

### Adding a video

1. **Choose the element.** Use `<video>` for video with optional audio, or `<audio>` for sound only.
2. **Add `controls`.** Do not rely on autoplay or custom controls that do not exist.
3. **Add a poster.** A poster gives the visitor a visual preview before playback.
4. **List the sources.** Put the most broadly supported format first and add `type` hints.
5. **Add fallback text.** Put a short sentence between the opening and closing tags.
6. **Decide about `loop` and `muted`.** Both change the experience; use them intentionally.
7. **Test in more than one browser.** Format support and autoplay policies vary.
8. **Check the file size.** Large media files make the page slow.

### Adding an iframe

1. **Use the provider's embed URL.** A normal watch page is not the same as an embed URL.
2. **Write a specific `title`.** Describe the embedded content, not just "video player".
3. **Set `width` and `height`.** Use CSS for responsive sizing.
4. **Grant only the features you need.** Keep the `allow` list purposeful.
5. **Add `allowfullscreen` if the embed supports it.**
6. **Remove obsolete presentational attributes.** Use CSS for borders.
7. **Test the embed with keyboard navigation.** Confirm that focus can enter and leave it.

### Adding an SVG

1. **Start with `viewBox`.** It defines the coordinate system and makes the graphic scalable.
2. **Draw the shape with `<path>` or basic shapes.** Keep the path data readable.
3. **Set a fill or stroke.** Without either, the shape may be invisible.
4. **Decide whether it is informative.** If it conveys meaning, add a `<title>` and a role.
5. **Hide decorative SVGs.** Use `aria-hidden="true"` and `focusable="false"`.
6. **Test at different sizes.** A vector graphic should stay sharp.

## G. Repository implementations

| Implementation | Media feature | Status | Source |
| --- | --- | --- | --- |
| HTML Video Player | Four video formats, poster, controls, loop, muted | HTML-only | [Open](<../../HTML/Basic HTML Project/Build an HTML Video Player/HTML_Video_Player.html>) |
| Audio and Video Player | Video with nested source and an audio player | HTML-only | [Open](<../../HTML/Basic HTML Project/Build an HTML Audio and Video Player/Build an HTML Audio_and_Video_Player.html>) |
| Music Player | Three audio elements with headings and artist lines | HTML-only | [Open](<../../HTML/Basic HTML Project/Build an HTML Music Player/HTML_Music_Player.html>) |
| Video Compilation | Three YouTube iframes with `allow` and `referrerpolicy` | HTML-only | [Open](<../../HTML/Basic HTML Project/Build a Video Compilation Page/Video_Compilation_Page.html>) |
| iframe Video Display | A single embedded YouTube video | HTML-only | [Open](<../../HTML/Basic HTML Project/Build a Video Display Using iframe/Display Videos_in_an_iframe.html>) |
| Heart Icon | Inline SVG with `viewBox` and a path | HTML-only | [Open](<../../HTML/Basic HTML Project/Build a Heart Icon/Heart_Icon.html>) |

## H. Additional challenges

These are new practice tasks for this course; they are not requirements from the original exercises.

1. Remove `src=""` from the Audio and Video Player's `<video>` element and confirm that the nested `<source>` still loads.
2. Rewrite the three iframe titles in the Video Compilation page so each one names its topic.
3. Add fallback text to the Video Player's `<video>` element.
4. Replace `frameborder="0"` with a CSS rule and confirm that the iframe border disappears.
5. Add a `<title>` and `role="img"` to the Heart Icon, then change it to a decorative SVG with `aria-hidden="true"`. Compare the accessibility tree.
6. Create a simple SVG icon of your own using a `<circle>` and a `<path>`. Give it a `viewBox` and test it at three different sizes.
7. Add `loading="lazy"` to an image on a page that has several images. Observe when the browser requests it.
8. Write a short page that embeds one video and one audio file. Include controls, fallback text, and a poster.

## I. Common mistakes

- **Autoplaying with sound.** This surprises users and may be blocked by the browser.
- **Omitting `controls`.** The visitor cannot pause or adjust the media.
- **Using one file format for every browser.** Provide `<source>` alternatives where possible.
- **Forgetting fallback text.** A browser that cannot render the element shows nothing useful.
- **An iframe without a title.** The embedded region has no accessible name.
- **Using a normal YouTube watch URL in `src`.** Use the embed URL.
- **Keeping obsolete attributes such as `frameborder`.** Use CSS instead.
- **An SVG without `viewBox`.** It may not scale as expected.
- **An informative SVG with no accessible name.** Add a `<title>` or `aria-label`.
- **Hiding a focusable SVG with `aria-hidden`.** Do not hide something the keyboard can reach.
- **Assuming a poster image is a substitute for a video track.** The poster is only a preview.
- **Forgetting that remote media can disappear.** Production pages should control their own assets.

## J. Summary

Video and audio use `<source>` elements to offer formats and `controls` to keep the visitor in charge. Iframes embed another page and need a meaningful `title`, a deliberate `allow` list, and modern attributes. Inline SVG uses a coordinate system and paths; it can be informative or decorative, and its accessibility markup should match that role.

The repository's media pages are compact examples of the syntax. They also contain small lessons in what to clean up: an empty video `src`, generic iframe titles, an obsolete `frameborder`, and an SVG without an accessible name. These are the kinds of details that separate a working demo from a maintainable page.

## K. Next module

The HTML track ends here. Continue to the [CSS track](../css/01-css-fundamentals.md) to learn how to control the presentation of the structures you have built, starting with the cascade and the stylesheet link.
