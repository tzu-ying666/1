<template>   <!--html -->
  <div id = "app">
    <h1>My ToDo List</h1>
    <!--
    <img alt = "Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    -->
    <p>{{ message }}</p>
    <input type="text"
     v-model = "message"
     @keydown.enter="buttonClick">
    <button type="button" id="button" v-on:click="buttonClick">Add Todo</button>
    <br>
    <div v-show="isShow">No ToDos, ya!</div>
    <br>
    <div class = "list">
      <ul>
        <div v-if="recordBtnState === 'all'">
          <li v-for="(item, index) in arr" :key="item + '_' + index">
            <input type="checkbox" v-bind:value="item" name=item v-model="checkedList" />  <!-- v-bind:value = :value -->
            <!--第{{index}}項目 :--> {{ item }}
            <button type="button" id="button1" v-on:click="buttonDelete(index)">Delete</button>  <!-- v-on:click = @click -->
          </li>
        </div>
        
        <div v-else-if="recordBtnState === 'completed'">
          <li v-for="(item, index) in checkedList" :key="item + '_' + index">
            <input type="checkbox" v-bind:value="item" name=item v-model="checkedList" />  <!-- v-bind:value = :value -->
            <!--第{{index}}項目 :--> {{ item }}
            <button type="button" v-on:click="buttonDelete(index)">Delete</button>  <!-- v-on:click = @click -->
          </li>
        </div>

        <div v-else-if="recordBtnState === 'Incompleted'">
           <li v-for="(item, index) in inCompleteList" :key="item + '_' + index">
            <input type="checkbox" v-bind:value="item" name=item v-model="checkedList" />  <!-- v-bind:value = :value -->
            <!--第{{index}}項目 :--> {{ item }}
            <button type="button" v-on:click="buttonDelete(index)">Delete</button>  <!-- v-on:click = @click -->
          </li>
        </div>
      </ul>
    </div>
    <div class = "complete">
      <button type="button" id="button2" v-on:click="checkAll">All</button>
      <button type="button" id="button2" v-on:click="checkCompleted">Completed</button>
      <button type="button" id="button2" v-on:click="checkIncomplete">Incomplete</button>
    </div>

    <homeWork></homeWork>
  </div>
</template>

<script>    //js
import homeWork from './components/homeWork.vue'

// <li v-for="(item, index) in arr" :key="item + '_' + index"></li>
//               {{ item }} 

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

  watch: {  //監聽有無動作
    checkedList (arrList) {
      console.log('已完成項目:', arrList);
      for (let ii = 0; ii < arrList.length; ii++) {
        let loopTarget = arrList[ii];  //arr內的值
        let position = this.inCompleteList.indexOf(loopTarget);  //arr內值的位置

        if (position !== -1) {
          this.inCompleteList.splice(position, 1);
        } 
        // else if (position === -1) {
        //     this.inCompleteList.push(loopTarget);
        // }
      console.log(position);
      }

    let newInCompleteList = [];
    for (let jj = 0; jj < this.arr.length; jj++) {
      let currentTarget = this.arr[jj];
      let searchPosition = arrList.indexOf(currentTarget);

      if (searchPosition === -1) {
        newInCompleteList.push(currentTarget)
      }
    }
      this.inCompleteList = newInCompleteList;
      console.log('尚未完成的項目: ', this.inCompleteList);
    }
  },
  computed: {},
  methods: {
    buttonClick () {  //buttonClick: function ()
      if (this.message != '') {
      const addTodo = this.message;
      this.recordList = addTodo;
      this.arr.push(addTodo);  //將addTodo的值push到arr陣列
      this.message = '';
      // console.log(addTodo);
      this.inCompleteList.push(addTodo);
      this.isShow2();
      }
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
    },
    clickTest (value) {
      console.log('click item:', value);
      // this.checkItemComplete(value);
    },
    checkItemComplete (str) {
      let checkComplete = false;

      for (let kk = 0; kk < this.checkedList.length; kk++) {
        let search = this.checkedList.indexOf(str);

        if (search !== -1) {
          checkComplete = true;
        }
      }

      console.log('item?', checkComplete);

      return checkComplete;
    }
    
  },
  created() {
    
  },

}

</script>

<style lang="scss">  /*css*/
body {
  margin: 0px;
  > #app {
    text-align: center;
  }
}

h1 {
  margin: 0px;
}

/* #app {
  font-family: 'Press Start 2P', cursive;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: #FAD9E2;
} */

#button {
  width: 80px;
  height: 80px;
  margin-left: 8px;
  border-radius: 50%;
  background-color: #F7B8BC;
  border: 0px;
  outline:none;

}

#button1 {
  width: 60px;
  height: 20px;
  border: 0px;
  background-color: #F7B8BC;
}

#button2 {
  width: 90px;
  height: 40px;
  border: 0px;
  background-color: #F7B8BC;
  margin: auto;
}

#app li {
  list-style:none;
  margin-bottom: 10px;
}

.list {
  width: 200px;
  margin: auto;
  text-align: center;
}

.complete {
  width: 400px;
  margin: auto;
  margin-top: 30px;
  display:flex;
  flex-direction: row;
  justify-content: space-evenly;
} 

#button:hover{
  background-color: #F7E8B8;
}


</style>
