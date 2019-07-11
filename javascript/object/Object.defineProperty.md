## Object.defineProperty

- Object.defineProperty 是 ES5 的新特性，**作用是直接在一个对象上定义一个新的属性，或者修改一个已经存在的属性，并返回这个对象**

- Object.defineProperty(obj,prop,descriptor)中的 descriptor 有如下几个参数：
  - configurable: 当该属性的 configurable 为 true 时，该属性描述符才能够被改变，同时该属性也能从对应的对象上被删除。默认为 false
  - enumerable：当该属性的 enumerable 为 true 时，该属性才能够出现在对象枚举属性中。默认为 false
  - value：该属性对应的值。可以是任何有效的 JavaScript 值（数值，对象，函数等）。默认为 undefined
  - writable：当该属性的 writable 为 true 时，value 才能被赋值运算符改变。默认为 false
  - get：一个给属性提供 getter 的方法，如果没有 getter 则为 undefined。当访问该属性时，该方法会被执行，方法执行时没有参数传入，但是会传入 this 对象（由于继承关系，这里的 this 并不一定是定义该属性的对象）。默认为 undefined
  - set：一个给属性提供 setter 的方法，如果没有 setter 则为 undefined。当属性值修改时，触发执行该方法。该方法将接受唯一参数，即该属性新的参数值。默认为 undefined
  - （在 descriptor 中不能同时设置访问器(get 和 set)和 value）

```
var d = Date.prototype;
/* 通过defineProperty为Date.prototype增加一个属性 */
Object.defineProperty(d, "year", {
  /* 为year属性增加getter、setter方法 */
  get: function () {
    return this.getFullYear();
  },
  set: function (y) {
    return this.setFullYear(y);
  }
})

var now = new Date();
console.log(now.year);
now.year = 2014;
console.log(now);
```

- 完整示例代码如下：

```
Object.defineProperty(obj,prop,{
  configurable:true,
  enumerable:true,
  writable:true,
  value:'',
  get:function(){},
  set:function(){}
})
```
