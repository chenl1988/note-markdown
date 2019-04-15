## MVC

- MVC 是应用最广泛的软件架构之一，一般 MVC 分为：
  - Model(模型)：提供数据
  - View(视图)：负责显示
  - Controller(控制器)：负责逻辑处理

---

## MVP

- MVP 是从 MVC 模式演变而来的。
  - Model(模型)：提供数据
  - View(视图)：负责显示
  - Presenter()：负责逻辑处理，与 View 没有直接关联，而是通过定义好的接口进行交互，从而使得在变更 View 的时候保持 Presenter 不变

---

## MVVM

- MVVM 只是把 MVC 的 Controller 和 MVP 中的 Presenter 改成了 ViewModel。view 的变化会自动同步到 ViewModel,ViewModel 的变化也会自动同步到 View 上显示
- 这种自动同步是因为 ViewModel 中的属性实现了 Observer，当属性(数据)变更时都能触发对应的操作
