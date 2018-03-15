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
    <p>child tell me:{{ childWords }}</p>
    <!-- 大写A转换成-a -->
    <component-a msgfromfather='you' v-on:child-tell-me-something='listenToMyBoy'></component-a>
  </div>
</template>

<script>
//使用ES6特性引入 localstorage 储存脚本，命名为 Store
import Store from './store'
//引入 componentA.vue 组件，命名为 componentA
import ComponentA from './components/componentA'
//ES6语法，相当于
//new Vue({})
export default {
  // name: 'App',
  data: function(){
    return{
      title:"<span>?<span>todo list",
      items: Store.fetch(),//获取存在 store 里面的键值对
      // items:[],
      newItem:'',
      childWords:''
    }
  },
  components:{
    ComponentA
    //在#app元素内，注册组件
  	//Hello
  },
  watch:{
    items:{
      handler:function(items){
        Store.save(items)
      },
      deep:true
    }
  },
  //xiugai
  // events:{
  //   'child-tell-me-somthing':function(message){
  //     this.childWords = message;
  //   }
  // },
  methods:{
    toggleFinish: function (item){
      //逆反布尔值
      item.isFinished = !item.isFinished
    },
    addNew: function(){
      this.items.push({
        label:this.newItem,
        isFinished: false
      })
      // console.log(this.newItem);
      //清空在input输入的内容
      this.newItem=''
    },
    listenToMyBoy:function(message) {
      this.childWords = message;
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
