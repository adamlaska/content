---
title: WeakSet.prototype.delete()
short-title: delete()
slug: Web/JavaScript/Reference/Global_Objects/WeakSet/delete
page-type: javascript-instance-method
browser-compat: javascript.builtins.WeakSet.delete
sidebar: jsref
---

The **`delete()`** method of {{jsxref("WeakSet")}} instances removes the specified element from this `WeakSet`.

{{InteractiveExample("JavaScript Demo: WeakSet.Prototype.delete()")}}

```js interactive-example
const weakset = new WeakSet();
const object = {};

weakset.add(object);

console.log(weakset.has(object));
// Expected output: true

weakset.delete(object);

console.log(weakset.has(object));
// Expected output: false
```

## Syntax

```js-nolint
weakSetInstance.delete(value)
```

### Parameters

- `value`
  - : The value to remove from the `WeakSet` object.

### Return value

`true` if an element in the `WeakSet` object has been removed successfully. `false` if the `value` is not found in the `WeakSet`. Always returns `false` if `value` is not an object or a [non-registered symbol](/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol#shared_symbols_in_the_global_symbol_registry).

## Examples

### Using the delete() method

```js
const ws = new WeakSet();
const obj = {};

ws.add(window);

ws.delete(obj); // Returns false. No obj found to be deleted.
ws.delete(window); // Returns true. Successfully removed.

ws.has(window); // Returns false. The window is no longer present in the WeakSet.
```

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- {{jsxref("WeakSet")}}
- {{jsxref("WeakSet.prototype.add()")}}
- {{jsxref("WeakSet.prototype.has()")}}
