<template>
  <div id="app">
    <h1 v-text="title"></h1>
    <h1 v-html="title"></h1>
    <input v-model="newItem">
    <button type="button" name="button" @click="addNew">add</button>
    <ul>
      <li v-for="item in items" v-bind:class="{finished:item.isFinished}" v-on:click="toggleFinish(item)">
        {{item.label}}
      </li>
    </ul>
  </div>
</template>

<script>
import Store from './store'

export default {
  // name: 'App',
  data: function(){
    return{
      title:"<span>?<span>todo list",
      // items: Store.fetch(),
      items:[],
      newItem:[]
    }
  },
  // watch:{
  //   items:{
  //     handler:function(items){
  //       Store.save()
  //     },
  //     deep:true
  //   }
  // },
  methods:{
    toggleFinish: function (item){
      item.isFinished = !item.isFinished
    },
    addNew: function(){
      this.items.push({
        label:this.newItem,
        isFinished: false
      })
      // console.log(this.newItem);
      this.newItem=''
    }
  }
}
</script>

<style>
.finished {
  text-decoration: underline;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
