## DocumentFragment

- DocumentFragment 文档片断接口，表示一个没有父级文件的最小文档对象。它被作为轻量版的 Document 使用，用于存储已经排好版的或尚未打理好格式的 XML 片段。最大区别是因为 DocumentFragment 不是真实 DOM 树的一部分，它的变化不会触发 DOM 树的（重新渲染），且不会导致性能等问题

- DocumentFragment(文档片断)可以看作节点容器，它可以包含多个子节点，当我们将它插入到 DOM 中时，只有它的子节点会插入目标节点，所以把它看作一组节点的容器

- 使用 DocumentFragment 处理节点，速度和性能远远优于直接操作 DOM

- 最常用的方法是使用文档片段作为参数（例如：任何 node 接口类似 Node.appendChild 和 Node.insertBefor 的方法），这种情况下被添加（append）或被插入（inserted）的是片段的所有子节点，不非片段本身。因为所有的节点会被一次插入到文档中，而这个操作仅发生一个重新渲染的操作，而不是每个节点分别被插入到文档中，因为后者会发生多少重新渲染的操作。

- 可以使用 document.createDocumentFragment()方法或者构造函数来创建一个空的 DomcumentFragment

- documentFragment 的 nodeType 值为 11，nodeName 的值为#document-fragment

---

- vue 进行编译时，就是将挂载目标的所有子节点支持（通过 append 方法，DOM 中的节点会被自动删除）到 DomcumentFragment 中，经过一番处理后，再将 DocumentFragment 整个返回插入挂载目标
