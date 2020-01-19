# Symbol

- Symbols本质上是一种唯一标识符，可用作对象的唯一属性名，这样其他人就不会改写或覆盖你设置的属性值。
- Symbol函数前是不能使用new命令，否则会报名，这是因为生成的Symbol是一个原始类型的值，不是对象，不能添加属性，基本上，它是一个类似于字符串的数据类型
- Symbol数据类型的特点是唯一性，即使是用同一个变量生成的值也不相等
```
let id = Symbol("id");
let id2 = Symbol("id");

console.log(id == id2);
```
- Symbol数据类型的另一个特点是隐藏性，for...in，object.keys()不能访问
- 但是也有能够访问的方法：Object.getOwnPropertySymbols()，方法会个数组，成员是当前对象的所有用途属性名的Symbol值
```
let id3 = Symbol("id");
let obj = {
  [id3]:'symbol',
  c:1
};
for(let option in obj){
  console.log(obj[option],"----");
}

let arr = Object.getOwnPropertySymbols(obj);
console.log(arr);
console.log(obj[arr[0]]);
```
- 虽然这样保证了Symbol的唯一性，但我们不排除希望能够多次使用同一个symbol值的情况。为此，官方提供了全局注册并登记的方法：Symbol.for()
```
let name1 = Symbol.for('name');//检测到未创建后新建
let name2 = Symbol.for("name");//检测到已创建后返回
console.log(name1 === name2);
```
- 通过这种方法就可以通过参数值获取到全局的symbol对象了，反之，能不能通过symbol对象获取参数值呢？可以通过Symbol.keyFor()
```
console.log(Symbol.keyFor(name1));
console.log(Symbol.keyFor(name2));
```
- **在创建Symbol类型数据时的参数只是作为标识使用，所以Symbol()也是可以的**