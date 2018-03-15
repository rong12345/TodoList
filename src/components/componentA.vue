
<template>
  <div class="hello">
    <h1>{{ message }}</h1>
    <h1>{{ msgfromfather }}</h1>
    <button v-on:click="onClickMe">open mouse</button>
  </div>

</template>

<script>
export default {
  // name: 'hello',
  data () {
    return {
      message: 'from componenta!'
    }
  },
  props:['msgfromfather'],
  methods:{
    onClickMe:function () {
      console.log(this.msgfromfather);
      //vue废弃$dispatch $broadcast
      // this.$dispatch('child-tell-me-something',this.message)
      this.$emit('child-tell-me-something',this.message)
    }
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
