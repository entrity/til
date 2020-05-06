In Javascript, you can partition values from an Object. It requires the keyword `var|let|const`

```js
var myObj = {a: 1, b: 2, c: 3, d: 4, e: 5};
var {a, b, c, ...other} = myObj;
// => a = 1, b = 2, b = 3, other = {d: 4, e: 5}
```
