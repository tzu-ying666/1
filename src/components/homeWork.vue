<template>
  <div id = 'app2'>
    <!-- {{ arr }} -->
    <ul>
      <li v-for="(item, index) in arr" :key="item + '_' + index">
        <p v-for="post in item" :key="post">{{ post }}</p>  <!-- item等於上面的item -->
      </li>
    </ul>
  </div>
</template>
<script>
        // <input type="text" v-bind:value="firstnum" name=item />

export default {
  data () {
    return {
      arr: [],
      firstarr: [],
      lastarr: [],
      firstnum: '',
      lastnum: '',
    }
  },

  watch: {

  },

  computed: {

  },

  methods: {

  },
  created() {
    for (let firstnum = 1; firstnum <= 9; firstnum++) {
      // this.firstarr.push(firstnum);
      let numArray = [];
      for (let lastnum = 1; lastnum <= 9; lastnum++) {

        let ans = firstnum * lastnum;
        numArray.push(firstnum + ' x ' + lastnum + ' = ' + ans);
      }
      this.arr.push(numArray);
    }    
  },

}

</script>
<style>
  #app2 {
  font-family: 'Press Start 2P', cursive;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
  }

  #app2 li {
    list-style:none;
    width: 100px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    background-color: #F7B8BC;
    border-radius: 10px;    
    margin: 20px;
  }

  ul{
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    
  }


  
</style>