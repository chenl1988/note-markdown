## reduce

- reduce() 方法接收一个函数作为累加器（accumulator），数组中的每个值（从左到右）开始合并，最终为一个值
- reduce 为数组中的每个元素依次执行回调函数，回调函数包含四个参数：
  - 初始值（或者上一次回调函数的返回值）
  - 当前元素值
  - 当前索引
  - 调用 reduce 的数组

```
//将数组所有项相加
var res = [0, 1, 2, 3, 4, ].reduce(function (previousValue, currentValue, index, array) {
  return previousValue + currentValue;
})
console.log(res);

//数据扁平化
var flattened = [
  [0, 1],
  [2, 3],
  [3, 4]
].reduce(function (a, b) {
  return a.concat(b);
})
```
