<script setup>
import { Trash } from "lucide-vue-next";

const { todo } = defineProps(["todo"]);
const emit = defineEmits(["deleteTodo", "toggleTodo"]);

const deleteTodo = (id) => {
  emit("deleteTodo", id);
};

const toggleTodo = (id) => {
  emit("toggleTodo", id);
};
</script>

<template>
  <li class="flex items-center justify-between">
    <div class="flex items-center gap-2">
      <!-- bind checkbox checked to todo.completed -->
      <input
        class="w-5 h-5 border border-gray-300 rounded cursor-pointer"
        type="checkbox"
        :checked="todo.completed"
        @change="toggleTodo(todo.id)"
      />

      <!-- add conditional class for line-through -->
      <span
        :class="[
          'text-2xl font-medium',
          todo.completed ? 'line-through text-gray-400' : 'text-black/80'
        ]"
      >
        {{ todo.label }}
      </span>
    </div>

    <Trash
      @click="deleteTodo(todo.id)"
      class="cursor-pointer text-red-500 hover:text-red-700"
    />
  </li>
</template>

