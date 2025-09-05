<script setup>
import { computed, watch } from "vue";
import TodoItem from "./TodoItem.vue";
const props = defineProps([
  "todos",
  "deleteTodo",
  "toggleTodo",
  "completed",
]);


const reverseTodos = computed(() => {
  if (!props.todos || !Array.isArray(props.todos)) {
    console.error('todos is not an array:', props.todos);
    return [];
  }
  return [...props.todos].reverse();
});
</script>
<template>
  <ul class="mt-4 space-y-1.5">
    <div v-if="!props.todos || props.todos.length === 0" class="text-center py-4 text-gray-500">
      No todos yet. Add one above!
    </div>
    <template v-else>
      <TodoItem
        v-for="todo in reverseTodos"
        :todo="todo"
        :completed="props.completed"
        :key="todo.id"
        @deleteTodo="props.deleteTodo"
        @toggleTodo="props.toggleTodo"
      />
    </template>
  </ul>
</template>
<style scoped></style>
