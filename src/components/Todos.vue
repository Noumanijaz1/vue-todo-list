<script setup>
import { ref, watch, onMounted } from "vue";
// component import
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
  const saved = localStorage.getItem("todos");
  if (saved) {
    todos.value = JSON.parse(saved);
  }
});

// Watch todos and save them whenever they change
watch(
  todos,
  (newTodos) => {
    localStorage.setItem("todos", JSON.stringify(newTodos));
  },
  { deep: true } // important because todos is an array of objects
);

// add todo function
const addTodo = (todoData) => {
  todos.value.push({
    id: randomId(),
    label: todoData.title,
    description: todoData.description || '',
    priority: todoData.priority || 'medium',
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
    <TodoFilters :isOpen="isOpenAddTodo" @update:isOpen="isOpenAddTodo = $event" />
    <TodoList
      :todos="todos"
      :deleteTodo="deleteTodo"
      :toggleTodo="toggleTodo"
    />
  </div>
</template>
