<template>
  <div>
    <h2>Todo application</h2>
    <router-link to="/">Home</router-link>
    <AddTodo @add-todo="addTodo" />
    <select v-vodel="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">In progress</option>
    </select>
    <hr />
    <Loader v-if="loading" />
    <TodoList
      v-else-if="filteredTodos.length"
      v-bind:todos="filteredTodos"
      @remove-todo="removeTodo"
    />
    <p v-else>All done!</p>
  </div>
</template>

<script>
import TodoList from "@/components/TodoList";
import AddTodo from "@/components/AddTodo";
import Loader from "@/components/Loader";

export default {
  name: "app",
  data() {
    return {
      todos: [],
      loading: true,
      filter: "all"
    };
  },
  components: {
    TodoList,
    AddTodo,
    Loader
  },
  mounted() {
    fetch("https://jsonplaceholder.typicode.com/todos?_limit=3")
      .then(response => response.json())
      .then(json => {
        setTimeout(() => {
          this.todos = json;
          this.loading = false;
        }, 300);
      });
  },
  computed: {
    filteredTodos() {
      if (this.filter === "all") {
        return this.todos;
      } else if (this.filter === "completed") {
        return this.todos.filter(t => t.completed);
      } else {
        return this.todos.filter(t => !t.completed);
      }
    }
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id);
    },
    addTodo(todo) {
      this.todos.push(todo);
    }
  }
};
</script>
