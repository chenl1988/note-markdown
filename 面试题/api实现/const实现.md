# 在ES5环境下实现const

## const实现的关键在于Object.defineProperty(); 这个API用于给一个对象上增加或修改属性，通过配置属性标识符，可以精确的控制属性行为

### Object.defineProperty(obj, prop, desc)
  - obj: 要定义属性的对象
  - prop: 要定义或修改的属性名称
  - desc: 将被定义或修改的属性描述符
  - 属性描述符：
    - value: 该属性对应的值。
    - get: 一个给属性提供getter的方法
    - set: 一个给属性提供setter的方法。当属性值修改时，触发执行该方法
    - writable: 当且仅当该属性的writable为true时，value才能被赋值运算符改变，默认为false
    - enumerable: 定义了对象的属性是否可以在for...in和Object.keys()中被枚举
    - configurable: 表示对象的属性是否可以被删除，以及除value和writable特性外的其他特性是否可以被修改

### 对于const不可修改的特性，可以通过设置writable属性来实现
```
function _const(key, value){
  const desc = {
    value,
    writable: false
  }
  Object.defineProperty(window, key, desc)
}

_const('obj', {a: 1}) //定义obj
obj.b = 2; //可以正常给obj的属性赋值
obj = {} //抛出错误，提示对象read-only
```