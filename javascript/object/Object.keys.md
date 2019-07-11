## Object.keys

- Object.key()可以获取对象的 key，必须将属性的 enumerable 设置为 true 才能获取，否则返回的是空数组

```
let obj = {};
Object.defineProperty(obj, "name", {
  enumerable: true,
  value: "ccc"
})
console.log(Object.keys(obj));
```
