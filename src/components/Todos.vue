<script setup>
import { ref, watch, onMounted } from "vue";

import AddTodo from "./AddTodoForm.vue";
import TodoList from "./TodoList.vue";
import TodoMetrix from "./TodoMetrix.vue";
import TodoFilters from "./TodoFilters.vue";

const todos = ref([]);
const isOpenAddTodo = ref(false);

// generate random id function
const randomId = () => {
  return Date.now().toString(36) + Math.random().toString(36).substr(2, 9);
};

// Load todos from localStorage when app starts
onMounted(() => {
  const savedTodos = localStorage.getItem("todos");
  console.log("LOCAL STORAGE TODOS", savedTodos);
  todos.value = JSON.parse(savedTodos);
});

// Watch todos and save them whenever they change
watch(
  todos,
  (newTodos) => {
    try {
      localStorage.setItem("todos", JSON.stringify(newTodos));
    } catch (error) {
      console.error("Error saving todos to localStorage:", error);
    }
  },
  { deep: true } // important because todos is an array of objects
);

// add todo function
const addTodo = (todoData) => {
  todos.value.push({
    id: randomId(),
    label: todoData.title,
    description: todoData.description || "",
    priority: todoData.priority || "medium",
    dueDate: todoData.dueDate || null,
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
  <div class="py-12">
    <TodoMetrix :todos="todos" />
    <AddTodo :addTodo="addTodo" v-model:isOpen="isOpenAddTodo" />
    <TodoFilters
      :isOpen="isOpenAddTodo"
      @update:isOpen="isOpenAddTodo = $event"
    />
    <TodoList
      :todos="todos"
      :deleteTodo="deleteTodo"
      :toggleTodo="toggleTodo"
      :completed="false"
    />
  </div>
</template>
