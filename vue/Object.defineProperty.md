## Object.defineProperty

- Object.defineProperty 有两个明显的缺点：

  - Object.defineProperty 无法监控到数组下标的变化，导致直接通过数组的下标给数组设置值，不能实时响应。为了解决这个问题，经过 vue 内部处理后可以使用以下几种方法来监听数组：

    - push()
    - pop()
    - shift()
    - unshift()
    - splice()
    - sort()
    - reverse()
    - [ 由于只针对了以上八种方法进行了 hack 处理，所以其他数组的属性也是检测不到，还是有一定的局限性 ]

  - Object.defineProperty 只能劫持对象的属性，因此我们需要对每个对象的每个属性进行遍历。在 Vue2.x 里，是通过递归 + 遍历 data 对象来实现对数据的监控的，如果属性值也是对象那么要深度遍历，显示如果能劫持一个完整的对象才是更好的选择
