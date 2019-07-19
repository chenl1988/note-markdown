## DocumentFragment

- vue 进行编译时，就是将挂载目标的所有子节点支持（通过 append 方法，DOM 中的节点会被自动删除）到 DomcumentFragment 中，经过一番处理后，再将 DocumentFragment 整个返回插入挂载目标
