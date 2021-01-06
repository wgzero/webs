# Vue3文档

### 1.创建实例

```html
import { createApp } from "vue"
import App from "./App.vue"
const app = createApp(App)
app.mount('#app')
```

### 2.全局调用方法

```vue
// main.ts页面
import { createApp } from "vue"
import App from "./App.vue"
const app = createApp(App)
app.mount('#app')
// 扩展方法
app.config.globalProperties.$http = () => {
  console.log("xxx")
}

// test.vue测试页面

<template>
  <div class="main">
    test
  </div>
</template>

<script lang="ts">
import { defineComponent, getCurrentInstance, onMounted } from "vue"
export default defineComponent({
  name: "",
  props: {},
  component: {},
  setup(){
    const { ctx }  = getCurrentInstance() as any
    onMounted(() => {
      console.log("ctx---", ctx)
      ctx.$http()
    })
    return {}
  }
})
</script>
```







### 3.emits用法

```html
// sonTest.vue
<template>
  <div class="main" @click="handleCancel">
    test
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive } from "vue"
export default defineComponent({
  name: "",
  // 外面组件要使用的方法
  emits: ["handleCancelSon"],
  setup(props, { emit, attrs }){
    const state = reactive({
      num: 1,
      visiable: false
    })
    // 取消
    const handleCancel = () => {
      // 触发方法并返回值
      emit("handleCancelSon", state.visiable)
    }
    return {
      state,
      handleCancel
    }
  },
})
</script>
<style scoped>
.main{
  width: 100px;
  height: 50px;
  background: red;
  color: white;
  text-align: center;
  line-height: 50px;
}
</style>

//father.vue
<template>
  <div class="main">
    test---
    <h1 @click="handleShow">{{ state.num }}</h1>
    <son-test @handleCancelSon="handleCancalFather" v-if="state.fatherVisiable"></son-test>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive } from "vue"
import sonTest from "./components/sonTest.vue"
export default defineComponent({
  components: {
    sonTest
  },
  setup(){
    const state = reactive({
      num: 1,
      fatherVisiable: true
    })

  // 消失
    const handleCancalFather = (value: boolean) => {
      state.fatherVisiable = value
    }
    // 显示
    const handleShow = () => {
      state.fatherVisiable = !state.fatherVisiable
    }
    return {
      state,
      handleCancalFather,
      handleShow
    }
  },
})
</script>
```

### 4.页面数据定义

```html
// index.vue文件
<template>
  <div class="main">
    main
    <h1>{{ num }}</h1>
    <h2>{{ age1 }}</h2>
    <h2>{{ handleAge }}</h2>
    <div class="box" :ref="dom">123</div>
    <test></test>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, nextTick, onMounted, reactive, ref, toRef, toRefs, watch } from "vue"
// 6.tsx写法 tsx组件
import test from "./components/test"
/** 
defineComponent: 已启用类型推断
0.setup函数入口
1.ref：需要通过.value来进行赋值，但是在html模板中则可以直接写
2.reactive： 通过对象点的方式来赋值
3.toRefs： 在return中将reactive的值打散，在html模板中直接使用值
4.computed:使用场景 
A.就是将已知的数据变成新的数据返回
5.watch:使用场景
A.根据数据的实时变化，做出反应并显示
6.h函数 <==> tsx写法
7.获取dom节点
*/

export default defineComponent({
  name: "test1",
  props: {},
  components: {
    test
  },
  // 0.setup
  setup(){
    // 1.ref
    const age1 = ref(0)
    const age2 = ref(5)
    // 2.reactive
    const state = reactive({
      num: 1
    })
    onMounted(() => {
      age1.value = 10
      state.num = 25
    })

    // 4.computed
    const handleAge = computed(() => {
      return age1.value + age2.value
    })
    // 5.watch
    watch(() => state.num, (newVal, oldVal) => {
      console.log("newVal", newVal)
      console.log("oldVal", oldVal)
    })

    // 7.获取dom节点
    let refs = ""
    const dom = (el: any) => {
      refs = el
    }

    nextTick(() => {
      console.log("refs", refs) // 
    })


    return {
      // 3.toRefs
      ...toRefs(state),
      age1,
      handleAge,
      dom
    }
  }
})
</script>

// test.tsx文件
import { defineComponent, ref, h, reactive } from "vue"
// h函数参数：（type, props, children）类型 值 子节点 
export default defineComponent({
  setup(){
    const num = ref(5)
    const state = reactive({
      name: "summer"
    })
    return () => h("div", [num.value, "---" ,state.name])
  }
})
```



### 4.teleport瞬移提升节点

```html
<div class="main">
	<div class="one">one</div>
	<div class="two">two</div
</div>
// 和main盒子在同一层
<teleport to="main"></teleport>
```

### 5.Vue3生命周期

### 6.vue-router的使用

### 7.vuex的使用

### 5.

### 6.

### 7.

### 8.

### 9.

### 10.

### 11.

### 12.