## virtual dom 虚拟节点

- virtual dom 也就是虚拟节点。它是通过 javascript 的 Object 对象模拟 DOM 中的节点，然后再通过特定的 render 方法将其渲染成真实的 DOM 节点

- 对于页面的重新渲染一般的做法是通过操作 dom ，重置 innerHTML 去完成；而 virtual dom 则是通过 javascript 层面的计算，返回一个 patch[补丁] 对象，即补丁对象，在通过特定的操作解析 patch 对象，完成页面的重新渲染。

- diff 算法，对虚拟节点 Element 的对比，并返回一个 patch 对象，用来存储两个节点不同的地方。这也是整个 virtual dom 实现最核心的一步。

- 而 diff 算法又包含了两个不一样的算法，一个是 O(N)，一个则是 O(max(m,n))
  - O(n)：同层级元素比较
  - O(max(m,n))：listDiff 实现 O(m\*n) => O(max(m, n))
