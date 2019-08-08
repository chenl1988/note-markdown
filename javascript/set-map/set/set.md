## set 数据类型（集合）

- es6 中引入了一个新的数据类型：Set,而 Set 与 Array 的结构是很类似的，且 Set 和 Array 可以相互进行转换

- set 对象允许存储任何类型的唯一值，无论是原始值或者是对象引用；类似数组，但成员的值都是唯一的，没有重复的值

- 在 set 的内部两个 NaN 相等

- Set 本身是一种构造函数，用来生成 Set 数据结构。

- set 的 size 属性，用于查看元素数量（与数组不同 set 没有 length）

- set 的操作方法

  - has(value)：判断集合中是否包含 value

  - add(value)：新增，相当于 array 中的 push

  - delete(value)：存在即删除集合中的 value

  - clear()：清空集合

- set 的遍历方法

  - keys()：返回一个包含集合中所有键的迭代器

  - values()：返回一个包含集合中所有值的迭代器

  - entries()：返回一个包含 Set 对象中所有元素的键值对迭代器

  - forEach(callbackFn,thisArg)：用于对集合成员执行 callbackFn 操作，如果提供了 thisArg 参数，回调中的 this 会是这个参数，没有返回值

- set 可以使用 map,filter 方法

* 将 set 数据结构转为数组有两种方式（from 或者展示运算符）

  - `let arr = Array.from(new Set([1,2,3,4,5,5]))`

  - `[...new Set([1,2,3,4,5,5])]`

```
let set = new Set();
set.add(1);
set.add(2);
set.add(5);
set.add(5);
for (let i of set) {
  console.log(i);
}

let set1 = new Set([1, 2, 3, 3]);
console.log([...set1]);

let arr = [1, 2, 3, 3, 6, 6];
console.log([...new Set(arr)]);

let a = Array.from(new Set(arr));
console.log(Object.prototype.toString.call(a)); //[object Array]

/* 判断是否包含key[object和set] */
let obj = {
  name: "cl",
  age: '12'
}
if (obj['name']) {
  console.log("object has key!")
}

let set2 = new Set([4, 5, 6, 4]);
if (set2.has(5)) {
  console.log("set has key!")
}
```
