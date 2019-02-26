## instanceof 

- instanceof运算符，验证原型与实例对象之间的关系
- instanceof的意思是：左边操作数的`__proto__`原型链上是否包括右边操作数的prototype
  - 即如果有表达式 L instanof R 则运算结果是：`L.__proto__.__proto__... === R.prototype`;
  - 运算符左边最终结果是instanceof运算时会递归查找L的原型链