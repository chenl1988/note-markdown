## js 的 new 操作符做了哪些事情

- 四大步骤：
  - 新生成一个对象
  - 链接到原型
  - 绑定 this
  - 返回新对象

```
function myNew(){
  // 创建一个空的对象
  let obj = new Object();
  // 获得构造函数
  let Con = [].shift.call(arguments);
  // 链接到原型
  obj.__proto__ = Con.prototype;
  // 绑定 this，执行构造函数
  let result = Con.apply(obj,arguments);
  // 确保 new 出来的是个对象
  return typeof result === "object" ? result : obj;
}
```

---

- new 操作符新建了一个空对象，这个空对象原型指向构造函数的 prototype，执行构造函数后返回这个对象
