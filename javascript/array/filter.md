## filter

- 过滤

- **返回一个数组，只有当指定函数返回 true 时，相应的元素才会被包含在这个数组中**

```
const arr = [1, 2, 3, 4, 5, 6];
const filtered = arr.filter(el => el === 2 || el === 4);
console.log(filtered);
```
