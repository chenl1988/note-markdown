## CSS 的 scoped 私有作用域和深度选择器

- vue 文件中的<style>标签有 scoped 属性时，它的 CSS 只作用于当前组件中的元素

```
//编译前
<style scoped>
.example {
  color: red;
}
</style>

//编译后
<style>
.example[data-v-f3f3eg9] {
  color: red;
}

//在写的组件的样式，添加了一个属性，这样就实现了所谓的私有作用域
```

- scoped 属性也会有弊端，考虑到浏览器渲染各种 CSS 选择器的方式，当 p{color:red;}设置了作用域时（即与特性选择器组件使用时）会慢很多倍；如果使用 class 或者 id 取代，性能问题就会消除，所以在样式里，应避免直接使用标签。

- 如果希望 scoped 样式中的一个选择器能够作用的“更深”，例如影响子组件，或第三方组件，可以使用`>>>`

```
<style scoped>
  .parent >>> .child{/* ... */}
</style>
//上面的代码会被编译成
.parent[data-v-f3f3eg9] .child {
    /* ... */
}
```

- 如果使用了 less/sass 等预编译，是不支持`>>>`的，可以使用`/deep/`来替换`>>>`操作符

```
.parent /deep/ .child { /* ... */ }
```
