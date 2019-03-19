## construstor 构造函数

- 实际上并不存在所谓的“构造函数”，只有对于函数的“构造调用”
- 构造函数本身也是函数，但是内部使用了this变量。对构造函数使用new操作符，就能生成实例。并且this变量会绑定在实例对象上。
```
function Cat(name,color){
  this.name = name;
  this.color = color;
}

var cat1 = new Cat("大毛","黄色");
console.log(cat1.name,cat1.color);
var cat2 = new Cat("二毛","橘色");
console.log(cat2.name,cat2.color);

//这时cat1和cat2会自动含有一个constructor属性，指向它们的构造函数（cat1和cat2就有了内在的联系）
```
- constructor 返回创建实例对象时构造函数的引用。此属性的值是对函数本身的引用，不是一个包含函数名称的字符串
- constructor 属性值对于引用类型来说是可以修改的，但是对于基本类型来说是只读的
- Object,Array...这些都是原生的构造函数
- 任何函数，通过 new 操作符来调用，就可以作为构造函数；而任何函数，如果不通过 new 操作符来调用，那它跟普通函数没有区别

## 构造函数扩展

- var a = {};语法糖 var a = new Object();
- var a = [];语法糖 var a = new Array();
- function foo(){...};语法糖 var foo = new Function();
