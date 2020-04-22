<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-on:del-todo="deleteTodoItem" v-bind:todos="todos" />
  </div>
</template>

<script>
import Todos from '../components/Todos';
import AddTodo from '../components/AddTodo';

import axios from 'axios';

export default {
  name: 'Home',
  components: { Todos, AddTodo },
  data() {
    return {
      todos: [],
    };
  },
  methods: {
    deleteTodoItem(id) {
      // Send to the server and delete upstream
      const url = `https://jsonplaceholder.typicode.com/todos/${id}`;
      axios
        .delete(url)
        .then((response) => {
          this.todos = this.todos.filter((todo) => todo.id !== id);
          return response;
        })
        .catch((err) => console.log(err));
    },
    addTodo(newTodo) {
      const { id, title, completed } = newTodo;
      console.log(`Creating todo id ${id}`);
      // Send this to todo to the server
      const url = 'https://jsonplaceholder.typicode.com/todos';
      axios
        .post(url, {
          title,
          completed,
        })
        .then((response) => this.todos.push(response.data))
        .catch((err) => console.log(err));
    },
  },
  created() {
    const url = 'https://jsonplaceholder.typicode.com/todos?_limit=4';
    axios
      .get(url)
      .then((response) => (this.todos = response.data))
      .catch((err) => console.log(err));
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}
.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}
.btn:hover {
  background: #666;
}
</style>
