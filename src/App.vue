<template>
  <div class="app">
    <h3>我是App组件</h3>
    <Suspense>
      <template v-slot:default> <!--真正展示东西的地方-->
        <Child/>
      </template>
      <template v-slot:fallback> <!--当没加载出来展示的地方-->
        <h3>稍等，加载中....</h3>
      </template>
    </Suspense>
  </div>
</template>

<script>
    // import Child from './components/Child.vue';//静态引入
    import { defineAsyncComponent } from 'vue';  
    const Child = defineAsyncComponent(() => import('./components/Child.vue'));  //动态引入（异步引入）
    export default {
        name:'App',
        components:{Child},
}
</script>

<style>
    .app{
        background-color: gray;
        padding: 10px;
    }
</style>