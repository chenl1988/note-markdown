## prototype

- prototype 是函数的属性，当函数创建时会被自动创建
- prototype 属性的值是一个对象，里面只有一个 constructor 构造函数属性，其中存放的是函数本身

## `__proto__`

- `__proto__`是对象属性，当对象创建时会被自己创建
- `__proto__`的属性值 constructor 构造函数中存放的是构造对象使用的构造函数

---

## other

- function 关键字是语法糖，实际上还是 new Function()
- `let obj = {"name":"chenl"}`; {}也是语法糖，new Object()
- `let arr = [1,2]`; []也是语法糖，new Array()
