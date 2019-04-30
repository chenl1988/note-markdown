## fastClick 的 300ms 延迟解决方案

- 不管 vue 项目还是 jq 项目，都可以使用 fastClick 解决

- 安装 fastClick

```
cnpm install fastclick -S

//在main.js中引入fastClick和初始化:
import FastClick from 'fastclick'; // 引入插件
FastClick.attach(document.body); // 使用 fastclick
```
