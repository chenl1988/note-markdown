## MVVM

- MVVM 是 Model-View-ViewModel 的编写；mvvm 是一种设计思想。

  - Model 层代表数据模型，也可以在 Model 中定义数据修改和操作的业务逻辑
  - View 代表 UI 组件，它负责将数据模型转化成 UI 展现出来
  - ViewModel 是一个同步 View 和 Model 的对象

- 数据（Model）和视图（View）是不能直接通讯的，而是需要通过 ViewModel 来实现双方的通讯。当数据变体的时候，ViewModel 能够监听到这种变化，并及时通知道 view 做出修改。同样的，当页面有事件触发时，ViewModel 也能够监听到事件，并通知 model 进行响应；ViewModel 就相当于一个观察者，监控着双方的动作，并及时通知双方进行相应的操作
