## Array.from

- Array.from允许在Javascript集合（如：数组、类数组对象、或者是字符串、map、set等可迭代对象）是进行有用的转换

- `Array.from(arrayLike[,mapFunction[,thisArg]])`
  - arrayLike：必传参数，想要转换成数组的伪数组对象或可迭代对象
  - mapFunction：可选参数，mapFunction(item,index){...}是在集合中的每个项目上调用的函数。返回值将插入到新集合中。
  - thisArg：可选参数，执行回调函数mapFunction时this对象。这个参数很少使用

```
const someNumbers = { '0': 10, '1': 15, length: 2 };
Array.from(someNumbers, value => value * 2); // => [20, 30]
```

- Array.from的第一个参数可以是任意一个可迭代的对象

- Array.from可以接受一个map函数，并且这个map函数不会跳过值为undefined的数据值，这些特性给Array.from()提供了很多可能

```
Array.from('Hey');                   // => ['H', 'e', 'y']
Array.from(new Set(['one', 'two'])); // => ['one', 'two']

const map = new Map();
map.set('one', 1)
map.set('two', 2);
Array.from(map); // => [['one', 1], ['two', 2]]

```

### 将类数组转换成数组

- 类数组对象有：函数中的arguments关键字，或者是一个DOM集合
```
//对函数的参数求和
function sumArguments() {
    return Array.from(arguments).reduce((sum, num) => sum + num);
}

sumArguments(1, 2, 3); // => 6
```

### 克隆一个数组

- Array.from()可以很容易的实现数组的浅拷贝
```
const numbers = [3, 6, 9];
const numbersCopy = Array.from(numbers);

numbers === numbersCopy; // => false 这意味着numbers和numbersArray有着相同的项，但是它们有不同的数组对象
```

```
/* recursiveClone() 能够对数组的深拷贝，通过判断 数组的 item 是否是一个数组，
如果是数组，就继续调用 recursiveClone() 来实现了对数组的深拷贝 */
function recursiveClone(val){
  return Array.isArray(val)?Array.from(val,recursiveClone):val;
}
const numbers = [[0,1,2],["one","two","three"]];
const numbersClone = recursiveClone(numbers);

console.log(numbersClone);
console.log(numbers[0]===numbersClone[0]);
```

### 使用值填充数组

- 需要使用相同的值来初始化数组，那么 Array.from() 将是不错的选择
```
/* result 是一个新的数组，它的长度为3，数组的每一项都是0。
调用 Array.from() 方法，传入一个类数组对象 { length } 和 返回初始化值的 mapFunction 函数。 */
const length = 3;
const init = 0;
const result = Array.from({length},()=>init);

console.log(result);
```
- 有一个可以替代的方法array.fill，可以实现同样的功能
```
/* fill() 使用初始值正确填充数组。 */
const resultFill = Array(length).fill(init);
console.log(resultFill);
```
#### 使用对象填充数组

- 当初始化数组的每个项都应该是一个新对象时，Array.from() 是一个更好的解决方案
```
const resultA = Array.from({length},()=>({}));
const resultB = Array(length).fill({});
console.log(resultA); //[ {}, {}, {} ]
console.log(resultB);//[ {}, {}, {} ]
//由 Array.from 返回的 resultA 使用不同空对象实例进行初始化。之所以发生这种情况是因为每次调用时，mapFunction，即此处的 () => ({}) 都会返回一个新的对象。
console.log(resultA[0]===resultA[1]); //false
//fill() 方法创建的 resultB 使用相同的空对象实例进行初始化。不会跳过空项
console.log(resultB[0]===resultB[1]); //true
```

### 生成数字范围

- 可以使用 Array.from() 生成值范围。例如，下面的 range 函数生成一个数组，从0开始到 end - 1

```
/*  */
function range(end){
  return Array.from({length:end},(_,index)=>index);
}
console.log(range(4));
/* 在 range() 函数中，Array.from() 提供了类似数组的 {length：end} ，以及一个简单地返回当前索引的 map 函数 。这样你就可以生成值范围。 */
```

### 数组去重

- 由于Array.from()的入参是可迭代对象，因而我们可以利用其与Set结合来实现快速从数组中删除重复项
```
function unique(array){
  //new Set(array) 创建了一个包含数组的集合，Set 集合会删除重复项
  //因为 Set 集合是可迭代的，所以可以使用 Array.from() 将其转换为一个新的数组。
  return Array.from(new Set(array));
}
console.log(unique([1,1,2,2,3,3]));
```