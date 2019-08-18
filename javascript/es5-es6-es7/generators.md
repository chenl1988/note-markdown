## generators(生成器)

- 生成器是一种特殊的行为，实际上是一种设计模式，通过调用 next()方法来遍历一组有序的值。

- 想象一下，例如使用遍历器对数组[1,2,3,4,5]进行遍历。第一次调用 next()方法返回 1，第二次调用 next()方法返回 2，以此类推。当数组中的所有值都返回后，调用 next()方法将返回 null 或 false 或其他可能的值用来表示数组中的所有元素都已经遍历完毕

- yield：暂停代码
- next：继续执行代码

```
function* greeter() {
  yield "Hi";
  yield "How are you";
  yield "Bye"
}

const greet = greeter();
console.log(greet.next().value); //Hi
console.log(greet.next().value); //How are you
console.log(greet.next().value); //Bye
console.log(greet.next().value); //undefined

//使用生成器生成无限个值：

function* idCreator() {
  let i = 0;
  while (true) {
    yield i++;
  }
}
const ids = idCreator();
console.log(ids.next().value);
console.log(ids.next().value);
console.log(ids.next().value);
```
