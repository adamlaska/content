---
title: offset-rotate
slug: Web/CSS/offset-rotate
page-type: css-property
browser-compat: css.properties.offset-rotate
sidebar: cssref
---

The **`offset-rotate`** [CSS](/en-US/docs/Web/CSS) property defines the orientation/direction of the element as it is positioned along the {{cssxref("offset-path")}}.

{{InteractiveExample("CSS Demo: offset-rotate")}}

```css interactive-example-choice
offset-rotate: auto;
```

```css interactive-example-choice
offset-rotate: 90deg;
```

```css interactive-example-choice
offset-rotate: auto 90deg;
```

```css interactive-example-choice
offset-rotate: reverse;
```

```html interactive-example
<section class="default-example" id="default-example">
  <div class="transition-all" id="example-element"></div>
  <button id="playback" type="button">Play</button>
</section>
```

```css interactive-example
#example-element {
  width: 24px;
  height: 24px;
  background: #2bc4a2;
  offset-path: path("M-70,-40 C-70,70 70,70 70,-40");
  animation: distance 8000ms infinite linear;
  animation-play-state: paused;
  clip-path: polygon(0% 0%, 70% 0%, 100% 50%, 70% 100%, 0% 100%, 30% 50%);
}

#example-element.running {
  animation-play-state: running;
}

#playback {
  position: absolute;
  top: 0;
  left: 0;
  font-size: 1em;
}

@keyframes distance {
  0% {
    offset-distance: 0%;
  }
  100% {
    offset-distance: 100%;
  }
}

/* Provides a reference image of what path the element is following */
#default-example {
  position: relative;
  background-position: calc(50% - 12px) calc(50% + 14px);
  background-repeat: no-repeat;
  background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="-75 -45 150 140" width="150" height="140"><path d="M-70,-40 C-70,70 70,70 70,-40" fill="none" stroke="lightgrey" stroke-width="2" stroke-dasharray="4.5"/></svg>');
}
```

```js interactive-example
window.addEventListener("load", () => {
  const example = document.getElementById("example-element");
  const button = document.getElementById("playback");

  button.addEventListener("click", () => {
    if (example.classList.contains("running")) {
      example.classList.remove("running");
      button.textContent = "Play";
    } else {
      example.classList.add("running");
      button.textContent = "Pause";
    }
  });
});
```

> [!NOTE]
> Early versions of the spec called this property `motion-rotation`.

## Syntax

```css
/* Follow the path direction, with optional additional angle */
offset-rotate: auto;
offset-rotate: auto 45deg;

/* Follow the path direction but facing the opposite direction of `auto` */
offset-rotate: reverse;

/* Keep a constant rotation regardless the position on the path */
offset-rotate: 90deg;
offset-rotate: 0.5turn;

/* Global values */
offset-rotate: inherit;
offset-rotate: initial;
offset-rotate: revert;
offset-rotate: revert-layer;
offset-rotate: unset;
```

- `auto`
  - : The element is rotated by the angle of the direction of the {{cssxref("offset-path")}}, relative to the positive x-axis. This is the default value.
- {{cssxref("&lt;angle&gt;")}}
  - : The element has a constant clockwise rotation transformation applied to it by the specified rotation angle.
- `auto <angle>`
  - : If `auto` is followed by an {{cssxref("&lt;angle&gt;")}}, the computed value of the angle is added to the computed value of `auto`.
- `reverse`
  - : The element is rotated similar to `auto`, except it faces the opposite direction. It is the same as specifying a value of `auto 180deg`.

## Formal definition

{{cssinfo}}

## Formal syntax

{{csssyntax}}

## Examples

### Setting element orientation along its offset path

#### HTML

```html
<div></div>
<div></div>
<div></div>
```

#### CSS

```css
div {
  width: 40px;
  height: 40px;
  background: #2bc4a2;
  margin: 20px;
  clip-path: polygon(0% 0%, 70% 0%, 100% 50%, 70% 100%, 0% 100%, 30% 50%);
  animation: move 5000ms infinite alternate ease-in-out;

  offset-path: path("M20,20 C20,50 180,-10 180,20");
}
div:nth-child(1) {
  offset-rotate: auto;
}
div:nth-child(2) {
  offset-rotate: auto 90deg;
}
div:nth-child(3) {
  offset-rotate: 30deg;
}

@keyframes move {
  100% {
    offset-distance: 100%;
  }
}
```

#### Result

{{EmbedLiveSample('Setting_element_orientation_along_its_offset_path', '100%', '200')}}

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- {{cssxref("offset")}}
- {{cssxref("offset-anchor")}}
- {{cssxref("offset-distance")}}
- {{cssxref("offset-path")}}
- {{cssxref("offset-position")}}
