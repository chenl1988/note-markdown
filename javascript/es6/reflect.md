## reflect

- reflect 是 es6 新增的内置对象。Reflect 不是构造函数，要使用的时候直接通过 Reflect.method()调用，Reflect 有的方法和 Proxy 差不多，而且多数 Reflect 方法原生的 Object 已经重新实现
- 为什么要使用 reflect 的原因:

  - 1. 更加有用的返回值：reflect 有一些方法和 ES5 中的 Object 方法一样，比如：Reflect.getOwnPropertyDescriptor 和 Reflect.defineProperty,不过 Object.defineProperty(obj,name,desc)执行成功后返回 obj，以及其它原因导致的错误，Reflect.defineProperty 只会返回 false 或者 true 来表示对象属性是否设置成功

  ```
  try{
    Object.defineProperty(obj,name,desc);
  }catch(e){

  }
  // 使用Reflect重构
  if(Reflect.defineProperty(obj,name,desc)){
    //success
  }else{
    //failure
  }
  ```

  - 2. 函数操作，如果要判断一个 Obj 有定义或者了属性 name，在 ES5 中判断：name in obj;或者删除一个属性：delete obj[name]，虽然这些很好用，很简短，很明确，但是要使用的时候也要封装一个类；有了 Reflect，它封装好了：Reflect.has(obj,name),Reflect.deleteProperty(obj,name);

  - 3. 更加可靠的函数式执行方式：在 ES 中，要执行一个函数 f，并给它传一组参数 args，还要绑定 this 的话：

  ```
  f.applay(obj,args);
  //但是f的apply可能被重新定义成用户自己的apply，所以要这样写：
  Function.prototype.apply,call(f,obj,args);
  //上面这段代码太长，而且不好懂，有了Reflect可以更短更简明：
  Reflect.apply(f,obj,args);
  ```

  - 4. 可变参数形式的构造函数
  - 5. 控制访问器或者读取器的 this
  - 6. 避免直接访问`__proto__`
