## hash 和 history 模式

- 对于 Vue 这类渐进式前端开发框架，为了构建 SPA（单页面应用），需要引入前端路由系统，这也就是 Vue-Router 存在的意义。前端路由的核心，就在于--**改变视图的同时不会向后端发出请求**

### hash

- 即地址栏 URL 中的#符号（此 hash 不是密码学里的散列运算）；比如这个 URL:`http://www.abc.com/#/hello`，hash 的值为`#/hello`。它的特点在于：**hash 虽然出现在 URL 中，“#”后面的内容不会被包括在 HTTP 请求中，对后端完全没有影响，因为改变 hash 不会重新加载页面**

### history

- history 模式利用了 HTML5 History Interface 中新增的 pushState()和 replaceState()方法（需要特定浏览器支持）；这两个方法应用于浏览器的历史记录栈，在当前已有的 back、forward、go 的基础之上，它们提供了对历史记录进行修改的功能。只是当它们执行修改时，虽然改变了当前的 URL，但浏览器不会立即向后端发送请求

- 因此可以说，hash 模式和 history 模式都属于浏览器自身的特性，Vue-router 只是利用了这两个特性（通过调用浏览器提供的接口）来实现前端路由

- history.pushState(stateObject,title,url)\*_主要是在不刷新浏览器的情况中，创建新的浏览并插入到浏览记录队列中_ 。
  - 状态对象（stateObject）--stateObject 是一个 JavaScript 对象，通过 pushState 方法可以将 stateObject 内容传递到新页面中
  - 标题（title）--几乎没有浏览器支持该参数，但是传一个空字符串会比较安全
  - 地址（url）--新的历史记录条目的地址（可选，不指定的话则为文档当前 url）；浏览器在调用 pushState()方法后不会加载该地址；传入的 URL 与当前 URL 应该是**同源**的，否则，pushState()会抛出异常

### history.pushState()的优势：

- pushState()设置的新 URL 可以是与当前 URL 同源的任意 URL；而 hash 只可修改#后面的部分，因此只能设置与当前 URL 同文档的 URL;
- pushState()设置的新 URL 可以与当前 URL 一模一样，这样也会把记录添加到栈中；而 hash 设置的新值必须与原来不一样才会触发动作将记录添加到栈中；
- pushState()通过 stateObject 参数可以添加任意类型的数据到记录中；而 hash 只可添加短字符串；
- pushState()可额外设置 title 属性供后续使用

### history 和 hash 在通过**URL 向后端发送 HTTP 请求时，两者的差异**：

- history 也不是样样都好，SPA 虽然在浏览器里游刃有余，但真要通过 URL 向后端发起 HTTP 请求时，两者的差异就来了。尤其在用户手动输入 URL 后回车，或者刷新（重启）浏览器的时候
  - hash 模式下，仅 hash 符号之前的内容会被包含在请求中，如`http://www.abc.com`，因此对于后端来说，即使没有做到对路由的全覆盖，也不会返回 404 错误。
  - history 模式下，前端 URL 必须和实际上后端发起请求的 URL 一致，如：`http://www.abc.com/book/id`。如果后端缺少对`/book/id`的路由的处理，将返回 404 错误

### history 模式下后端如何配置

- history 模式下直接打开导出的网页时，页面是无法渲染成功的，文件加载正常，但页面却没显示任何内容。这是因为在 history 模式下，浏览器去打开`.../padExam/home`页面时，会向服务端发送 http 请求来获取页面资源，而此处为本地路径，后端没有对路径进行配置，请求自然以失败告终，因此需要在服务端后台配置文件的访问根目录

```
export default new Router({
  mode:'history',
  base:'padExam',//导出后所在的目录
  routes:[{
    ...
  }]
})
```
