## every

- every()：方法对数组中的每一项运行给定函数，如果该函数对每一项都返回 true，则返回 true

- 接收两个参数，第一个是函数（函数接收三个参数：数组当前项的值，当前项在数组中的索引，数组对象本身），第二个参数是执行第一个参数的作用域对象（也就是函数中的 this 所指向的值）如果不设置默认为 undefined

- every()方法不会修改原数组

- 与之对应的是 some()方法

```
let arr = [1, 2, 3, 4, 5, 6, ];
console.log(arr.every((item, index, array) => {
  console.log(`item=${item},index=${index},array=${array}`);
  return item > 3;
}));//false
```
