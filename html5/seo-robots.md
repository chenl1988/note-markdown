## seo-robots

- robots.txt 是放在网站中，文件级的网络蜘蛛授权；
- 而 robots Meta 标签是放在网页中，一般用于部分网页需要单独设置的情况下。
- 两者的功能是一样的。

- <meta name="robots" content="index,follow"/>      搜索引擎抓取
  - content中的值决定允许抓取的类型，必须同时包含两个值：是否允许索引（index）和是否跟踪链接（follow，也可以理解为是否允许沿着网页中的超级链接继续抓取）
  - 共有4个参数可选，组成4个组合：
    - index,follow：允许抓取本页，允许跟踪链接。
    - index,nofollow：允许抓取本页，但禁止跟踪链接。
    - noindex,follow：禁止抓取本页，但允许跟踪链接。
    - noindex,nofllow：禁止抓取本页，同时禁止跟踪本页中的链接。
  - index,follow可以写成all `<meta name="robots" content="all" />`
  - noindex,nofollow可以写成none `<meta name="robots" content="none" />`

- 需要注意的是，robots Meta 标签很多搜索引擎是不支持的，只有少数搜索引擎能够识别并按给定的值抓取。所以，尽可能的使用 robots.txt 文件来限制抓取。

- 不需要太刻意的在 robots.txt 中设置过多禁止文件或目录，只设置确实不希望被搜索引擎索引的目录和文件就可以了。

- 特别是在不清楚文件或目录的作用时，不要轻易禁止抓取。前阵一位做旅游的朋友，网站中有大量的旅游景点图片，几大搜索引擎中却都没有索引，后来对网站检查时发现图片目录 upload 在管理目录 admin 下，被 robots.txt 禁止抓取了。
