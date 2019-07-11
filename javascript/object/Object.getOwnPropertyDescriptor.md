## Object.getOwnPropertyDescriptor

- 使用 Object.getOwnPropertyDescriptor 可以查看对象上属性的枚举类型值

```
let obj = {};
Object.defineProperty(obj, "name", {
  value: "aaaa"
});

console.log(Object.getOwnPropertyDescriptor(obj, "name"));

let obj2 = {};

Object.defineProperty(obj2, "name", {
  enumerable: true,
  writable: true,
  value: "bbb"
})
console.log(Object.getOwnPropertyDescriptor, "name");
```
