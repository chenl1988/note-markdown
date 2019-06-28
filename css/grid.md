## grid 一个超酷的图像网格图

- grid 将根据屏幕的宽度来改变列的数量。最精彩的地方在于：所有的响应特性被添加到一行 css 代码中

- css 栅格布局带来一个全新的值：fraction 单位，fraction 单位通常简写为 fr,它允许你根据需要将容器拆分为多个块
  ![](./grid-fraction.gif)

- repeat() ：这是一个强大的指定列和行的方法 grid-template-columns:repeat(3,100px);相当于 grid-template-columns(100px 100px 100px);第一个参数指定行与列的数量，第二个参数指定它们的宽度

- auto-fit：让我们跳过固定数量的列，将 3 替换为自适应数量 grid-template-columns(auto-fit,100px)

- minmax()：函数定义的范围大于或等于 min，小于或等于 max
