<template>
  <h2>姓名：{{ name }}</h2>
  <h2>年龄：{{ age }}</h2>
  <h2>薪资：{{ job.j1.salary }}k</h2>
  <button @click="name+='~'">增长姓名</button>
  <button @click="age++">增长年龄</button>
  <button @click="job.j1.salary++">增长薪资</button>
</template>
  
  <script>
    import {reactive,toRef,toRefs} from 'vue'
    export default {
      name:'Demo',
      setup() {
        //数据
        let person = reactive({
          name:'张三',
          age:18,
          job:{
            j1:{
              salary:20
            }
          }
        })

        // const name1 = person.name
        // console.log('%%%',name1);

        // const name2 = toRef(person,'name')
        // console.log('%%%',name2);

        // const x = toRefs(person)
        // console.log('*****',x);

        //返回一个对象（常用）
        return {
          // ...person或者age:person.age(=age:18) 会导致(外层)不是响应式
          //浅拷贝与深拷贝的区别（弹幕：浅拷贝只是第一层 深拷贝可以处理内部的引用数据类型）
          /* name:toRef(person,'name'),
          age:toRef(person,'age'),
          salary:toRef(person.job.j1,'salary') */
          ...toRefs(person)
        }
  
      }
    }
  </script>
  