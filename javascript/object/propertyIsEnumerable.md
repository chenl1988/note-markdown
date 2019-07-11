## propertyIsEnumerable

- 通过 propertyIsEnumerable 可以判断定义的对象是否可枚举

```
let obj = {};
Object.defineProperty(obj, "name", {
  value: "ddd"
});
console.log(obj.propertyIsEnumerable("name")); //false

let obj2 = {};

Object.defineProperty(obj2, "name", {
  enumerable: true,
  value: "eee"
})

console.log(obj2.propertyIsEnumerable("name"));
```
