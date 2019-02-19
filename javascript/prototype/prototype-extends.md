## javascript 的原型继承实现方式：

- 定义新的构造函数，并在内部用 call()调用希望“继承”的构造函数，并绑定 this
- 借助中间函数 F 实现原型链继承，最好通过封装的 inherits 函数完成
  ```
    function inherits(Child,Parent){
        var F = function(){};
        F.prototype = Parent.prototype;
        Child.prototype = new F();
        Child.prototype.constructor = Child;
    }
  ```
- 继续在新的构造函数的原型上定义方法
