# null

- null不是对象
- 虽然typeof null会输出object，但是这只是JS存在的一个悠久的bug，在js的最初版本中使用的是不是吧位系统，为了性能考虑使用低位存储变量的类型信息，000开头代表是对象然而null表示为全零，所以将它错误的判断为object