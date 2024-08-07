<template>
  <h4>当前求和为：{{ sum }}</h4>
  <button @click=sum++>点我++</button>
  <hr>
  <h2>姓名：{{ name }}</h2>
  <h2>年龄：{{ age }}</h2>
  <h2>薪资：{{ job.j1.salary }}k</h2>
  <h3 v-show="person.car">座驾信息：{{ person.car }}</h3>
  <button @click="name+='~'">增长姓名</button>
  <button @click="age++">增长年龄</button>
  <button @click="job.j1.salary++">增长薪资</button>
  <button @click="showRawPerson">输出最原始的person</button>
  <button @click="addCar">给人添加一台车</button>
  <button @click="person.car.name+='!'">换车名</button>
  <button @click="person.car.price++">换价格</button>
</template>
  
  <script>
    import {reactive,ref,toRefs,toRaw,markRaw} from 'vue'
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

        function showRawPerson(){
          console.log(toRaw(person)); //toRaw只能处理reactive缔造的响应对象
        }

        function addCar(){
          let car = {name:'奔驰',price:'40'}
          person.car = markRaw(car)  //需求：当有一堆很复杂的对象中，给了你数据不需要响应式，可以使用markRow提升效率
        }

        //返回一个对象（常用）
        return {
          ...toRefs(person),
          person,//把整个person响应对象交出去，当person更新时setup会调用第二次，就能实现person对象ref
          sum,
          showRawPerson,
          addCar
        }
  
      }
    }
  </script>
  