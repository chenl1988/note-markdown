## CORS 跨域资源共享

- CORS 是一个 W3C 标准，全称是“跨域资源共享”（Cross-origin resource sharing）
- 它允许浏览器向跨源服务器，发出 XMLHttpRequest 请求，从而克服了**AJAX 只能同源使用的限制**。
- CORS 需要浏览器和服务器同时支持。目前，所有浏览器都支持该功能，IE 浏览器不能低于 IE10。
- 整个 CORS 通信过程，都是浏览器自动完成，不需要用户参与。对于开发都来说，CORS 通信与同源的 AJAX 通信没有差别，代码上完成一样。浏览器一旦发现 AJAX 请求，就会自动添加一些附加的头信息，有时还会多出一次附加的请求，但用户不会有感觉。
- 因此，实现 CORS 通信的关键是服务器。只要服务器实现了 CORS 接口，就可以跨源通信。

- 浏览器将 CORS 请求分为两类：简单请求（simple request）和非简单请求（not-so-simple request）

- 只要同时满足以下两个条件，就属于简单请求：

  - （1）请求方法是以下三种方法之一：
    - HEAD
    - GET
    - POST
  - （2）HTTP 的头信息不超出以下几种字段：
    - Accept
    - Accept-Language
    - Content-Language
    - Last-Event-ID
    - Content-Type：只限于三个值：application/x-www-form-urlencoded、multipart/form-data、text/plain
  - 凡是不同时满足上面两个条件，就属于非简单请求

- 浏览器对简单请求和非简单请求的处理，是不一样的

  - 简单请求，浏览器直接发出 CORS 请求。具体来说，就是在头信息之中，增加一个 origin 字段。

    - 下面例子，浏览器发现这次跨源 AJAX 请求是简单请求，就是在头信息中，添加一个 origin 字段；

    ```
    GET /cors HTTP/1.1
    Origin:http://api.bob.com
    Host:api.alice.com
    Accept-Language:en-US
    Connection:keep-alive
    User-Agent:Mozlla/5.0...
    ```

    - 上面的头信息中，Origin 字段用来说明，本次请求来自哪个源（协议 + 域名 + 端口）。服务器根据这个值，决定是否同意这次请求
    - 如果 Origin 指定的源，不在许可范围内，服务器会返回一个正常的 HTTP 回应。浏览器发现，这个回应的头信息没有包含 Access-Control-Allow-Origin 字段，就知道出错了，从而抛出一个错误，被 XMLHttpRequest 的 onerror 回调函数捕获。注意，这种错误无法通过状态码识别，因为 HTTP 回应的状态码有可能是 200。
    - 如果 Origin 指定的域名在许可范围内，服务器返回的响应，会多出几个头信息字段

    - **Access-Control-Allow-Origin:http://api.bob.com //该字段是必须的。它的值要么是请求时 Origin 字段的值，要么是一个\*，表示接受任意域名的请求**

    - Access-Control-Allow-Credentials:true //该字段可选，它的值是一个布尔值，表示是否允许发送 Cookie。默认情况下，Cookie 不包括在 CORS 请求之中。设为 true，即表示服务器明确许可，Cookie 可以包含在请求中，一起发送给服务器。这个值也只能设为 true，如果服务器不要浏览器发送 Cookie，删除字段即可。

    - Access-Control-Expose-Headers:FooBar //该字段可选。CORS 请求时，XMLHTTPRequest 对象的 getResponseHeader()方法只能拿到 6 个基本字段：Cache-Control、Content-Language、Content-Type、Expires、Last-Modified、Pragma。如果想拿到其他字段，就必须在 Access-Control-Expose-Headers 里面指定。例子里指定，getResponseHeader("Foobar")可以返回 Foobar 字段的值。

    - Content-Type:text/html;charset=utf-8

  - 非简单请求，对服务器有特殊要求的请求，比如请求方式是 put 或 delete。或者 content-type 字段的类型是 application/json

    - 非简单请求的 cors 请求，会在正式通信之前，增加一次 http 查询请求，称为预检请求；浏览器先询问服务器，当前网页所在的域名是否在服务器的许可名单之中，以及可以使用哪些 HTTP 动词和头信息字段。只有得到肯定答复，浏览器才会发出正式的 XMLHttpRequest 请求，否则就报错

    ```
    <!-- HTTP请求的方法是PUT，并且发送一个自定义头信息 X-Custom-Header -->
    var url = "http://api.alice.com/cors";
    var xhr = new XMLHTTPRequest();
    xhr.open('PUT',url,true);
    xhr.setRequestHeader('X-Custom-Header','value');
    xhr.send();

    <!-- 浏览器发现，这是一个非简单请求，就自动发出一个“预检”请求，要求服务器确认这样可以请求，下面是“预检”请求的HTTP头信息 -->

    OPTIONS /cors HTTP/1.1  //“预检”请求用的请求方法是OPTIONS，表示这个请求是用来询问的
    Origin: http://api.bob.com //表示请求来自哪个源
    Access-Control-Request-Method: PUT //是必须的，用来列出浏览器的CORS请求会用到哪些HTTP方法
    Access-Control-Request-Headers: X-Custom-Header //该字段是一个逗号分隔的字符串，指定浏览器CORS请求会额外发送的头信息字段
    Host: api.alice.com
    Accept-Language: en-US
    Connection: keep-alive
    User-Agent: Mozilla/5.0

    <!-- “预检”请求的头信息包括两个特殊字段：Access-Control-Request-Method， Access-Control-Request-Headers-->
    ```

    - 服务器收到了“预检”请求以后，检查了 Origin、Access-Control-Request-Method 和 Access-Control-Request-Headers 字段以后，确认允许跨源请求，就可以做出回应

    ```
    HTTP/1.1 200 OK
    Date: Mon, 01 Dec 2008 01:15:39 GMT
    Server: Apache/2.0.61 (Unix)
    Access-Control-Allow-Origin: http://api.bob.com //表示http://api.bob.com可以请求数据。该字段也可以设为星号，表示同意任意跨源请求 `Access-Control-Allow-Origin: *`
    Access-Control-Allow-Methods: GET, POST, PUT
    Access-Control-Allow-Headers: X-Custom-Header
    Content-Type: text/html; charset=utf-8
    Content-Encoding: gzip
    Content-Length: 0
    Keep-Alive: timeout=2, max=100
    Connection: Keep-Alive
    Content-Type: text/plain
    ```

    - 如果浏览器否定了“预检”请求，会返回一个正常的 HTTP 回应，但是没有任何 CORS 相关的头信息字段。这时浏览器就会认定，服务器不同意预检请求，因此触发一个错误，被 XMLHttpRequest 对象的 onerror 回调函数捕获

    - 服务器回应的其他 CORS 相关字段如下：

    ```
    Access-Control-Allow-Methods: GET, POST, PUT
    Access-Control-Allow-Headers: X-Custom-Header
    Access-Control-Allow-Credentials: true
    Access-Control-Max-Age: 1728000

    //Access-Control-Allow-Methods：该字段必需，它的值是逗号分隔的一个字符串，表明服务器支持的所有跨域请求的那个方法。注意，返回的是所有支持的方法，而不单是浏览器请求的那个方法。这是为了避免多次“预检”请求。

    //Access-Control-Allow-Headers：如果浏览器请求包括Access-Control-Request-Headers字段，则Access-Control-Allow-Headers字段是必需的。它也是一个逗号分隔的字符串，表明服务器支持的所有头信息字段，不限于浏览器在"预检"中请求的字段。

    //Access-Control-Allow-Credentials：该字段可选。它的值是一个布尔值，表示是否允许发送Cookie。默认情况下，Cookie不包括在CORS请求之中。设为true，即表示服务器明确许可，Cookie可以包含在请求中，一起发给服务器。这个值也只能设为true，如果服务器不要浏览器发送Cookie，删除该字段即可。

    //Access-Control-Max-Age：该字段可选，用来指定本次预检请求的有效期，单位为秒。上面结果中，有效期是20天（1728000秒），即允许缓存该条回应1728000秒（即20天），在此期间，不用发出另一条预检请求。
    ```

    - 一旦服务器通过了“预检”请求，以后每次浏览器正常的 CORS 请求，就都跟简单请求一样，会有一个 Origin 头信息字段。服务器的回应，也都会有一个 Access-Control-Allow-Origin 头信息字段

    ```
    <!-- “预检”请求之后，浏览器的正常CORS请求 -->
    PUT /cors HTTP/1.1 //浏览器自动添加的
    Origin: http://api.bob.com
    Host: api.alice.com
    X-Custom-Header: value
    Accept-Language: en-US
    Connection: keep-alive
    User-Agent: Mozilla/5.0...
    <!-- 下面是服务器的正常的回应 -->
    Access-Control-Allow-Origin: http://api.bob.com //每次回应都必定包含
    Content-Type: text/html; charset=utf-8
    ```

- CORS 与 JSONP 的使用目的相同，但是比 JSONP 更强大。
- JSONP 只支持 GET 请求，CORS 支持所有类型的 HTTP 请求。JSONP 的优势在于支持老式浏览器，以及可以向不支持 CORS 的网站请求数据。

```
/* 原生 */
var xhr = new XMLHttpRequest(); // IE8/9需用window.XDomainRequest兼容
//前端设置是否带cookie
xhr.withCredentials = true;
xhr.open('post', 'http://www.domain2.com:8080/login', true);
xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
xhr.send('user=admin');

xhr.onreadystatechange = function () {
  if (xhr.readyState == 4 && xhr.status == 200) {
    alert(xhr.responseText);
  }
}

/* jquery */
$.ajax({
  ...
  xhrFields: {
    withCredentials: true //前端设置是否带cookie
  },
  crossDomain: true, //会让请求头中包含跨域的额外信息，但不会含cookie
})

/* postMessage(data,origin) 方法接收两个参数 */
/*
  a.html
  <iframe id="iframe" src="http://www.domain2.com/b.html" style="display:none"></iframe>
*/
var iframe = document.getElementById("iframe");
iframe.onload = function () {
  var data = {
    name: 'aym'
  }
  iframe.contentWindow.postMessage(JSON.stringify(data), 'http://www.domain2.com');
}
window.addEventListener("message", function (e) {
  alert('data from domain2--->' + e.data);
}, false);
/* b.html */
window.addEventListener('message', function (e) {
  alert("data from domain1 --->" + e.data);

  var data = JSON.parse(e.data);
  if (data) {
    data.number = 16;

    //处理后再发回domain1
    window.parent.postMessage(JSON.stringify(data), 'http://www.damain1.com');
  }
}, false)
```
