## 用ES5实现数组的map方法

- 核心要点：
  - 回调函数的参数有哪些，返回值如何处理
  - 不修改原来的数组

```
//map方法，迭代数组中的元素，为数组中的元素执行回调函数，并将结果放到新的数组中返回
Array.prototype.myMap = function(fn,context){
  var arr = Array.prototype.slice.call(this); ////由于是ES5所以就不用...展开符了
  var mapedArr = []; //返回新数组
  for(var i=0;i<arr.length;i++){
    //为数组中的每一个元素执行fn回调函数
    mapedArr.push(fn.call(context,arr[i],i,this));
  }
  return mapedArr;
}

let arr = [1,2,3];
const maped = arr.myMap(function(el){
  return el+20;
});
console.log(maped);
```