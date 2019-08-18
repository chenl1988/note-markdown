## 随机数

### 预备知识

- Math.ceil(n); //向上取整。返回大于等于 n 的最小整数
- Math.floor(n); //向下取整。返回为 n 的整数部分
- Math.round(n);// 四舍五入。返回为 n 四舍五入后的整数
- Math.random(n);//0.0~1.0 之间的一个伪随机数。【包含 0，不包含 1】//比如 0.8647578968666494

---

- `Math.ceil(Math.random()*10);`//获取从 1 到 10 的随机整数，取 0 的概率极小
- `Math.floor(Math.random() * 10);`//可均衡获取 0 到 9 的随机整数
- `Math.round(Math.random());`//可均衡 0 或 1 的随机整数（因为 random()生成的是 0-1 的数，四舍五入后只有 0 或 1）
- `Math.round(Math.random() * 10)`//可基本均衡获取 0~10 的随机整数，其中获取最小值 0 和最大值 10 的几率少一半

---

- parseInt(),Math.floor(),Math.ceil()和 Math.round()都可以取得整数，但是 parseInt()和 Math.floor()结果都是向下取整

### 生成[n,m]的随机整数

- 生成【1，max】的随机数，公式如下：

  - `parseInt(Math.random()*max,10)+1`
  - `Math.floor(Math.random()*max)+1`
  - `Math.ceil(Math.random()*max)`

- 生成【0，max】的随机数，公式如下：

  - `parseInt(Math.random()*(max+1),10);`
  - `Math.floor(Math.random()*(max+1));`

- 生成【min,max】的随机数，公式如下：
  - `parseInt(Math.random()*(max-min+1)+min,10)`;
  - `Math.floor(Math.random()*(max-min+1)+min)`;

```
function randomNum(min, max) {
  switch (arguments.length) {
    case 1:
      return parseInt(Math.random() * min + 1, 10);
    case 2:
      return parseInt(Math.random() * (max - min + 1) + min, 10);
  }
}
console.log(randomNum(5, 10));
```
