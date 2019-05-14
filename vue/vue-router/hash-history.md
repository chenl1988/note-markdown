## History 模式

- vue-router 默认 hash 模式，使用 URL 的 hash 来模拟一个完整的 URL，于是当 URL 改变时，页面不会重新加载。

- history 模式，这种模式充分利用**history.pushState**api 来完成 URL 跳转而无须重新加载页面
