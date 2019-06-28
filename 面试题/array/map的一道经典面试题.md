## map 高阶函数对应的一道经典面试题

```
//输出结果
["1","2","3"].map(parseInt); //[1, NaN, NaN]


//如果想要得到[1,2,3]
["1","2","3"].map(item=>{parseInt(item)});
["1","2","3"].map((item)=>{return parseInt(item)});
```
