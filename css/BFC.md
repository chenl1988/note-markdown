## BFC 原理

- BFC：Block formatting context = block-level box + Formatting Context
- Box：即盒子模型

  - block-level box 即块级元素：display 属性为 block,list-item,table 的元素，会生成 block-level box;并且参与 block formatting
  - inline-level box 即行内元素：display 属性为 inline,inline-block,inline-table,会生成 inline-level box。并且参与 inline formatting context

- Formatting context:是 W3C CSS2.1 规范中的一个概念。**它是页面中的一块渲染区域，并且有一套渲染规则，它决定了其子元素将如何定位，以及和其他元素的关系、相互作用。** 最常见的 Formatting context 有 Block formatting context(简称 BFC)和 Inline formatting context(简称 IFC)；

  - CSS2.1 中只有 BFC 和 IFC，CSS3 中还增加 G(grid)FC 和 F(flex)FC

- Box：盒 Box 是 CSS 布局的对象和基本单位，元素的类型和 display 属性决定了 Box 的类型

### BFC 的定义

- **BFC(Block formatting context)直译为“块级格式化上下文”。它是一个独立的渲染区域，只有 Block-level box 参与，它规定了内部的 Block-level Box 如何布局，并且与这个区域外部毫不相关**

### BFC 的生成

- CSS2.1 中规定满足下列 CSS 声明之一的元素便会生成 BFC
  - **根元素（body）**
  - **float 的值不为 none**
  - **overflow 的值不为 visible**
  - **display 的值为 inline-block、table-cell、table-caption、flex、inline-flex。（display:table 也认为可以生成 BFC，其实这里的主要原因在于 table 会默认生成一个匿名的 table-cell，正是这个匿名的 table-cell 生成了 BFC）**
  - **position 的值为 absoulte 或 fixed**

### BFC 的约束规则

- 内部的 Box 会在垂直方式上一个接一个的放置
- 垂直方向上的距离由 margin 决定。（完整的说法是：属于同一个 BFC 的两个相邻的 Box 的 margin 会发生重叠（塌陷），与方向无关）
- 每个元素的左外边距与包含块的左边界相接触（从左到右），即使浮动元素也是如此（这说明 BFC 中的子元素不会超出他的包含块，而 position 为 absoulte 的元素可以超出他的包含块边界）
- BFC 的区域不会与 float 元素区域重叠
- 计算 BFC 的高度时，浮动子元素也参与计算
- BFC 就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面元素，反之亦然
- 看到以上几条约束，想想我们学习 CSS 时的几条规则：
  - Block 元素会扩展到与父元素同宽，所以 block 元素会垂直排列
  - 垂直方向上的两个相邻 DIV 的 margin 会重叠，而水平方向不会（此规则并不完全正确）
  - 浮动元素会尽量接近往左上方（或右上方）

### BFC 在布局中的应用

- 防止 margin 重叠（塌陷）
- 清除内部浮动
- 自适应多栏布局的

### 总结

- BFC 就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素，反之也是如此
- 因为 BFC 内部的元素和外部的元素绝对不会互相影响
- 当 BFC 外部存在浮动时，它不应该影响 BFC 内部 BOX 的布局，BFC 会通过变窄，而不与浮动有重叠。同样的，当 BFC 内部有浮动时，为了不影响外部的元素的而已，BFC 计算高度时会包括浮动的高度。避免 margin 重叠也是这样一个道理。
