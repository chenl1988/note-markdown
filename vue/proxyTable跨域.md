## proxyTable 代理

- vue 的 proxyTable 是用于开发阶段配置跨域的工具，可以同时配置多个服务器跨域请求接口，其真正依赖的 npm 包是 http-proxy-middleware

```
// 代理配置表，在这里可以配置特定的请求代理到对应的API接口
// 例如将'localhost:8080/api/xxx'代理到'www.example.com/api/xxx'

proxyTable: {
  '/api': {
    target: 'http://xxxxxx.com', // 接口的域名
    // secure: false,  // 如果是https接口，需要配置这个参数
    changeOrigin: true, // 如果接口跨域，需要进行这个参数配置
    pathRewrite: {
      '^/api': ''
    }
  }
},
```

- 注意：**'/api'为匹配项，target 为请求的地址**，因为在 ajax 的 url 中加了前缀'/api'，而原本的接口是没有这个前缀的，所有需要 pathRewrite 来重写地址，将前缀'/api'转为'/'。如果本身的接口地址就有'/api'这种通用的前缀，就可以把 pathRewrite 删掉。
