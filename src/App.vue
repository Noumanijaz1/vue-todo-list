<script setup>
import TodosList from "./components/Todos.vue";
import Header from "./components/Header.vue";
import TodoFilters from "./components/TodoFilters.vue";
</script>

<template>
  <div class="py-12 max-w-3xl mx-auto">
    <Header />
    <TodosList />
  </div>
</template>

<style scoped></style>
