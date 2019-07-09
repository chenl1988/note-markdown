## 编写一个 loader

- loader 就是一个 node 模块，它输出了一个函数。当某种资源需要用到这个 loader 转换时，这个函数会被调用并且，这个函数可以通过提供给它的 this 上下文访问 Loader API

- reverse-txt-loader

```
module.exports = function (src) {
  //src是原文件内容，下面对内容进行处理，这里是反转
  var result = src.split("").reverse().join("");
  //返回javascript源码，必须是string或者Buffer
  return `module.exports = ${result}`;
}


/* 在webpack中使用 */
{
  test: /\.txt/,
  use: [{
    './path/reverse-txt-loader'
  }]
}
```
