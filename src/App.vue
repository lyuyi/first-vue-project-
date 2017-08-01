<template>
  <div id="app">
      <h1>{{title1}}</h1>
      <h1 v-text="title"></h1>
      <h2 v-html="msg"></h2>
      <input v-model="newItem" @keyup.enter="addNew">
      <ol>
        <li v-for="item in items" v-bind:class="[classA, {finished: item.isFinished}]" v-on:click="toggleFinish(item)">
          {{item.label}}
        </li>
      </ol>
      <p>child tells me: {{ childWords }}</p>
      <component msgfromfather='you good!' v-on:child-tell-me-something="listenToMyBoy"></component>
      <!-- child-tell-me-sth是父组件绑定的自定义事件,listentomyboy是父组件绑定的事件发生时触发的函数 -->
  </div>
</template>

<script>
import Store from './store.js'
import Component from './components/component'
export default {
  data: function () {
    return {
      title1: 'this is a todo list',
      title: 'Welcome !',
      msg: '<span>Simply todolist - vuejs</span>',
      items: Store.fetch(),
      newItem: '',
      classA: 'isli',
      childWords: ''
    }
  },
  components: { Component },
  watch: {//监察某个值
    items: {
      handler: function (items) {
        Store.save(items)
      },
      deep: true  //如果不写这个的话，items如果有key更改了，也不会被认为是更改了。
    }
  },
  methods: {
    toggleFinish: function (item) {
      item.isFinished = !item.isFinished
    },
    addNew: function () {
      this.items.push({
        label: this.newItem,
        isFinished: false
      })
      this.newItem = ''
    },
    listenToMyBoy: function (msg){
      console.log(msg);
      this.childWords = msg;
    }
  }
}
</script>

<style>
html {
  height: 100%;
}
body {
  font-family: Helvetica, sans-serif;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%; 
}
.isli{
  cursor: pointer;
}
.finished{
  text-decoration: line-through;
}
</style>
