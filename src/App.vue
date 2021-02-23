<template>   <!--html -->
  <div id = "app">
    <h1>My ToDo List</h1>
    <!--
    <img alt = "Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    -->
    <p>{{ message }}</p>
    <input v-model = "message">
    <button type="button" v-on:click="buttonClick">Button</button>
    <br>
    <div class = "list">
      <ul>
        <li v-for="(item, index) in arr" :key="item + '_' + index">
          第{{index}}項目 : {{ item }}
          <button type="button" v-on:click="buttonDelete(index)">ok</button>
        </li>
        
      </ul>
    </div>
  </div>
</template>

<script>    //js
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    // HelloWorld
  },  //找文件
  
  data() { 
    return {
      message: '' ,
      recordList: '',
      arr: ['123'],
    }
  },
  watch:{
    // info(x){
    // }
  },
  computed: {},
  methods: {
    buttonClick () {  //buttonClick: function ()
      const addTodo = this.message;
      this.recordList = addTodo;
      this.arr.push(addTodo);
      this.message = '';
      // console.log(addTodo);
    },

    buttonDelete (index) {  //index是arr位置
      this.arr.splice(index,1);
      this.message = '';
      console.log(index);
    },
  },
  created() {},

}

</script>

<style>  /*css*/
#app {
  font-family: 'Press Start 2P', cursive;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.list{
  display: flex;
  width: 1000px;
  height: 1000px;
  position: absolute;
  margin-top: 30px;
  margin-left: 600px
}
</style>
