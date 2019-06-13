## reduce

- reduce() 方法接收一个函数作为**累加器（accumulator）**，数组中的每个值（从左到右）开始缩减，最终为一个值。
- reduce 为数组中的每一个元素依次执行回调函数，不包括数组中被删除或从未被赋值的元素，接受四个参数：初始值（或者上一次回调函数的返回值），当前元素值，当前索引，调用 reduce 的数组。

- 语法:arr.reduce(callback,[initialValue])

  - callback （执行数组中每个值的函数，包含四个参数）
    - previousValue （上一次调用回调返回的值，或者是提供的初始值（initialValue））
    - currentValue （数组中当前被处理的元素）
    - index （当前元素在数组中的索引）
    - array （调用 reduce 的数组）

  -initialValue （作为第一次调用 callback 的第一个参数。）

```
const arr = [1, 2, 3, 4, 5, 6];
const reduced = arr.reduce((total, current) => total + current);
console.log(reduced);
```
