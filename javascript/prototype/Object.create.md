## Object.create

- 调用Object.create(..)会凭空创建一个“新”对象并把新对象内部的`[[prototype]]`关联到指定的对象；这样可以充分发挥`[[prototype]]`机制的威力（委托）并且避免不必要的麻烦（比如使用new的构造函数调用会生成.prototype和constructor引用）