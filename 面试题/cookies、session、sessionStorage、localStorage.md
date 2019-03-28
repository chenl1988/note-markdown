## cookies、session、sessionStorage、localStorage

- cookies:存储于浏览器端的数据。可以设置 cookies 的到期时间，如果不设置时间，则在浏览器关闭窗口的时候会消失
- session:存储于服务器端的数据。session 存储特定用户会话所需的属性和配置信息

- cookies 和 session 的区别在于：
  - cookies 数据存储在客户的浏览器上，session 数据存放在服务器上
  - cookies 在前端安全性有问题
  - session 如果在生效期内量过大，会占用服务器性能
  - 单个 cookies 保存的数据不能超过 4K，很多浏览器限制一个站点保存最多 20 个 cookies

---

- sessionStorage:生命周期存在于标签页或窗口，用于本地存储一个会话（session）中的数据，这些数据会随着窗口或者标签页的关闭而被清空
- localStorage:生命周期是永久的，除非用户主动清除浏览器上存储的 localStorage 信息，否则它将会永久存在
- sessionStorage 和 localStorage 操作方法:setItem、getItem 以及 removeItem
