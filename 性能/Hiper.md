## Hiper：一款令人愉悦的性能分析工具

```
//全局安装
cnpm install hiper -g

// 最简单的用法
hiper baidu.com

// 如何url中含有任何参数，请使用双引号括起来
hiper "baidu.com?a=1&b=2"

//  加载指定页面100次
hiper -n 100 "baidu.com?a=1&b=2"

//  禁用缓存加载指定页面100次
hiper -n 100 "baidu.com?a=1&b=2" --no-cache

//  禁JavaScript加载指定页面100次
hiper -n 100 "baidu.com?a=1&b=2" --no-javascript

//  使用GUI形式加载指定页面100次
hiper -n 100 "baidu.com?a=1&b=2" -H false

// 使用指定useragent加载网页100次
hiper -n 100 "baidu.com?a=1&b=2" -u "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36"

```

- 当项目打开速度慢时，这个工具可以帮助快速定位到底在哪一步影响页面加载的速度
