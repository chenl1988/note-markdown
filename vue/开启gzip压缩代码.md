## 开启 gzip 压缩代码

- spa 这种单面应用，首屏由于一次性加载所有资源，所以首屏加载速度很慢，解决这个问题非常有效的手段之一就是前后端开启 gizp（其它还有缓存、路由懒加载等等）。
- gzip 其实就是减少文件体积，能压缩到 30%左右，即 100k 的文件 gzip 后大约只有 30k

```
vue2需配合vue-cli3 cnpm i compression-webpack-plugin@1.1.11
//然后在config/index.js中开启即可:
build: {
    // 其他代码
    …………
    productionGzip: true, // false不开启gizp，true开启
    // 其他代码
}
```

- 打包的时候，除了会生成之前的文件，还是生成.gz 结束的 gzip 过后的文件。具体实现就是如果客户端支持 gzip，那么后台返回 gzip 文件，如果不支持就返回正常没有 gzip 文件

- **注意：这里前端进行的打包时的 gzip，但是还需要后台服务器的配置。配置是比较简单的，配置几行代码就可以**
