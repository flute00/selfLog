### vue + typescript

配置环境略过

```
<template>
  <div class='dashboard-container'>
    <div class='goback' @click='goback'>返回</div>
    <div class='dashboard-text'>test1</div>
    <div class='test' @click='showSelfMsgBox'>测试自定义全局弹窗</div>
    <div class='sdf' @click='gotest2'>sdfsdfsf</div>
    <JSX :param='ceshi' @emites='getEvent'></JSX>
  </div>
</template>

<script lang='ts'>

import { Component, Vue } from 'vue-property-decorator'
import JSX from './jsx.vue'

/*import { State,
  Getter,
  Action,
  Mutation,
  namespace } from 'vuex-class'*/

@Component({
  components: {
    JSX
  }
})
export default class Test1 extends Vue {
  @Getter device
  @Getter avatar
  @State('app') sname:string
  @Action('FedLogOut') actionFedOut
  @Mutation('SET_AVATAR') mutationSET_AVATAR


  msg: string = '34535'
  ceshi: Number = 123456

  mounted() {
    console.log('mounted', this.msg)
    console.log(this.device, this.avatar);
    console.log(this.sname)
    // console.log(this.$store.state.user.name);
  }

  getEvent(pa) {
    console.log(pa)
  }

  gotest2() {
    this.$router.push('test2')
  }

  goback():string {
    // this.$router.goBack()
    return 'tes222t'
  }

  showSelfMsgBox():void {
    this.$selfMsgBox(this.goback(), (res) => {
      console.log('reback fun:' + res)
    })
  }
}
</script>
<style rel='stylesheet/scss' lang='scss' scoped>
.dashboard {
  &-container {
    // margin: 10px;
    font-size: 15px
  }
  &-text {
    font-size: 10px;
    line-height: 46px
  }
}
</style>

```

---

### template、style 写法照旧

### script lang='ts'
1. import { Component, Vue } from 'vue-property-decorator'
2. @Prop @Model @Watch @Inject @Provide @Emit [官网地址](https://github.com/kaorun343/vue-property-decorator)
```
@Component({
  components: {
    JSX
  }
})
```

### vuex用法
1. 标准vue中的用法可以正常使用
2. 
```
@Getter avatar   // 对应getter里面内容
@State('app') sname:string
@Action('FedLogOut') actionFedOut
@Mutation('SET_AVATAR') mutationSET_AVATAR
mounted() {
  console.log('mounted', this.msg)
  console.log(this.sname)
  console.log(this.device, this.avatar);
  this.actionFedOut()
  this.mutationSET_AVATAR('dddd')
}
```





