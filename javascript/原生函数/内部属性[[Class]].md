## 内部属性[[Class]]

- 所有的typeof返回值为“object”的对象（如数组）都包含一个内部属性`[[Class]]`（可以把它看作一个内部的分类，而非传统的面向对象意义上的类），这个属性无法直接访问，一般通过Object.prototype.toString(..)来查看
```
Object.prototype.toString.call([1,2,4]);
//[Object Array]

Object.prototype.toString。call(/regex-literal/i);
//[Object RegExp]
```
- 虽然Null()和Undefined()这样的原生构造函数不存在，但是内部`[[Class]]`属性仍然是"Null"和"Undefined"
- 其他基本类型的情况有所不同，通常称为“包装boxing”-,基本类型值被各自的封装对象自动包装，所以它们的内部`[[Class]]`属性值分别为"String","Number","Boolean"
  