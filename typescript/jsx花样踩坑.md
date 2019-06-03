### jsx花样作死之旅

配置环境略过

为什么要使用jsx：
	jsx -> 
	vue + typescript ->
	vue 3.0 ->
	react + typescript ->
	react native

假设已熟练使用template语法，v-for v-if v-model 

[官网地址](https://cn.vuejs.org/v2/guide/render-function.html)

---

##### v-if

可以通过变量来判断
	
```	
bRender: boolen = true
	render (h, context) {
	return (
		<div>
			{
				if(this.bRender)
					return h('div', 'div')
			}
		</div>
		)
}
```
	上述{}内容相当于 <div v-if="bRender"></div>
