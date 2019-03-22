## this的绑定规则

- 找到调用位置，然后判断需要应用到下面四条规则中的哪一条：
  - 默认绑定，独立函数调用。可以把这条规则看作是无法应用其他规则时的默认规则
  ```
  function foo(){
    console.log(this.a);
  }
  var a = 2;
  foo();
  ```
  - 隐性绑定，需要考虑的是调用位置是否有上下文对象，或者说是否被某个对象拥有或包含
  ```
  function foo(){
    console.log(this.a);
  }
  var obj = {
    a:2,
    foo:foo
  }
  obj.foo();
  ```
  - 显示绑定，可以使用函数的call()和apply()方法，这两个方法的第一个参数是一个对象，是给this准备的，接着在调用函数时将其绑定到this。因为可以直接指定this的绑定对象，称之为显示绑定
  ```
  function foo(){
    console.log(this.a);
  }
  var obj = {
    a:2
  }
  foo.call(obj);
  ``` 
- new绑定 ，使用new来调用函数，或者说发生构造函数调用时，会自动执行下面的操作：
  - 创建（或者说是构造）一个全新的对象
  - 这个新对象会被执行`[[prototype]]`连接
  - 这个新对象会绑定到函数调用的this
  - 如果函数没有返回其他对象，那么new表达式中的函数调用会自动返回这个新对象

