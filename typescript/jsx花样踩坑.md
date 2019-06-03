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

```	 可以通过变量来判断

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

上述{}内容相当于 
`<div v-if="bRender"></div>`


##### v-model

```	 可以通过变量来判断
	placeholder: stirng='说点啥。。。'
	inputMsg: string = ''

	divClick(text:string = '333'){
		console.log(text)
	}
    <input placeholder={this.placeholder}
      value={this.inputMsg}

      on-keyup={(val) => {
        this.inputMsg = val.target.value.trim()
        var temp = this.inputMsg +'sd'
        if (val.keyCode === 13 ) this.divClick(temp)
      }}/>

```

其中： 
	value={this.inputMsg} 是设置默认值
	on-keyup={} 是监听键盘函数，如果不需要监听，可以用：
	`on-input={}` 来代替
上述{}内容相当于 
`<input type='text' v-model="inputMsg" :placeholder="placeholder" @keyup.enter="divClick"></div>`
无视字符串处理。。。

##### v-for
 
   ceshis: Array<Number> = [100,220, 5, 30]
   render (h, context) {
	  return (
	    <div>
	    ```
	    {
          this.ceshis.map((it, index) => {
            if(index !== 1)
              return h('div',
                { class:[ {'323': true, 'ceshi': true}, 'asdfasd' ],
                  attrs:{dataParm: 'csss'},
                  key: index,
                  on:{ click: () => {
                      console.log(this.ceshis[index]);
                    }}
                }, `heel${it}`)
            else
              return <li key={index} on-click={() => {console.log(this.ceshis);} }>{it},,,,haha, { `heel${it}`}</li>
          })
        }
        ```
	    </div>
   )
   }
   1. array.map()循环渲染
   2. if() 条件渲染
   3. jsx 函数
   		- class:[{'323': true, 'ceshi': true}, 'asdfasd'] 对象和字符串组成的数组，类似bind：class
   		- @click： 要写成on:{click:() =>{}}的形式
   		注意：若写成on:{click:{this.divClick('ss')}} 会报错
   4. jsx 模板
   		绑定的变量要用{}而不是{{}}，@click : on-click

##### 组件传参

```
props: ['param']
mounted() {
	console.log(this.$attrs.param);
}
```

##### 组件回调
`this.$emit('emites', this.ceshis[index])`

##### 完整示例
```
<script lang="tsx">
import { Vue, Component } from 'vue-property-decorator'

@Component({

})
export default class FilterItem extends Vue {

  ceshiMsg: string = 'testString'
  inputMsg: string = '2352354'
  placeholder: string = 'placeholder'
  ceshis: Array<Number> = [100,220, 5, 30]
  props: ['param']
  divClick(con: string = '333') {
    console.log(con);
  }
  mounted() {
    console.log(this.$attrs.param);
  }
  render (h, context) {
    return (
      <div class='testClass'>
        <div>这条是jsx{this.$attrs.param}</div>
        <input placeholder={this.placeholder}
          value={this.inputMsg}
          on-keyup={(val) => {
            this.inputMsg = val.target.value.trim()
            var temp = this.inputMsg +'sd'
            if (val.keyCode === 13 ) this.divClick(temp)
          }}/>
        <div on-click={() => {this.divClick('bbbbb')}}>11111111111111111</div>
        {
          this.ceshis.map((it, index) => {
            console.log(it);
            if(index !== 1)
              // return <li key={it}>haha,{it}</li>
              return h('div',
                { class:[ {'323': true, 'ceshi': true}, 'asdfasd' ],
                  attrs:{dataParm: 'csss'},
                  key: index,
                  on:{ click: () => {
                      this.$emit('emites', this.ceshis[index])
                    }}
                }, `heel${it}`)
            else
              return <li key={index} on-click={() => {console.log(this.ceshis);} }>{it},,,,haha, { `heel${it}`}</li>
          })
        }
      </div>
    )
  }
}
```




