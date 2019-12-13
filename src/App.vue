<template>
  <div id="app">
    <h1>Welcome to my todo application</h1>
    <hr />
    <TodoList :todos="todos" @remove-todo="removeTodo" />
  </div>
</template>

<script>
import TodoList from "@/components/TodoList";

export default {
  name: "app",
  data() {
    return {
      todos: [
        { id: 1, title: "Buy some bread", completed: false },
        { id: 2, title: "Buy some milk", completed: false },
        { id: 3, title: "Tidy up!", completed: false }
      ]
    };
  },
  components: {
    TodoList
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id);
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
