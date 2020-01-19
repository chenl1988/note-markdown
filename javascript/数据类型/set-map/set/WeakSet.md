## WeakSet

- WeakSet 和 Set 结构类似，也是不重复的值的集合，但 WeakSet 的成员只能是对象

- WeakSet 对象允许将**弱引用对象**储存在一个集合中

- WeakSet 对象中储存的对象值都是被弱引用的，即垃圾回收机制不考虑 WeakSet 对该对象的应用，如果没有其他变量或属性引用这个对象值，则这个对象将会被垃圾回收掉（不考虑该对象还存在于 WeakSet 中）

* WeakSet 的 API：

  - add():增加
  - delete():删除
  - has():是否存在

* WeakSet 没有 size 属性，因为它不可遍历（因为 WeakSet 的成员都是弱引用，随时可以消失，成员是不稳定的）

* WeakSet 的用处：

  - **使用 WeakSet 储存 DOM 节点，就不用担心节点从文档中移除时，会引发内存泄漏（即在移除的节点上绑定的 click 等事件）**

  - 下面的代码保证了 Foo 的实例方法，只能在 Foo 的实例上调用。这个使用 WeakSet 的好处是，foos 对实例的引用，不会被讲稿内存回收机制，所以删除实例的时候，不用考虑 foos，也不会出现内存泄漏

  ```
  const foos = new WeakSet();
  class Foo {
    constructor() {
      foos.add(this);
    }
    method() {
      if (!foos.has(this)) {
        throw new TypeError('Foo.prototype.method 只能在Foo的实例上调用');
      }
    }
  }
  ```

```
let arr = [
  [1, 2],
  [3, 4]
];
let ws = new WeakSet(arr);
console.log(ws);
```
