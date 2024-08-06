<template>
  <h2>当前求和为：{{ sum }}</h2>
  <button @click="sum++">点我+1</button>
  <hr>
  <h2>当前的信息为：{{ msg }}</h2>
  <button @click="msg+='!'">修改信息</button>
  <hr>
  <h2>姓名：{{ person.name }}</h2>
  <h2>年龄：{{ person.age }}</h2>
  <h2>薪资：{{ person.job.j1.salary }}k</h2>
  <button @click="person.name+='~'">增长姓名</button>
  <button @click="person.age++">增长年龄</button>
  <button @click="person.job.j1.salary++">增长薪资</button>
</template>
  
  <script>
    import {ref,reactive,watch} from 'vue'
    export default {
      name:'Demo',
      setup() {
        //数据
        let sum = ref(0)
        let msg = ref('你好啊')
        let person = ref({
          name:'张三',
          age:18,
          job:{
            j1:{
              salary:20
            }
          }
        })

        console.log(person);

        //sum不能.value，使用相当于监视let sum = ref(0)中的0
        watch(sum,(newValue,oldValue)=>{
          console.log('watch',newValue,oldValue);
        })

        //ref定义的数据对象类型的需要开启深度监视才能看到
        watch(person,(newValue,oldValue)=>{
          console.log('watch',newValue,oldValue);
        },{deep:true})

        //person.value检测的不再是ref所定义的数据了，而是ref里面调用reactive定义的数据
        watch(person.value,(newValue,oldValue)=>{
          console.log('watch',newValue,oldValue);
        })


        //返回一个对象（常用）
        return {
          sum,
          msg,
          person
        }
  
      }
    }
  </script>
  