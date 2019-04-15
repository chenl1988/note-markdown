## CORS 跨域资源共享

- CORS是一个W3C标准，全称是“跨域资源共享”（Cross-origin resource sharing）
- 它允许浏览器向跨源服务器，发出XMLHttpRequest请求，从而克服了**AJAX只能同源使用的限制**。
- CORS需要浏览器和服务器同时支持。目前，所有浏览器都支持该功能，IE浏览器不能低于IE10。
- 整个CORS通信过程，都是浏览器自动完成，不需要用户参与。对于开发都来说，CORS通信与同源的AJAX通信没有差别，代码上完成一样。浏览器一旦发现AJAX请求，就会自动添加一些附加的头信息，有时还会多出一次附加的请求，但用户不会有感觉。
- 因此，实现CORS通信的关键是服务器。只要服务器实现了CORS接口，就可以跨源通信。

- 浏览器将CORS请求分为两类：简单请求（simple request）和非简单请求（not-so-simple request）

- 只要同时满足以下两个条件，就属于简单请求：
  - （1）请求方法是以下三种方法之一：
    - HEAD
    - GET
    - POST
  - （2）HTTP的头信息不超出以下几种字段：
    - Accept
    - Accept-Language
    - Content-Language
    - Last-Event-ID
    - Content-Type：只限于三个值：application/x-www-form-urlencoded、multipart/form-data、text/plain
    - 凡是不同时满足上面两个条件，就属于非简单请求

- 浏览器对简单请求和非简单请求的处理，是不一样的
  - 简单请求，浏览器直接发出CORS请求。具体来说，就是在头信息之中，增加一个origin字段。
    - 下面例子，浏览器发现这次跨源AJAX请求是简单请求，就是在头信息中，添加一个origin字段；
    ```
    GET /cors HTTP/1.1
    Origin:http://api.bob.com
    Host:api.alice.com
    Accept-Language:en-US
    Connection:keep-alive
    User-Agent:Mozlla/5.0...

    //上面的头信息中，Origin字段用来说明，本次请求来自哪个源（协议 + 域名 + 端口）。服务器根据这个值，决定是否同意这次请求
    //如果Origin指定的源，不在许可范围内，服务器会返回一个正常的HTTP回应。浏览器发现，这个回应的头信息没有包含Access-Control-Allow-Origin字段，就知道出错了，从而抛出一个错误，被XMLHttpRequest的onerror回调函数捕获。注意，这种错误无法通过状态码识别，因为HTTP回应的状态码有可能是200。
    //如果Origin指定的域名在许可范围内，服务器返回的响应，会多出几个头信息字段

    Access-Control-Allow-Origin:http://api.bob.com //该字段是必须的。它的值要么是请求时Origin字段的值，要么是一个*，表示接受任意域名的请求
    Access-Control-Allow-Credentials:true //该字段可选，它的值是一个布尔值，表示是否允许发送Cookie。默认情况下，Cookie不包括在CORS请求之中。设为true，即表示服务器明确许可，Cookie可以包含在请求中，一起发送给服务器。这个值也只能设为true，如果服务器不要浏览器发送Cookie，删除字段即可。
    Access-Control-Expose-Headers:FooBar //该字段可选。CORS请求时，XMLHTTPRequest对象的getResponseHeader()方法只能拿到6个基本字段：Cache-Control、Content-Language、Content-Type、Expires、Last-Modified、Pragma。如果想拿到其他字段，就必须在Access-Control-Expose-Headers里面指定。例子里指定，getResponseHeader("Foobar")可以返回Foobar字段的值。
    Content-Type:text/html;charset=utf-8
    ```

    // 来自:http://www.ruanyifeng.com/blog/2016/04/cors.html