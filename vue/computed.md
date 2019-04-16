## computed 计算属性

- 计算属性里可以完成各种复杂的逻辑。包括运算、函数调用等。只要最终返回一个结果就可以；计算属性还可以依赖多个 vue 实例的数据，只要其中任一数据变化，计算属性就会重新执行，视图也会更新。
- 每一个计算属性都包含一个 getter 和一个 setter。

```
data:{
  firstName:'Jack',
  lastName:'Green'
},
computed:{
  fullName:{
    //getter用于读取
    get:function(){
      return this.firstName + ' ' + this.lastName;
    },
    //setter,写入时触发
    set:funciton(newValue){
      var names = newValue.split(' ');
      this.firstName = names[0];
      this.lastName = names[names.length - 1];
    }
  }
}
```

- 绝大多数情况下，只会用默认的 getter 方法来读取一个计算属性

- **计算属性除了简单的文本插值外，还经常用于动态地设置元素的样式名称 class 和内联样式 style。当使用组件时，计算属性也经常用来动态传递 props。**
- **计算属性还有两个很实用的技巧：一是计算属性可以依赖其他计算属性；二是计算属性不仅可以依赖当前 Vue 实例的数据，还可以依赖其他实例的数据。**

- computed 和 methods 的区别：
  - 计算属性是基于它的依赖缓存的。一个计算属性所依赖的数据发生变化时，它才会重新取值，所以数据只要不改变，计算属性也就不更新；
  - methods 只要重新渲染，它就会被调用，因此函数也会被执行。
  - 使用 methods 还是 computed 取决于是否需要缓存，当遍历大数组和大量计算时，应该使用计算属性，除非你不希望得到缓存。
