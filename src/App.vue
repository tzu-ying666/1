<template>   <!--html -->
  <div id = "app">
    <h1>My ToDo List</h1>
    <!--
    <img alt = "Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    -->
    <p>{{ message }}</p>
    <input v-model = "message">
    <button type="button" v-on:click="buttonClick">Add Todo</button>
    <br>
    <div v-show="isShow">No ToDos, ya!</div>
    <br>
    <div class = "list">
      <ul>
        <li v-for="(item, index) in arr" :key="item + '_' + index">
        <input type="checkbox" v-bind:value="item" name=item v-model="checkedList" />  <!-- v-bind:value = :value -->
          第{{index}}項目 : {{ item }}
            <div v-if="recordBtnState === 'all'">
              all 的項目 : {{ arr }} 
            </div>
            
            <div v-else-if="recordBtnState === 'completed'">
              complete 的項目 : {{ checkedList }}
            </div>

            <div v-else-if="recordBtnState === 'Incompleted'">
              complete 的項目 : {{ checkedList }}
              <button></button>
            </div>
          <button type="button" v-on:click="buttonDelete(index)">Delete</button>  <!-- v-on:click = @click -->
        </li>
      </ul>
    </div>
    <div class = "complete">
      <button type="button" v-on:click="checkAll">All</button>
      <button type="button" v-on:click="checkCompleted">Completed</button>
      <button type="button" v-on:click="checkIncomplete">Incomplete</button>
    </div>

    <homeWork />
  </div>
</template>

<script>    //js
import homeWork from './components/homeWork.vue'

export default {
  name: 'App',
  components: {
    homeWork
  },  //找文件
  
  data() { 
    return {
      message: '' ,
      recordList: '',
      arr: [],
      isShow: true,
      checkedList: [],
      inCompleteList: [],
      recordBtnState: 'all', // all、completed
    }
  },

  watch: {
    checkedList (arrList) {
      console.log('已完成項目:', arrList);
      for (let ii = 0; ii < arrList.length; ii++) {
        let loopTarget = arrList[ii];
        let position = this.inCompleteList.indexOf(loopTarget);

        if (position !== -1) {
          this.inCompleteList.splice(position, 1);
        }

      console.log(position);
      }
      console.log('尚未完成的項目: ', this.inCompleteList);
    }
  },
  computed: {},
  methods: {
    buttonClick () {  //buttonClick: function ()
      const addTodo = this.message;
      this.recordList = addTodo;
      this.arr.push(addTodo);  //將addTodo的值push到arr陣列
      this.message = '';
      // console.log(addTodo);
      this.inCompleteList.push(addTodo);
      this.isShow2();
    },

    buttonDelete (index) {  //index是arr位置
      this.arr.splice(index,1);  //將arr陣列的值拉掉
      this.message = '';
      console.log(index);
      this.isShow2();
    },

    isShow2 () {
      const length = this.arr.length;
      if (length === 0) {
          this.isShow = true;
      } else {
          this.isShow = false;
      }
    },

    checkAll () {
      console.log('check all list');
      this.recordBtnState = 'all';
    },
    checkCompleted () {
      console.log('check completed list');
      this.recordBtnState = 'completed';
    },
    checkIncomplete () {
      console.log('check other list');
      // this.checkedList = this.checkedList.filter(arr => {
      //   return
      // })
      this.recordBtnState = 'Incompleted';
    }
    
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

/* .list {
  display: flex;
  width: auto;
  height: auto;
  position: absolute;
  margin-top: 30px;
  padding-left: 600px;
  text-align: left;
}

.complete {
  width: 300px;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  padding-left: 600px;
} */
</style>
