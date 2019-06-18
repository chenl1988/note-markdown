## 改变函数内部 this 指针的指向函数（bind，apply，call 的区别）

- 执行函数并将 this 的指向进行修改

- 通过 call 和 apply 改变函数的 this 指向，这两个函数的第一个参数都是一样的，表示要改变指向的那个对象，第二个参数，apply 是数组，而 call 则是 arg1,arg2...这种形式。

- 通过 bind 改变 this 作用域会返回一个新的函数，这个函数不会马上执行，需要调用执行（返回函数，柯里化）

- call 是 apply 方法的语法糖

---

- call,apply,bind 都是用来改变函数执行时上下文，可借它们实现继承
- call 和 apply 唯一区别是参数不一样，call 是 apply 的语法糖
- bind 是返回一个新函数，供以后调用

```
/*原生js实现bind方法*/

let a = {
  value: 1
}
function getValue(name, age) {
  console.log(this, "===")
  console.log(name);
  console.log(age);
  console.log(this.value);
  console.log(...arguments);
}
/* bind和其他两个方法作用也是一致的，只是该方法会返回一个函数，并且可以通过bind实现柯里化 */

/*
  柯里化是函数的一个比较高级的应用，接收函数作为参数的函数都可以叫做高阶函数（常常利用高阶函数来封装一些公共的逻辑）
  柯里化其实就是高阶函数的一种特殊用法，
  柯里化是指这样一个函数（假设叫做createCurry），他接收函数A作为参数，运行后能够返回一个新的函数。并且这个新的函数能够处理函数A的剩余参数
*/

/* 如何实现一个bind函数 */
Function.prototype.myBind = function (context) {
  if (typeof this !== 'function') {
    throw new TypeError('Error');
  }

  var _this = this;
  //args中存放的是调用myBind时候传入的参数
  var args = [...arguments].slice(1);
  /* bind返回的是方法 ,arguments为返回方法的参数*/
  return function F() {
    /* 可借它们实现继承 */
    if (this instanceof F) {
      return new _this(...args, ...arguments);
    }
    //arguments为返回方法F的参数
    return _this.apply(context, args.concat(...arguments))
  }
}

let bindRes = getValue.myBind(a, 'chenlong', '20', 'hahaha');
console.log(bindRes("33", "55"));


/*原生js实现call方法*/
Function.prototype.myCall = function (context) {
  var context = context || window;
  //给context添加一个属性

  context.fn = this;
  //将context后面的参数取出来
  var args = [...arguments].slice(1);

  var result = context.fn(...args);

  delete context.fn;
  return result;
}

getValue.myCall(a, 'cl', '25');


/*原生js实现apply方法*/
Function.prototype.myApply = function (context) {
  var context = context || window;
  context.fn = this;

  var result;
  //需要判断是否存在第二个参数
  //如果存在就将第二个参数展开
  if (arguments[1]) {
    result = context.fn(...arguments[1]);
  } else {
    result = context.fn();
  }
  delete context.fn;
  return result;
}
getValue.myApply(a, 'cl', '18');
```
