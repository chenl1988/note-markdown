## 函数的arguments为什么不是数组？

- 因为arguments本身并不能调用数组方法，它是一个另外一种对象类型，只不过属性从0开始排，依次为0,1,2..最后还有callee和length属性。我们也把这样的对象称为类数组。

- 常见的类数组还有：
  - 用getElementsByTagName/ClassName() 获得的HTMLCollection
  - 用querySelector获得的nodeList

## 类数组如何转化成数组？

- Array.prototype.slice.call()  