<template>
  <Demo @hello="showHelloMsg" msg="你好啊" myName="lsb">
    <template v-slot:qwe>
      <span>lsb</span>
    </template>
    <template v-slot:asd>
      <span>lsb</span>
    </template>
  </Demo>
</template>

<script>
  import Demo from './components/Demo.vue';
  export default {
    name:'App',
    components:{
      Demo
    },
    setup(){
      function showHelloMsg(value){
        alert(`你好啊，你触发了hello事件，我收到的参数时：${value}`)
      }

      return{
        showHelloMsg
      }
    }
  }
</script>
