## 如何判断一个变量是否是数组

- 使用 Array.isArray 判断，如果返回 true，说明是数组
- 使用 instanceof Array 判断，如果返回 true，说明是数组
- 使用 Object.prototype.toString.call 判断，如果值是[object Array]，说明是数组
- 通过 constructor 来判断，如果是数组，那么 arr.constructor === Array （不准确，因为代码可以指定 obj.constructor = Array）

```
function fn() {
  console.log(Array.isArray(arguments)); //false
  console.log(Array.isArray([1, 2, 3, 4])); //true
  console.log(arguments instanceof Array); //false
  console.log([1, 2, 3, 4] instanceof Array); //true
  console.log(Object.prototype.toString.call(arguments)); //[Object Arguments]
  console.log(Object.prototype.toString.call([1, 2, 3, 4])); //[Object Array]
  console.log(arguments.constructor === Array); //false
  arguments.constructor = Array;
  console.log(arguments.constructor === Array); //true
  console.log(Array.isArray(arguments)); //false
}
fn(1, 2, 3, 4);
```
