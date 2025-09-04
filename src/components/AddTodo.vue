<script setup>
import { ref } from "vue";
const props = defineProps(["addTodo"]);
const newItem = ref("");
const todos = ref([]);

const submitHandle = (e) => {
  e.preventDefault();
  props.addTodo(newItem.value);
  newItem.value = "";
};
</script>

<template>
  <form v-on:submit="submitHandle">
    <div class="flex align-center justify-between gap-3">
      <input
        type="text"
        v-model="newItem"
        class="w-full px-4 py-3 border border-red-300 rounded focus:border-amber-200 focus:ring-gray-800"
      />
      <button class="bg-red-300 px-4 py-3 text-white rounded min-w-fit">
        Add Todo
      </button>
    </div>
  </form>
</template>
<style lang=""></style>
