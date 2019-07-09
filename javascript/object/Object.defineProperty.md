## Object.defineProperty

- Object.defineProperty 是 ES5 的新特性，作用是直接在一个对象上定义一个新的属性，或者修改一个已经存在的属性，并返回这个对象

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
