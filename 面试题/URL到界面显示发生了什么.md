## URL 到界面显示发生了什么

- 1、DNS 解析，先本地缓存，在一层层找将常见的地址解析成唯一对应的 ip 地址基本顺序为：本地域名服务器->根域名服务器->com 顶级域名服务器，以此类推下去，找到后记录并缓存下来，如：www.google.com 为`.->.com->google.com->www.google.com`

- 2、TCP 连接 三次握手，只要没收到确认消息就要重新发：
  - 主机向服务器发送一个建立连接的请求（您好，我想认识您）
  - 服务器接到请求后发送同意连接的信号（好的，很高兴认识您）
  - 主机接到同意连接的信号后，再次向服务器发送了确认信号（我也很高兴认识您），自此，主机与服务器两者建立了连接
- 3、发送 HTTP 请求 浏览器解析这个 Url，并设置好报文发出。请求报文中包括请求行、请求头、空行、请求主体。https 默认请求端口 443，http 默认 80。常见的 http 请求如下：

```
POST / HTTP1.1
Host:www.wrox.com
User-Agent:Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 2.0.50727; .NET CLR 3.0.04506.648; .NET CLR 3.5.21022)
Content-Type:application/x-www-form-urlencoded
Content-Length:40
Connection: Keep-Alive

name=Professional%20Ajax&publisher=Wiley

第一部分：请求行，第一行说明是post请求，以及http1.1版本
第二部分：请求头部，第二行至第六行
第三部分：空行，第七行空行
第四部分：请求数据，第八行
```

- 4、服务器处理请求并返回 HTTP 报文，后端处理返回 HTTP 报文如下：

```
HTTP/1.1 200 OK
Date: Fri, 22 May 2009 06:07:21 GMT
Content-Type: text/html; charset=UTF-8

<html>
      <head></head>
      <body>
            <!--body goes here-->
      </body>
</html>

第一行：状态行，（HTTP/1.1）表明HTTP版本1.1版本，状态码为200，状态消息为（ok）
第二行和第三行为消息报头
  - Date：生成响应的日期和时间；
  - Content-Type：指定了MIME类型的HTML（text/html）,编码类型是UTF-8
第三部分：空行，消息报头后面的空行是必须的
第四部分：响应正文，服务器返回给客户端的文本信息
空行后面的html部分为响应
```

- 5、浏览器解析渲染页面

  - 通过 HTML 解析器解析 HTML 文档，构建一个 DOM Tree，同时通过 CSS 解析器解析 HTML 中存在的 CSS，构建 Style Rules，两者结合形成一个 Attachment(附件)
  - 通过 Attachment 构造出一个呈现树（Render Tree）
  - Render Tree 构建完毕，进入到布局阶段（layout/reflow），将会为每个阶段分配一个应出现在屏幕上的确切坐标
  - 最后将全部的节点遍历绘制出来后，一个页面就展现出来了。遇到 script 会停下来执行，所以通常把 script 放在底部

- 6、连接结束
