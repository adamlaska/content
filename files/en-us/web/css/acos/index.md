---
title: acos()
slug: Web/CSS/acos
page-type: css-function
browser-compat: css.types.acos
sidebar: cssref
---

The **`acos()`** [CSS](/en-US/docs/Web/CSS) [function](/en-US/docs/Web/CSS/CSS_Values_and_Units/CSS_Value_Functions) is a trigonometric function that returns the inverse cosine of a number between `-1` and `1`. The function contains a single calculation that returns the number of radians representing an {{cssxref("&lt;angle&gt;")}} between `0deg` and `180deg`.

## Syntax

```css
/* Single <number> values */
transform: rotate(acos(-0.2));
transform: rotate(acos(2 * 0.125));

/* Other values */
transform: rotate(acos(pi / 5));
transform: rotate(acos(e / 3));
```

### Parameters

The `acos(number)` function accepts only one value as its parameter.

- `number`
  - : A calculation which resolves to a {{cssxref("&lt;number&gt;")}} between `-1` and `1`.

### Return value

The inverse cosine of an `number` will always return an {{cssxref("&lt;angle&gt;")}} between `0deg` and `180deg`.

- If `number` is less than `-1` or greater than `1`, the result is `NaN`.
- If `number` is exactly `1`, the result is `0`.

## Formal syntax

{{CSSSyntax}}

## Examples

### Rotate elements

The `acos()` function can be used to {{cssxref("transform-function/rotate", "rotate")}} elements as it return an {{cssxref("&lt;angle&gt;")}}.

#### HTML

```html
<div class="box box-1"></div>
<div class="box box-2"></div>
<div class="box box-3"></div>
<div class="box box-4"></div>
<div class="box box-5"></div>
```

#### CSS

```css hidden
body {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 50px;
}
```

```css
div.box {
  width: 100px;
  height: 100px;
  background: linear-gradient(orange, red);
}
div.box-1 {
  transform: rotate(acos(1));
}
div.box-2 {
  transform: rotate(acos(0.5));
}
div.box-3 {
  transform: rotate(acos(0));
}
div.box-4 {
  transform: rotate(acos(-0.5));
}
div.box-5 {
  transform: rotate(acos(-1));
}
```

#### Result

{{EmbedLiveSample('Rotate elements', '100%', '200px')}}

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- {{CSSxRef("sin")}}
- {{CSSxRef("cos")}}
- {{CSSxRef("tan")}}
- {{CSSxRef("asin")}}
- {{CSSxRef("atan")}}
- {{CSSxRef("atan2")}}
