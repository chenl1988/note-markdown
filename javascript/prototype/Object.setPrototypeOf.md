## Object.setPrototypeOf

- 在ES6之前，只能通过设置`.__proto__`属性来实现修改对象的`[[prototype]]`属性，但是这个方法并不是标准并且无法兼容所有浏览器。
- ES6添加了辅助函数Object.setPrototypeOf(..)，可以用标准并且可靠的方法来修改关联