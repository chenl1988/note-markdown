# directives 指令

- 用以改写某个组件的默认行为，或者增强使其获得额外功能，一般来说可以在同一个组件上叠加若干个指令，使用获得多种功能。比如v-if，它可以安装或者卸载组件。

- 自定义指令分为全局指令和局部指令；全局指令是在main.js内使用Vue.directive注册，局部指令是在组件的directives选项写入

## vue指令生命周期
- bind:只调用一次，指令第一次绑定到元素调用，在这里可以进行一次性的初始化设置
- inserted:被绑定元素插入父节点时调用（仅保证父节点存在，但不一定已被插入文档中）
- update:所在组件的VNode更新时调用，但是可能发生在其子VNode更新之前。指令的值可能发生了改变，也可能没有。但是你可以通过比较更新前后的值来忽略不必要的模板更新。
- componentUpdate:指令所在组件的VNode及其子VNode全部更新后调用
- unbind:只调用一次，指令与元素解绑时调用

### 生命周期函数中的参数
- el:指令所绑定的元素，可以用来直接操作DOM，就是放置指令的那个元素
- binding:一个对象，里面包含了几个属性
  - name：指令名，不包括v-前缀
  - value:指令的绑定值，例如v-my-directives="1+1"中，绑定值为2
  - oldValue:指令绑定前的一个值，仅在update和componentUpdate钩子中可用，无论值是否改变都可用
  - expression:字符串形式的指令表达式。例如v-my-directive="1+1"中，表达式"1+1"
  - arg:传给指令的参数，可选。例如：v-my-directive:foo中，参数为foo
  - modifires:一个包含修饰符的对象，例如：v-my-directive.foo.bar,修饰符对象为{foo:true,bar:true}
- vnode:Vue编译生成的虚拟节点
- oldVnode:上一个虚拟节点，仅在update和componentUpdated钩子中可用