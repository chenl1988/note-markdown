## slot插槽

- 父组件需要在子组件上放一些DOM，那么这些DOM是显示、不显示、在哪里显示、如何显示就是slot分发的活

- 在不使用slot的情况下，在子组件中的标签内添加的DOM是无效的

### 单个slot
```
//单个slot
<div id="app">
	<children>
			<span>123</span>
	</children>
</div>
<script>
var vm = new Vue({
	el:"#app",
	components:{
		children:{
			template:"<button><slot></slot>为了明确作用范围，所以使用button标签</button>"
		}
	}
})
</script>
//<button><span>12345</span>为了明确作用范围，所以使用button标签</button>
```
### 具名slot
```
<div id="app">
	<child-component>
		<h2 slot="header">标题</h2>
		<p>正文内容</p>
		<p>更多正文内容</p>
		<div slot="footer">底部信息</div>
	</child-component>
</div>
<script>
	Vue.component('child-component',{
		template:`
		<div class="component">
			<div class="header">
				<slot name="header"></slot>
			</div>
			<div class="main">
				<slot></slot><!-- 父组件没有具名指定的内容会显示在这里 -->
			</div>
			<div class="footer">
				<slot name="footer"></slot>
			</div>
		</div>
		`
	});
	var app = new Vue({
		el:'#app'
	})
</script>
```