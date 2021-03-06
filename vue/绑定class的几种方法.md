## 绑定 class 的几种方法

- 对象语法，设置一个对象

  ```
  <div :class="{ 'active':isActive }"></div>
  <!-- 对象中可以传入多个属性，动态切换class -->
  <div :class="{ 'active':isActive,'error':isError }"></div>
  ```

  ***

  - 当:class 的表达式过长或者逻辑复杂时，还可以绑定一个计算属性

  ```
  <div :class="classes"></div>

  computed:{
    classes:function(){
      return{
        active:this.isActive && !this.error,
        'text-fail':this.error && this.error.type == 'fail'
      }
    }
  }
  <!-- 除了计算属性，也可以直接绑定一个Object类型的数据，或者使用类似计算属性的methods -->
  ```

- 数组语法

  ```
  <div :class="[activeCls,errorCls]"></div>
  <!-- 也可以使用三元表达式根据条件切换class -->
  <div :class="[isActive?activeCls:'',errorCls]"></div>
  ```

  - 在开发过程中，如果表达式较长或逻辑复杂，应该尽可能地优先使用计算属性

- 在组件上使用：如果直接在自定义组件上使用 class 或:class，样式规则会直接应用到这个组件的根元素上。

---

- 绑定内联样式，CSS 属性名称使用驼峰命名（camelClass）或短横分隔命名（kebab-case）

```
<div :style="{'color':color,'fontSize':fontSize+'px'}">文本</div>
data:{
  color:'red',
  fontSize:14
}
```
