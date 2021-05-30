<template>
  <div>
    <h1>Selamat datang </h1>
    <ul>
      <!-- <li v-for="item in todos">{{ item.Decs }}</li> -->
      <li v-for="(item) in todos" :key="item.Id">{{item.Id}} - {{item.Decs}}<button @click="dlt(item.Decs)">Delete</button> </li>
    </ul>
    <input v-model="myText"/>
    <button @click="tambah">Add</button>
  </div>
</template>

<script>
import axios from 'axios'
export default{
  data: function () {
    return {
      todos: [],
      myText: ''
    }
  },

  created: function() {
    axios.get('http://localhost:3000/todo')
      .then(tables=>{
        this.todos = tables.data
      })
  },

  methods: {
    tambah: (function () {
      // this.todos.push({ Decs:this.myText })
      const inpI = {Decs :this.myText}
      axios.post('http://localhost:3000/todo',inpI)
      this.todos.push(inpI)
      this.myText=""
    }),
  }
}
</script>
