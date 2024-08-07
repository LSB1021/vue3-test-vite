<template>
  <h4>当前求和为：{{ sum }}</h4>
  <button @click=sum++>点我++</button>
  <hr>
  <h2>姓名：{{ name }}</h2>
  <h2>年龄：{{ age }}</h2>
  <h2>薪资：{{ job.j1.salary }}k</h2>
  <button @click="name+='~'">增长姓名</button>
  <button @click="age++">增长年龄</button>
  <button @click="job.j1.salary++">增长薪资</button>
</template>
  
  <script>
    import {reactive,ref,toRefs,readonly,shallowReadonly} from 'vue'
    export default {
      name:'Demo',
      setup() {
        //数据
        let sum = ref(0)
        let person = reactive({
          name:'张三',
          age:18,
          job:{
            j1:{
              salary:20
            }
          }
        })

        //readonly函数接受一个响应式数据，此处效果为person内的所有数据都不允许修改
        // person = readonly(person)  

        //shallowReadonly只考虑对象里的第一层数据不能修改，第一层之后的数据可以修改
        // person = shallowReadonly(person)  

        // sum = readonly(sum)
        // sum = shallowReadonly(sum)

        //返回一个对象（常用）
        return {
          ...toRefs(person),
          sum
        }
  
      }
    }
  </script>
  