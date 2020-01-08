# JS数组的高阶函数——基础篇

- 一个函数可以接收另一个函数作为参数或者返回值为一个函数，这种函数就称之为高阶函数。

## 数组中的高阶函数

### map：
  - 接受两个参数，一个是回调函数，一个是回调函数的this值（可选）；其中，回调函数被默认传入三个值，依次为当前元素、当前索引、整个数组
  - **创建一个新数组，其结果是该数组中的每个元素都调用一个提供的函数后返回的结果**
  - 对原来的数组没有影响
```
let nums = [1,2,3];
let obj = {val:5};
let newNums = nums.map(function(item,index,array){
  return item + index + array[index] + this.val;
},obj);
console.log(newNums);

```
### reduce：
  - 为数组中的每一个元素依次执行回调函数，不包括数组中被删除或从未被赋值的元素
  - 接收两个参数，一个为回调函数，另一个为初始值。回调函数中四个默认参数，
  依次为积累值、当前值、当前索引、调用 reduce的数组；
  （如果没有提供初始值reduce会从索引1的地方开始执行callback，跳过第一个索引。如果提供）
  - reduce的简单用法是数组求和，求乘积
  - reduce的高级用法：
      计算数组中每个元素出现的次数、数组去重、
      将二维数组转化为一维、将多维数组转换为一维、对象里的属性求和
```
//数组求和
let nums2 = [1,2,3];
let newNums2 = nums2.reduce(function(preSum,curVal,array){
  return preSum + curVal;
},0);
console.log(newNums2);
//数组乘积
var mul = nums2.reduce((pre,cur)=>pre*cur);
console.log(mul);
// 计算数组中每个元素出现的次数
let names = ['Alice', 'Bob', 'Tiff', 'Bruce', 'Alice'];
let nameNum = names.reduce((pre,cur)=>{
  if(cur in pre){
    pre[cur]++;
  }else{
    pre[cur] = 1;
  }
  return pre;
},{})
console.log(nameNum);
/* 
数组去重
  push和concat两种方法：
  - push返回的是数组的长度，push是在原数组是进行修改；
  - concat是把原数组复制到一个新的数组,然后在新数组上进行操作，所以不会改变原数组的值)
*/
let arr = [1,2,3,4,4,1];
let newArr = arr.reduce((pre,cur)=>{
  if(!pre.includes(cur)){
    return pre.concat(cur);
  }else{
    return pre;
  }
},[]);
console.log(newArr);

let arr4 = [1,2,3,4,4,1];
let newArr4 = arr4.reduce((init,cur)=>{
  if(!init.includes(cur)){
    init.push(cur);
  }
  return init;
},[]);
console.log(newArr4);
// 将二维数组转化为一维
let arr2 = [[0, 1], [2, 3], [4, 5]];
let newArr2 = arr2.reduce((pre,cur)=>{
  return pre.concat(cur);
},[]);
console.log(newArr2);
// 将多维数组转化为一维
let arr3 = [[0, 1], [2, 3], [4,[5,6,7]]];
let newArr3 = function(arr){
  return arr.reduce((pre,cur)=>pre.concat(Array.isArray(cur)?newArr3(cur):cur),[]);
}
console.log(newArr3(arr3));
// 对象属性求和
var result = [
  {
      subject: 'math',
      score: 10
  },
  {
      subject: 'chinese',
      score: 20
  },
  {
      subject: 'english',
      score: 30
  }
];
let sum = result.reduce((init,cur)=>{
  console.log(init);
  return init +　cur.score;
},0);
console.log(sum);

```
### filter：
  - 接收一个函数参数，这个函数接受一个默认参数，就是当前元素。这个作为参数的函数返回值为一个布尔类型，决定元素是否保留
  - filter方法返回为一新的数组，这个数组里面包含参数里面所有被保留的项
```
// 保留奇数
let nums5 = [1,2,3];
let oddNums = nums5.filter(item=> {
  //console.log(item % 2);
  return item % 2;
});
console.log(oddNums);
```
### sort：
  - 一个用于比较的函数，它有两个默认参数，分别是代表比较的两个元素

  - 当比较函数返回值大于0，则a在b的后面，即a的下标应该比b大
  - 反之，则a在b的后面，即a的下标比b小
  - 整个过程就完成了一次升序的排列

  - sort()不传函数参数时，是将数字转换为字符串，然后根据unicode值进行升序反序，
  也就是根据字符串的比较规则进行升序排序
```
let nums6 = [2,3,1];
let flag = nums6.sort((a,b)=>{
  return a>b?1:a<b?-1:0;
})
console.log(flag);
```