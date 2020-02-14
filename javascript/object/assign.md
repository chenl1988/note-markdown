## Object.assign

- 语法：Object.assign(target, ...sources)
- 用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象

- 如果目标对象与源对象有同名属性，或多个源对象有同名属性，则后面的属性会覆盖前面的属性
```
const target = { a: 1, b: 1 };

const source1 = { b: 2, c: 2 };
const source2 = { c: 3 };

Object.assign(target, source1, source2);
target // {a:1, b:2, c:3}
```

- 如果只有一个参数，Object.assign会直接返回该参数
```
const obj = {a:1};
Object.assing(obj) === obj //true
```

- 如果该参数不是对象，则会先转成对象，然后返回
```
var a = Object.assign(2);
console.log(a);//{2}
```

- 由于undefined和null无法转成对象，所以如果它们作为参数，就会报错
```
Object.assign(undefined); // Cannot convert undefined or null to object
```