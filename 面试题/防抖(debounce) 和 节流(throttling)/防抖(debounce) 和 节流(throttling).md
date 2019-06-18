## 防抖(debounce) 和 节流(throttling)

- **防抖和节流是针对响应跟不上触发频率这类问题的两种解决方案**。在给 DOM 绑定事件时，有些事件是无法控制触发频率的。如鼠标移动事件 onmousemove,滚动滚动条事件 onscroll,窗口大小改变事件 onresize，瞬间的操作都会导致这些事件会被高频触发。如果事件的回调较为复杂，就会导致响应跟不上触发，出现页面卡顿，假死现象。在实时输入时，如果我们绑定 onkeyup 事件发请求去服务端检查，用户输入过程中，事件的触发频率也会很高，会导致大量的请求发出，响应速度会大大跟不上触发。

- 针对此类快速连续触发和不可控的高频触发问题，debounce 和 throttling 给出了两种解决策略

### debounce，去抖动

- debounce，去抖动。策略是当事件被触发时，设定一个周期延迟执行动作，若期间又被触发，则重新设定周期，直到周期结束，执行动作。这是 debounce 的基本思想，在后期又扩展了前缘 debounce，即执行动作在前，然后设定周期，周期内有事件被触发，不执行动作，而周期重新设定

- debounce 的特点是当事件快速连续不断触发时，动作只会执行一次。延迟 deounce，是在周期结束时执行，前缘 debounce，是在周期开始时执行。但当触发有间断，且间断大于我们设定的时间间隔时，动作就会有多次执行。

- 通过函数防抖，解决了多次触发事件时的性能问题

```
<div>111</div>
<div>222</div>
<div>333</div>
<div>444</div>
<div>555</div>
<div>666</div>
<div>777</div>
<script>
  function debounce_2(method, delay) {
    let timer = null;
    return function () {
      let selt = this;
      args = arguments;
      timer && clearTimeout(timer);
      timer = setTimeout(function () {
        method.apply(self, args);
      }, delay);
    }
  }

  window.onscroll = debounce_2(function () {
    let scrollTop = document.body.scrollTop || document.documentElement.scrollTop;
    console.log("滚动条位置：" + scrollTop);
  }, 1000)
</script>
```

### 节流 throttling

- 节流的策略是，固定周期内，只执行一次动作，若有新事件触发，不执行。周期结束后，又有事件触发，开始新的周期
- 节流策略也分前缘和延迟两种。与 debounce 类似，延迟是指周期结束后执行动作，前缘是指执行动作后再开始周期
