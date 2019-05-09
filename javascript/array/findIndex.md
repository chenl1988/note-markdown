## findIndex

- 与 find 方法几乎完全相同，但不是返回第一个匹配的元素，而是返回第一个匹配元素的索引

```
const arr = ["Nick", "Frank", "Joe", "Frank"];
const foundIndex = arr.findIndex(el => el === "Frank");
console.log(foundIndex);
```
