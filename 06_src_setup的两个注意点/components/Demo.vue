<template>
    <h1>一个人的信息</h1>
    <h2>姓名：{{ person.name }}</h2>
    <h2>年龄：{{ person.age }}</h2>
    <button @click="test">测试触发一下Demo组件的Hello事件</button>
  </template>
  
  <script>
    import {reactive} from 'vue'
    export default {
      name:'Demo',
      props:['msg','myName'],
      emits:['hello'],
      setup(props,context) {
        // console.log('Demo setup',props);
        console.log('Demo setup',context);
        // console.log('Demo setup',context.attrs); //相当于Vue2中的$attrs
        // console.log('Demo setup',context.emit); //触发自定义事件
        console.log('Demo setup',context.slots); //插槽
        //数据
        let person = reactive({
          name:'张三',
          age:18,
        })

        //方法
        function test(){
            context.emit('hello',666)
        }


        
        //返回一个对象（常用）
        return {
          person,
          test
        }
  
      }
    }
  </script>
  