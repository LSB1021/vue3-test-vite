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
        let person = reactive({
          name:'张三',
          age:18,
          job:{
            j1:{
              salary:20
            }
          }
        })

        //情况一：监视ref所定义的一个响应式数据
        /* watch(sum,(newValue,oldValue)=>{
          console.log('sum变了',newValue,oldValue);
        },{immediate:true}) */

        //情况二：监视ref所定义的多个响应式数据
        /* watch([sum,msg],(newValue,oldValue)=>{
          console.log('sum或msg变了',newValue,oldValue);
        },{immediate:true}) */



        /* 情况三：监视reactive所定义的一个响应式数据的全部属性
          111注意：此处无法正确的获取oldValue(打印出来的nvalue和ovalue一样) 学习时依旧
        */
        /* watch(person,(newvalue,oldvalue)=>{
          console.log('person变化了',newvalue,oldvalue);
        }),{deep:false} */  //此处deep配置有效

        /* 情况四：监视reactive所定义的一个响应式数据中的某个字符串数字等属性
          111注意：直接写person.age查不到，用箭头函数形式可以查到 
          222注意：直接写person.job可以查到监视（推测是因为person.job为reactive对象）
        */
        /* watch(()=>person.age,(newvalue,oldvalue)=>{
          console.log('person的age变化了',newvalue,oldvalue);
        }) */

        //情况五：监视reactive所定义的一个响应式数据中的某些字符串数字等属性
        /* watch(()=>[person.age,person.name],(newvalue,oldvalue)=>{
          console.log('person的age变化了',newvalue,oldvalue);
        }) */

        //特殊情况
        //(使用箭头函数形式写person.job对象时会识别不到内部变化，但是可以通过设置深度监视来解决)
        /* watch(()=>person.job,(newvalue,oldvalue)=>{
          console.log('person的job变化了',newvalue,oldvalue);
        },{deep:true}) */

        //返回一个对象（常用）
        return {
          sum,
          msg,
          person
        }
  
      }
    }
  </script>
  