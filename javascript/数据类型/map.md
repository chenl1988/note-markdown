# Map

- ES6标准新增的数据类型
- 它类似于对象，也是键值对的集合，但是键的范围不限于字符串，各种类型的值（包括对象）都可以当做键
- Map结构提供了**值-值**的对应，是一种更完善的Hash结构实现。
- 如果需要**键值对**的数据结构，Map和Object更合适
- Map的键实际上是跟内存地址绑定的，只要内存地址不末端，就视为两个键。这就解决了同名属性碰撞（clash）的问题。在扩展别人的库的时候，如果使用对象作为键名，就不用担心自己的属性和原作者的属性同名
```
var map = new Map();
var o = {p:"hello world"};
map.set(o,"content");

console.log("map.get:",map.get(o));
console.log("map.has:",map.has(o));
console.log("map.delete:",map.delete(o));
console.log("map.has:",map.has(o));

```
- **注意，只有对同一个对象的引用，Map结构才将其视为同一个键，这一点要非常小心**

```
/*
  下面的代码中的get和set方法，表面是针对同一个键，但实际上这是两个值，内存地址是不一样的，因些get方法无法读取该键，返回undefined
*/
var map2 = new Map();
map.set(['a'],555);
console.log(map.get(['a']));
console.log(map);
```
- 如果Map的键是一个简单类型的值（数字、字符串、布尔值），则只要两个值严格相等，Map将其视为一个键，包括0和-0
- 另外，虽然NaN不严格相等于自身，但Map将其视为同一个键
- Map实例属性和方法：size、set、get、has、delete、clear
- 遍历方法：keys()、values()、entries()、forEach()