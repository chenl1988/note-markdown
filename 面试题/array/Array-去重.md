## 数组去重

- Set 对象：允许存储任何类型的唯一值，无论是原始值或者是对象引用

  - `var j = [... new Set([1,2,4,4])]`

- sort() + reduce()

  ```
  var arr = [1, 2, 1, 2, 3, 5, 4, 5, 3, 4, 4, 4, 4];
  var init = [];

  var result = arr.sort().reduce((init, current) => {
    console.log("init:", init, "current:", current);
    if (init.length === 0 || init[init.length - 1] !== current) {
      init.push(current);
    }
    return init;
  }, []);
  console.log(result);
  ```
