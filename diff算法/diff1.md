## diff 算法

### 当数据发生改变时，vue 是怎么更新节点的

- 渲染真实 DOM 的开销是很大的，比如修改了某个数据，如果直接渲染到真实 dom 上会引起整个 dom 树的重绘和重排，diff 算法可以只更新一小块 dom 而不是更新整个 dom

- 首先根据真实 dom 生成一颗 virtual DOM，当 virtual DOM 某个节点的数据改变后会生成一个新的 Vnode，然后 Vnode 和 oldVnode 做对比，发现有不一样的地方就直接修改在真实的 DOM 上，然后使 oldVnode 的值为 Vnode

- diff 的过程就是调用名为 patch 的函数，比较新旧节点，一边比较一边给真实的 DOM 打补丁

### virtual DOM 和真实的 DOM 的区别

- virtual DOM 是将真实的 DOM 的数据抽取出来，以对象的形式模拟对开结构，比如 dom 是这样的：

```
<div>
  <p>122</p>
</div>
```

- 对应的 virtual DOM（伪代码）：

```
var Vnode = {
  tag:"div",
  children:[
    tag:'p',
    text:'123'
  ]
}
```

- VNode 和 oldVnode 都是对象

### diff 的比较方式

- 在采取 diff 算法比较新旧节点的时候，比较只会在同层级进行，不会跨层级比较

```
<div>
  <p>123</p>
</div>

<div>
  <span>456</span>
</div>
```

- 上面的代码会分别比较同一层的两个 div 以及第二层的 p 和 span，但是不会拿 div 和 span 做比较
