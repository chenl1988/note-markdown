## 如何优雅的只在当前页面中覆盖 ui 库中组件的样式

- 在 vue 文本中的样式都是写在`<style lang="less" scoped></style>`标签中的，加**scoped**是为了使得样式只在当前页面有效

- 正常写的所有样式，都会被加上`[data-v-23d425f8]`类似的这样的属性【**由于加入了这个属性所以样式只在当前页面生效**】，但是第三方组件内部并没有编译为带`[data-v-23d425f8]`这样的属性

- 可以在当前页面或公共的 css 文件中再写一个没有 scoped 属性的 style 标签，可以直接在里面对第三方组件样式进行修改；但是存在污染全局和命名冲突的问题。

- 优雅的解决方式：通过深度选择器解决；这里的深度选择器`/deep/`是因为使用了 less/sass 等，如果没有使用可以用`>>>`符号

```
//修改组件中的van-ellipsis类的样式
.van-tabs /deep/ .van-ellipsis{color:blue}

//编译后的结果
.van-tabs[data-v-23d425f8] .van-ellipsis{
  color:blue;
}
//这样就不会给van-ellipsis也添加[data-v-23d425f8]属性了
```
