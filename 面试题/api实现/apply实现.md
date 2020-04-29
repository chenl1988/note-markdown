# 手写apply()

## apply方法的功能是修改this的指向；apply方法调用一个具有指定this的函数，以及作为一个数组（或者类数组）提供的参数
  - 与call方法的区别只是接收的第二个参数

```
Function.prototype.myApply = function(thisArg, argArr){
  const fn = Symbol("fn");
  thisArg = thisArg || window;
  thisArg[fn] = this;
  argArr = argArr || []
  const result = thisArg[fn](argArr)
  delete thisArg[fn];
  return result;
};

const obj = {
  name: "applyTest"
}

function foo(){
  console.log(this.name);
}

foo.myApply(obj);
```
