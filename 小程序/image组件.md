# image组件

![](./image组件.png)

- 在小程序中图片不能根据宽度自适应高度，需要在image标签上增加mode="widthFix"
- mode 有 13 种模式，其中 4 种是缩放模式，9 种是裁剪模式。
- widthFix: 宽度不变，高度自动变化，保持原图宽高比不变