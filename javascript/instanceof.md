# instanceof

- 可以在实例的**原型对象链**中找到该**构造函数的prototype属性所指向的原型对象**，就返回true.

- 实现一个instanceof

```
function myInstanceof(left,right){
  // 基本数据类型直接返回false
  if(typeof left !== 'object' || left ===null) return false;

  // getPrototypeOf是Object对象自带的一个方法，能够拿到参数的原型对象
  let proto = Object.getPrototypeOf(left);

  while(true){
    //查找到尽头，还没有找到
    if(proto == null) return false;
    //找到相同的原型对象
    if(proto == right.prototype) return true;

    //继续在原型链上查找
    proto = Object.getPrototypeOf(proto);

  }
}

console.log(myInstanceof("111", String));
console.log(myInstanceof(new String('111'),String));
```