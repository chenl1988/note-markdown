# typeof

- 对于原始数据类型来说，除了Null都可以调用typeof显示正确的类型
```
typeof 1; //'number'
typeof '1'; //'string'
typeof undefined; //'undefined'
typeof true; //'boolean'
typeof Symbol; //'symbol'
```

- 但对于引用数据类型，除了函数之外，都会显示'object'
```
typeof [] //'object'
typeof {} //'object'
typeof console.log //'function'
```

- 采用typeof判断对象数据类型是不合适的，采用instanceof会更好