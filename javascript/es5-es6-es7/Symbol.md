## Symbol(符号)

- 符号Symbol是具有唯一性的特殊值（并非绝对），用它来对象属性不容易导致重名。该类型的引入主要源于ES6的一些特殊构造，此符呈也可以自行定义

- 符号可以用作属性名，但无论是在代码还是在开发控制台中都无法查看和访问它的值，只会显示为诸如Symbol(Symbol.create)这样的值。

- ES6中有一些预定义符号，以Symbol的静态属性形式出现，如Symbol.create,Symbol.iterator等
  `obj[Symbol.iterator] = function(){ /* .. */ }`

- 可以使用Symbol(...)原生构造函数来自定义符号。但它比较特殊，不能带new关键字，否则会出错

```
var mysym = Symbol(" my own symbol ");
console.log(mysym); //Symbol( my own symbol )
console.log(mysym.toString()); //Symbol( my own symbol )
console.log(typeof mysym); //symbol

var a = {};
a[mysym] = "foobar"
console.log(a[mysym]); //foobar
console.log(Object.getOwnPropertySymbols(a)); //[Symbol( my own symbol )]
```
- Symbol主要用于私有或特殊属性。很多开发人员喜欢用它来替代有下划线的前缀属性，而下划线前缀通常用于命名私有或特殊属性
- Symbol（符号）并非对象，而是一种简单标量基本类型