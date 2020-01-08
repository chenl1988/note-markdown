## ES5 实现数组 map 方法

```
Array.prototype.selfMap = function (fn, context) {
  let arr = this;
  if (typeof fn !== "function") {
    throw new TypeError(`${fn} is not a function`);
  }

  let mappedArr = [];
  for (let i = 0; i < arr.length; i++) {
    /* ES6t箭头函数this指向 */
    mappedArr.push(fn.call(context, arr[i], i, this));
  }
  return mappedArr;
}

let arr = [1, 2, 3, 4];
let mapped = arr.selfMap(function (el) {
  return el + 20;
});

let mapped_2 = arr.selfMap(el => {
  return el + 10;
})
console.log(mapped);
console.log(mapped_2);
```
