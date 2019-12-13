<template>
  <div>
    <ul>
      <TodoItem v-for="(todo, i) in todos" v-bind:key="i" v-bind:todo="todo" />
    </ul>
  </div>
</template>

<script>
import TodoItem from "@/components/TodoItem";
export default {
  props: ["todos"],
  components: {
    TodoItem
  }
};
</script>

<style lang="scss" scoped>
</style>