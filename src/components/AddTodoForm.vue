<script setup>
import { ref } from "vue";
import Input from "./ui/input/Input.vue";
import Button from "./ui/button/Button.vue";

const props = defineProps(["addTodo"]);
const newItem = ref("");

const submitHandle = (e) => {
  e.preventDefault();
  if (newItem.value.trim !== "") props.addTodo(newItem.value);
  newItem.value = "";
};
</script>

<template>
  <form v-on:submit="submitHandle">
    <div class="flex align-center justify-between gap-3">
      <Input
        type="text"
        v-model="newItem"
        class="w-full px-4 py-3 border border-red-300 rounded focus:border-amber-200 focus:ring-gray-800"
      />
      <Button class="bg-red-300 px-4 py-3 text-white rounded min-w-fit">
        Add Todo
      </Button>
    </div>
  </form>
</template>
<style lang=""></style>
