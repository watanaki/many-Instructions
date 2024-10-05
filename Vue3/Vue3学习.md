# Vue3



## 响应式







## 例子



### computed 事件绑定

---

```vue
<template>
  <div>
    <p>{{ count }}</p>
    <p>{{ year }}</p>
    <button @click="count++">测试结果:{{ doubleCount }}</button>
  <ul>
    <li v-for="cur in newList" :key="cur.id">
      {{ cur.name }} 汇率为: {{ cur.rate }}
    </li>
  </ul>
  <input type="text" placeholder="文本测试" @change="inputChange">
  <button @click="Click">按钮</button>
  </div>
</template>

<script setup lang="ts">
import { computed, reactive, ref } from 'vue';

type Currency={
  id:string,
  name:string,
  rate:number,
};

const count=ref(100)
const year=ref<number|string>('1145');
const doubleCount =computed(()=>count.value*2);
const Currency=reactive<Currency[]>( [
    { id:"001", name:"USD", rate:1 },
    { id:"002", name:"RUB", rate:90 },
    { id:"003", name:"KZT", rate:440 },
    { id:"004", name:"SGD", rate:1.3 },
  ]);
  const newList=computed(()=> Currency.filter((el)=>el.rate>60));
  const inputChange=(e:Event)=>{
    console.log((e.target as HTMLInputElement).value);
  }
  const Click=(e:Event)=>{
    console.log((e.target as HTMLButtonElement).textContent);

  }
</script>


<style scoped>

</style>
```

### nextTick()

---

[nextTick](https://vue3js.cn/global/nextTick.html)
```vue
<template>
  <input type="text" ref="autoFocusInput" v-model="inputValue" placeholder="空" />
  <p>{{ inputValue }}</p>
</template>

<script setup lang="ts">
import { computed, nextTick, onMounted, reactive, ref } from 'vue';

let inputValue=ref<string>("TTT");
const autoFocusInput=ref<null|HTMLInputElement>(null);
// 组件被第一次挂载时调用
onMounted(async()=>{
  // 数据变动,但Vue的DOM更新是异步的
  inputValue.value="SSS";
  if(autoFocusInput.value)
  //  同步代码先于异步,此时拿到的是更新前的值
  console.log(autoFocusInput.value.value);
  // nextTick创建一个异步任务,该异步任务排在Dom更新的异步任务后面
  await nextTick();
  if(autoFocusInput.value)
  // 执行到这里保证Dom更新已完成,拿到的是新值
  console.log(autoFocusInput.value.value);

})
</script>
```

