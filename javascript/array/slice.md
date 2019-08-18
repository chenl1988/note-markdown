## slice

- slice()方法可以从已有的数组中返回选定的元素（返回截断后的新数组，不改变原数组）

  `arrayObject.slice(start,end)`

- 返回一个新的数组（不破坏原数据），包含从 start 到 end（不包含 end 元素）

- 从指定的起始位置和指定的结束位置之前返回数组的浅拷贝。如果未指定结束位置，则返回数组的其余部分。重要的是，此方法不会修改数组，而是返回所需的子集

```
let arr = ["a", "b", "c", "d", "e"];
const sliced = arr.slice(2, 4);
console.log(sliced);
console.log(arr);
```
