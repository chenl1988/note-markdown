## typeof 和 instanceof

- typeof**能够正确的判断基本数据类型**，但是除了 null(typeof null 输出的是对象)
- instanceof 可以准确的判断复杂数据类型，但是不能正确判断基本数据类型
  - instanceof 是通过原型链判断的，A instanceof B:在 A 的原型链中层层查找，是否有原型等于 B.prototype，如果一直找到 A 的原型链的顶端（null;即：Object.prototype.**proto**）,仍然不等于 B.prototype 那么返回 false，否则返回 true。

```
/*
 * instanceof的实现代码
 * L:表示左表达式
 * R:表示右表达式
 */
function instance_of(L, R) {
  var O = R.prototype; //取R的显示原型
  L = L.__proto__; //取L的隐式原型
  while (true) {
    //已经找到栈顶
    if (L === null) {
      return false;
    }
    // 当O严格等于L时，返回true
    if (O === L) {
      return true;
    }
    // 继续向上一层原型链查找
    L = L.__proto__;
  }
}
```
