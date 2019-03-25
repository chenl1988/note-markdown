## ES6 Proxy

- 与 Object.defineProperty 相比 Proxy 有以下两个优点：
  - 可以劫持整个对象，并返回一个新对象
  - 有 13 种劫持操作

---

#### 什么是 Proxy

- Proxy 是 ES6 中新增的一个特性，翻译过来就是“代理”，用在这里表示由它来“代理”某些操作
- Proxy 能够以简洁易懂的方式控制外部对对象的访问。其功能非常类似于设计模式中的代理模式
- Proxy 可以理解成，在目标对象之前架设一层“拦截”，外界对该对象的访问，都必须先通过这层拦截，因此提供了一种机制，可以对外界的访问进行过滤和改写
- 使用 Proxy 的核心优点是可以交由它来处理一些非核心逻辑（如：读取或设置对象的某些属性前记录日志；设置对象的某些属性值前，需要验证；某些属性的访问控制等）。从而可以让对象只需关注于核心逻辑，达到关注点分离，降低对象复杂度等目的

---

#### 基本用法

- `let p = new Proxy(target,handler);`
- 参数 target 是用 Proxy 包装的被代理对象（可以是任何类型的对象，包括原生数组，函数，甚至是另一个代理）
- 参数 handler 是一个对，其声明了代理 target 的一些操作，其属性是当执行一个操作时定义代理的行为的函数
- p 是代理后的对象。当外界每次对 p 进行操作时，就会执行 handler 对象上的一些方法。Proxy 共有 13 种劫持操作，handler 代理的一些常用的方法有如下几个：
  - get: 读取
  - set: 修改
  - has: 判断对象是否有该属性
  - construct: 构造函数

```
let obj = {};
let handler = {
  get(target, property) {
    console.log(`${property}被读取----`);
    return property in target ? target[property] : 3;
  },
  set(target, property, value) {
    console.log(`${property}被设置为${value}---`);
    target[property] = value;
  }
}

let p = new Proxy(obj, handler);
p.name = "tom";
p.age;
console.log(p.name);
console.log(p.age);

/* p读取属性的值时，实际上执行的是handler.get() : 在控制台输出信息，并且读取被代理对象obj的属性 */
/* p设置属性的值时，实际上执行的是handler.set() : 在控制台输出信息，并且读取被代理对象obj的属性的值 */
```
