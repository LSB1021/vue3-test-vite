<template>
    <div class="child">
      <h3>我是Child组件</h3>
      {{ sum }}
    </div>
  </template>
  
<script>
    import {ref} from 'vue'
    export default {
        name:'Child',
        /* setup(){
            let sum = ref(0)
            return new Promise((resolve,reject)=>{
                setTimeout(()=>{
                    resolve({sum})
                },3000)
            })
        } */ //异步操作，在App组件内将此组件定义为了异步组件，故可以使用异步和suspense组件
        async setup(){
            let sum = ref(0)
            let p = new Promise((resolve,reject)=>{
                setTimeout(()=>{
                    resolve({sum})
                },3000)
            })
            return await p
        }
    }
</script>

<style>
    .child{
        background-color: skyblue;
        padding: 10px;
    }
</style>