- Object.create(null);和｛｝很像，但是并不会创建Object.prototype这个委托，所以它比{}“更空”

- `console.trace();`可以查看每一次当前的调用栈状态
```
function foo(n){
  console.trace();
  if(n<0){
    return;
  }
  console.log("begin:"+n);
  foo(n-1);
  console.log("end:"+n);

}
foo(3);
```