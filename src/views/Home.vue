<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos='todos' v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>

import Todos from '../components/Todos.vue'
import AddTodo from '../components/AddTodo.vue';
import axios from 'axios';

export default {
  name: 'Home',
  components: {
    // Componete
    Todos,
    AddTodo
  },
  data() {
    return {
      // dados apresentados no Todos componente
      todos: []
    }
  },
  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id)
    },
    addTodo(newTodo){
      const {title, completed } = newTodo;
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,
        completed
      })
        .then(response => this.todos = [...this.todos, response.data])
        .catch()
    },
  },
  created(){
      axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')  
        .then(response => this.todos = response.data)
        .catch()
    }
}
</script>

<style>
  * {box-sizing: border-box; margin: 0; padding: 0}
  body{font-family: Arial, Helvetica, sans-serif; line-height: 1.4}
  .btn {
    display:inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer
  }
  .btn:hover {
    background: #666
  }
</style>
