## key

- `<div v-for="i in dataList" :key='i'>{{ i }}</div>`

- key 是给每一个 vnode 的唯一 id，可以依靠 key 更准确，更快的拿到 oldVnode 中对应的 vnode 的节点
  - 更准确：因为带 key 就不是就地复用了，在 sameNode 函数 a.key === b.key 对比中可以避免就地利用的情况，所以会更加准确
  - 更快：利用 key 的唯一性生成 map 对象来获取对应节点，比遍历方式更快

---

vue 和 react 老师采用 diff 算法来对比新旧虚拟节点，从而更新节点
