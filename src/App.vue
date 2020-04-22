<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-on:del-todo="deleteTodoItem" v-bind:todos="todos" />
  </div>
</template>

<script>
import Todos from './components/Todos';
import Header from './components/layout/Header';
import AddTodo from './components/AddTodo';

export default {
  name: 'App',
  components: { Todos, Header, AddTodo },
  data() {
    return {
      todos: [
        {
          id: 1,
          title: 'My Love',
          completed: true,
        },
        {
          id: 2,
          title: 'Mi A3',
          completed: false,
        },
        { id: 3, title: 'Mothers day', completed: false },
        {
          id: 4,
          title: 'FIA Formula One Race',
          completed: false,
        },
      ],
    };
  },
  methods: {
    deleteTodoItem(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
    addTodo(newTodo) {
      this.todos.push(newTodo);
    },
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
