## map 高阶函数对应的一道经典面试题

```
//输出结果
["1","2","3"].map(parseInt); //[1, NaN, NaN]


//如果想要得到[1,2,3]
["1","2","3"].map(item=>{parseInt(item)});
["1","2","3"].map((item)=>{return parseInt(item)});
```

- 首先 map 接收两个参数，一个回调函数 callback，一个回调函数的 this 值；其中回调函数接收三个参数：currentValue、index、array

- 而题目中，map 只传入了回调函数 parseInt，其次 parseInt 只接收两个参数 string、radix(基数)【本题理解来说也就是 key 与 index】,parseInt(string,radix)
  - string：必须。需要被解析的字符串
  - radix：可选。表示要解析的数字的基数。
