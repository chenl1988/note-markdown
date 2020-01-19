# instanceof

- instanceof的原理是基于原型链的查询，只要处于原型链中，判断永远为true
```
const Person = function(){}
const p1 = new Person();
p1 instanceof Person //true

var str1 = "hello world";
str instanceof String //false

var str2 = new String("hello");
str2 instanceof String //true
```