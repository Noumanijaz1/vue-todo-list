<script setup>
import { computed } from "vue";
import TodoItem from "./TodoItem.vue";
const { todos, deleteTodo , toggleTodo , completed } = defineProps(["todos", "deleteTodo" , 'toggleTodo' , 'completed']);
const reverseTodos = computed(() => {
  return [...todos].reverse();
});
</script>
<template>
  <ul class="mt-4 space-y-1.5">
    <TodoItem
      v-for="todo in reverseTodos"
      :todo="todo"
      :completed="completed"
      :key="todo.id"
      @deleteTodo="deleteTodo"
      @toggleTodo="toggleTodo"
    />
  </ul>
</template>
<style scoped></style>
