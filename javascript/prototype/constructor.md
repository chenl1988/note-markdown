## construstor 构造函数

- 构造函数本身也是函数，只不过可以用来创建对象而已
- Object,Array...这些都是原生的构造函数
- 任何函数，通过 new 操作符来调用，就可以作为构造函数；而任何函数，如果不通过 new 操作符来调用，那它跟普通函数没有区别

## 构造函数扩展

- var a = {};语法糖 var a = new Object();
- var a = [];语法糖 var a = new Array();
- function foo(){...};语法糖 var foo = new Function();
