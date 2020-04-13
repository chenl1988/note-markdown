# 在ES5环境下实现let

## babel转换前后的结果
```
//原代码
for (let i=0;i<10;i++) {
  console.log(i);
}
console.log(i);

//babel转换后
for (var _i=0;_i<10;i++) {
  console.log(_i);
}
console.log(i);

/*
  babel在let定义的变量前加了道下划线，避免在块作用域外访问到该变量
*/
```

## 自执行函数模拟块级作用域
```
(function(){
  for(var i=0;i<10;i++){
    console.log(i);
  }
})();
console.log(i);
```