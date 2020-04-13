# 手写call()

## call()使用一个指定的this值和单独给出的一个或多个参数来调用一个函数；
  - call的原理比较简单，由于函数的this指向它的直接调用者，我们变更调用者即完成this指向的变更

```
Function.prototype.myCall = function(thisArg, ...args){
  const fn = Symbol('fn'); //声明一个独有的Symbol属性，防止覆盖已有属性
  thisArg = thisArg || window; //若没有传入this，默认绑定window对象
  thisArg[fn] = this; //this指向调用call对象，即我们要改变this指向的函数
  const result = thisArg[fn](...args); //执行当前函数
  delete thisArg[fn]; //删除我们声明的fn属性
  retun  result; //返回函数执行结果
}

function foo(){
  console.log(this.name);
}
const obj = {
  name: 'test';
}

foo.myCall(obj);
```