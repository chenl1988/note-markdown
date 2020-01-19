## set-map

- Set 和 Map 主要的应用场景在于数据重组和数据储存

- Set 是一种叫做集合的数据结构

- Map 是一种叫做字典的数据结构

- 集合与字典的区别：

  - 共同点：集合、字典可以储存不重复的值

  - 不同点：集合是以[value,value]的形式储存元素，字典是以[key,value]的形式储存

- 总结：

  - Set:
    - 成员唯一、无序且不重复
    - [value,value]，键值与键名完成一致（或者说只有键值，没有键名）
    - 可以遍历，方法有：add、delete、has
  - WeakSet:
    - 成员都是对象
    - 成员都是弱引用，可以被垃圾回收机制回收，可以用来保存 DOM 节点，不容易造成内存泄漏
    - 不能遍历，方法有：add、delete、has
  - Map
    - 本质上是键值对的集合，类似集合
    - 可以遍历，方法很多可以跟各种数据格式转换
  - WeakMap
    - 只接受对象作为键名（null 除外），不接受其他类型的值作为键名
    - 键名是弱引用，键值可以是任意的，键名所指向的对象可以被垃圾回收，此时键名是无效的
    - 不能遍历，方法有 get、set、has、delete

- 扩展：Object 与 Set、Map

  - Object 与 Set

  ```
  //Object
  const properties1 = {
    'width':1,
    'height':2
  }
  console.log(properties1['width']?true:false);//true

  //Set
  const properties2 = new Set();
  properties2.add('width');
  properties2.add('heigth');
  console.log(properties2.has('width'));//true
  ```

  - Object 与 Map，js 中的对象（object），本质上是键值对的集合（hash 结构）

  ```
  const data = {};
  const element = document.getElementsByClassName("App");

  data[element] = "metadata";
  console.log(data['[object HTMLCollection]']); //metadata
  ```

  但当以一个 DOM 节点作为对象 data 的键，对象会被自动转化为字符串[Object HTMLCollection]，所以说，Object 结构提供了**字符串-值**对应，Map 则提供了**值-值**的对应
