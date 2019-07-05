## jsonp

- jsonp 的缺点是只能实现 get 请求

```
/* 原生js */
var script = document.createElement("script");
script.type = 'text/javascript';

//传参并指定回调执行函数为onBack
script.src = "http://www.domain2.com:8080/login?user=admin&callback=onBack";
document.head.appendChild("script");

//回调执行函数
function onBack(res) {
  alert(JSON.stringify(res));
}

/* jquery */
$.ajax({
  url: "http://www.domain2.com:8080/login",
  type: "get",
  dataType: "jsonp", //请求方式为jsonp
  jsonpCallback: "onBack", //自定义回调函数名
  data: {}
})

/* vue */
this.$http.jsonp("http://www.domain2.com:8080/login", {
  params: {},
  jsonp: 'onBack'
}).then(res => {
  console.log(res);
})

/* 后端node接口 */
const querystring = require('querystring');
const http = require('http');
const server = http.createServer();
server.on('request', function (req, res) {
  var params = qs.parse(req.url.split('?')[1]);
  var fn = params.callback;

  //jsonp返回设置
  res.writeHead(200, {
    'Content-Type': 'text/javascript'
  })
  res.write(fn + '(' + JSON.stringify(params) + ')');

  res.end();
})
server.listen('8080');
```
