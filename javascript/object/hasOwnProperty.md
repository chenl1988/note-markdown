## hasOwnProperty

- hasOwnProperty 检测一个对象是否含有特定的自身属性；和 in 运算符不同，**该方法会忽略掉那些从原型链上继承到的属性**

```
// 使用Object.defineProperty创建对象属性
let obj = {};
Object.defineProperty(obj, "name", {
  value: "fff",
  enumerable: true
})
let obj2 = Object.create(obj);
obj2.age = 20;
for (key in obj2) {
  console.log(key); //name,age
}
console.log("------------");
for (key in obj2) {
  if (obj2.hasOwnProperty(key)) {
    console.log(key); //age
  }
}
//如果继承的对象属性是通过Object.defineProperty创建的，并且enumerable未设置成true，那么for..in依然不能枚举出原型上的属性
console.log("=================");
// 普通创建属性
let obj3 = {};
obj3.name = "jjj";
let obj4 = Object.create(obj3);
obj4.age = 18;
for (key in obj4) {
  console.log(key); //name,age
}
console.log("--------------");
for (key in obj4) {
  if (obj4.hasOwnProperty(key)) {
    console.log(key); //age
  }
```
