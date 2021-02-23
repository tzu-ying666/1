<template>   <!--html -->
  <div id = "app">
    <h1>ToDo List</h1>
    <img alt = "Vue logo" src="./assets/logo.png">
    <!-- 
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    -->
    <p>{{ message }}</p>
    <input v-model = "message">
    <button type="button" v-on:click="buttonClick">Button</button>
    <br>
    <a>{{arr}}</a>
    <div class = "list">
      <ul>
        <li v-for="item in arr" :key="item">{{ item }}</li>
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
      arr: [1,2,3,4,5,6],
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
      
      console.log(addTodo);
    }
  },
  created() {},

}

</script>

<style>  /*css*/
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.list{
  width:1000px;
  height:1000px;
  display: flex;
}
</style>
