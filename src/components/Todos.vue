<script setup>
import { ref } from "vue";
// component import
import AddTodo from "./AddTodo.vue";
import TodoList from "./TodoList.vue";

const todos = ref([]);

// generate random id function
const randomId = () => {
  return Date.now().toString(36) + Math.random().toString(36).substr(2, 9);
};

// add todo function
const addTodo = (newTodo) => {
  todos.value.push({
    id: randomId(),
    label: newTodo,
    completed: false, 
  });
};

// delete todo function
const deleteTodo = (id) => {
  todos.value = todos.value.filter((todo) => todo.id !== id);
};

// toggle todo function
const toggleTodo = (id) => {
  todos.value = todos.value.map((todo) =>
    todo.id === id ? { ...todo, completed: !todo.completed } : todo
  );
};
</script>

<template>
  <div class="max-w-xl mx-auto py-12">
    <h1 class="text-3xl font-bold mb-4 text-red-300">Todo List</h1>
    <AddTodo :addTodo="addTodo" />
    <TodoList
      :todos="todos"
      :deleteTodo="deleteTodo"
      :toggleTodo="toggleTodo"
    />
  </div>
</template>
