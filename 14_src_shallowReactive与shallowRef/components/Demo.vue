<template>
  <h4>当前的x.y的值是：{{ x.y }}</h4>
  <button @click="x={y:888}">点我替换x</button>
  <button @click="x.y++">点我x.y+1</button>
  <hr>
  <h2>姓名：{{ name }}</h2>
  <h2>年龄：{{ age }}</h2>
  <h2>薪资：{{ job.j1.salary }}k</h2>
  <button @click="name+='~'">增长姓名</button>
  <button @click="age++">增长年龄</button>
  <button @click="job.j1.salary++">增长薪资</button>
</template>
  
  <script>
    import {reactive,ref,toRefs,shallowRef,shallowReactive} from 'vue'
    export default {
      name:'Demo',
      setup() {
        //数据
        // let person = shallowReactive({  //使用shallowReactive，浅层代理，只考虑第一层数据的响应式
        let person = reactive({
          name:'张三',
          age:18,
          job:{
            j1:{
              salary:20
            }
          }
        })

        let x = shallowRef({
          y:0
        })
        console.log('********',x);


        //返回一个对象（常用）
        return {
          person,
          ...toRefs(person),
          x
        }
  
      }
    }
  </script>
  