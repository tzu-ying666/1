<template>
  <div id = 'app2'>
    {{ caculator }}
  </div>
</template>
<script>

export default {
  data () {
    return {}
  },

  watch: {

  },

  computed: {

  },

  methods: {
    caculator () {
      for (let ii = 1; ii <= 9; ii++) {
        for (let jj = 1; jj <= 9; jj++) {
            console.log('ii' + 'x' + 'jj' + '='  );
        }
      }
    },
  },
  crested() {},

}

</script>
<style>

</style>