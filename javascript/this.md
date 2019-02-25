## this

- this是javascript中最复杂的机制之一，它会被自动定义在所有函数的作用域中。
- this提供了一种更优雅的方式来隐式"传递"一个对象的引用，因此可以将API设计的更简洁并且易于复用
- this是在运行时进行绑定的，并不是在编写时绑定，它的上下文取决于函数调用时的各种条件。this的绑定和函数声明的位置没有任何关系，只取决于函数的调用方式。
- this的用法：
  - **函数调用**，属于全局属性，因此this就代表全局对象
  ```
  var x = 1;
  function test(){
    console.log(this.x);
  }
  test();
  ```
  - **作为对象方法调用**，函数还可以作为某个对象的方法调用，这时this就指向这个上级对象
  ```
  function test2(){
    console.log(this.x);
  }
  var obj = {};
  obj.x = 3;
  obj.m = test2;
  obj.m();
  ```
  - **作为构造函数调用**，所谓构造函数就是通过这个函数，可以生成一个新对象，这时this就指向这个新对象
  ```
  function test3(){
    this.x = 4;
  }
  var obj = new test3();
  console.log(obj.x);
  ```
  - **apply调用**，apply()是函数的一个方法，作用是改变函数的调用对象，它的第一个参数就表示改变后的调用这个函数的对象，因此this指的就是第一个参数
  ```
  var y = 5;
  function test4(){
    console.log(this.y);
  }
  var obj = {};
  obj.y = 6;
  obj.m = test4;
  obj.m.apply(obj);
  ```