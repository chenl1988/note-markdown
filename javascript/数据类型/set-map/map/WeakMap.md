## WeakMap

- WeakMap 对象是一组键值对的集合，其中的键是弱引用对象，而值可以是任意。

- 注意，WeakMap 弱引用的只是键名，而不是键值。键值依然是正常引用。

- WeakMap 中，每个键对自己所引用对象的引用都是弱引用，在没有其他引用和该键引用同一对象，这个对象将会被垃圾回收（相应的 key 则变成无效的），所以，WeakMap 的 key 是不可枚举的。

- 方法：
  - has(key)：判断是否有 key 关联对象
  - get(key)：返回 key 关联对象（没有则则返回 undefined）
  - set(key)：设置一组 key 关联对象
  - delete(key)：移除 key 的关联对象
