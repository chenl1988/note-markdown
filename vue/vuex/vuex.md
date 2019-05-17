## vuex

- vuex 是一个专门为 vue.js 设计的集中式状态管理架构。

- vuex 的几个核心概念：

  - state：vuex 中的数据源，需要保存的数据就保存在这里，可以在页面通过`this.$store.state`来获取定义的数据

  - getters：相当于 vue 中的 computed 计算属性，getter 的返回值会根据它的依赖被缓存起来，具只有当它的依赖值发生改变才会被重新计算。这里可以通过定义 vuex 的 Getter 来获取，Getters 可以用于监听、state 中的值的变化，返回计算后的结果

  - mutation:vuex 中去操作数据的方法（只能同步执行）

  - action：用来操作 mutation 的动作，不能直接去操作数据源，但**可以把 mutation 变成异步的**

  - module：模块化，当应用足够大的时候，可以把 vuex 分成几个子模块

---

### 状态

- 可以把它理解为在 data 中的属性需要共享给其他 vue 组件使用的部分，就叫状态
