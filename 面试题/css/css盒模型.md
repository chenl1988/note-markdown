## CSS 盒模型

- css 中有个属性叫 box-sizing,属性值有 border-box 和 content-box
  - border-box 中，整个 div 的宽、高，包括 margin、padding、border。
  - content-box 中，整个 div 的宽、高，则不包括上面的元素
- border-box 最好是在引用 reset.css 的时候，就对 border-box 进行统一设置
