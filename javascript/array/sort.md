## sort

- 根据提供的函数对数组进行排序。这个方法**就地修改数组**。**如果函数返回负数或 0，则顺序保持不变。如果返回正数，则交换元素顺序**

```
let arr = [1, 8, 3, -1, 8, 2];
const sorter = (firstEl, secondEl) => firstEl - secondEl;
arr.sort(sorter);
console.log(arr);

/*数组乱序*/
let arr = [1,2,3,4,5,6,7,8];

arr.sort(function(){
  return Math.random() - 0.5;
})

console.log(arr);
```
