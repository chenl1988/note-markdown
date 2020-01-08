# forEach

- forEach()：结束循环不能使用 break，可以用try/catch中的throw new Error停止

- forEach()：无法在所有元素都传递给调用的函数之前终止遍历

- forEach()：return false;在这里起的作用只是终止本次循环，继续执行，而不是终止 for 循环


# forEach中return有效果吗？
- forEach中的return不会返回，函数会继续执行 
```
let nums = [1,2,3];
nums.forEach((item,index)=>{
  console.log(item);
  return; //无效
})
```

# 如何中断forEach循环？

- 使用try监视代码块，在需要中断的地方抛出异常

- 官方推荐方法（替换方法）：用every和some替代forEach函数。every在碰到return false的时候，中止循环。some有碰到return true的时候，中止循环。
