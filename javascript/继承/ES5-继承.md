## ES5中实现继承

### Object.create()

```
function Super(){}
Super.prototype.getNumber = function(){
  return 1;
}

function Sub(){}
Sub.prototype = Object.create(Super.prototype,{
  constructor:{
    value:Sub,
    enumerable:false,
    writable:true,
    configurable:true
  }
})
let sub = new Sub();
console.log(sub.getNumber());
```