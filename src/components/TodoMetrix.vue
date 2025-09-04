<script setup>
import { Plus, CalendarCheck2, CalendarX, CalendarDays } from "lucide-vue-next";
const { todos } = defineProps(["todos"]);
</script>
<template>
  <div class="grid grid-cols-3 gap-4 mb-4">
    <div
      class="bg-white border rounded border-red-300 shadow-md p-6 flex items-center justify-between"
    >
      <div>
        <p class="text-sm text-muted-foreground">Total Tasks</p>
        <p class="text-3xl font-bold">{{ todos.length }}</p>
      </div>
      <div
        class="w-12 h-12 bg-red-300 rounded-lg flex items-center justify-center"
      >
        <Plus class="w-6 h-6 text-white" />
      </div>
    </div>
    <div
      class="bg-white border rounded border-red-300 shadow-md p-6 flex items-center justify-between"
    >
      <div>
        <p class="text-sm text-muted-foreground">Completed Todos</p>
        <p class="text-3xl font-bold">
          {{ todos.filter((todo) => todo.completed).length }}
        </p>
      </div>
      <div
        class="w-12 h-12 bg-green-300 rounded-lg flex items-center justify-center"
      >
        <CalendarCheck2 class="w-6 h-6 text-white" />
      </div>
    </div>
    <div
      class="bg-white border rounded border-red-300 shadow-md p-6 flex items-center justify-between"
    >
      <div>
        <p class="text-sm text-muted-foreground">Pending Todos</p>
        <p class="text-3xl font-bold">
          {{ todos.filter((todo) => !todo.completed).length }}
        </p>
      </div>
      <div
        class="w-12 h-12 bg-yellow-300 rounded-lg flex items-center justify-center"
      >
        <CalendarDays class="w-6 h-6 text-white" />
      </div>
    </div>
  </div>
</template>
<style scoped></style>
