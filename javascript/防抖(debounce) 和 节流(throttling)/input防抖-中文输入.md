## input 搜索如何防抖，如何处理中文输入

- elementui 是通过 compositionstart 和 compositionend 做的中文处理

```
<input
ref="input"
@compositionstart="handleComposition"
@compositionupdate="handleComposition"
@compositionend="handleComposition"
>
```

- 简单来说就是切换中文输入法时在打拼音时(此时 input 内还没有填入真正的内容)，会首先触发 compositionstart，然后每打一个拼音字母，触发 compositionupdate，最后将输入好的中文填入 input 中时触发 compositionend。触发 compositionstart 时，文本框会填入 “虚拟文本”（待确认文本），同时触发 input 事件；在触发 compositionend 时，就是填入实际内容后（已确认文本）,所以这里如果不想触发 input 事件的话就得设置一个 bool 变量来控制。

- input 事件：
  - 输入到 input 框触发 input 事件
  - 失去焦点后内容有改变触发 change 事件
  - 识别到你开始使用中文输入法触发 **compositionstart** 事件
  - 未输入结束但还在输入中触发 **compositionupdate** 事件
  - 输入完成（也就是我们回车或者选择了对应的文字插入到输入框的时刻）触发 compositionend 事件。
