<script setup>
import { ref } from "vue";
import Input from "./ui/input/Input.vue";
import Button from "./ui/button/Button.vue";
import Textarea from "./ui/textarea/Textarea.vue";
import {
  Dialog,
  DialogContent,
  DialogHeader,
  DialogTitle,
} from "@/components/ui/dialog";
import DatePicker from "./DatePicker.vue";
import { Plus } from "lucide-vue-next";
import { defineProps, defineEmits } from "vue";
const props = defineProps({
  isOpen: Boolean,
  addTodo: Function,
});

const emit = defineEmits(["update:isOpen"]);
const todoTitle = ref("");
const todoDescription = ref("");
const todoPriority = ref("medium");
const todoDueDate = ref(null);

const resetForm = () => {
  todoTitle.value = "";
  todoDescription.value = "";
  todoPriority.value = "medium";
  todoDueDate.value = null;
};

const submitHandle = (e) => {
  e.preventDefault();
  if (todoTitle.value.trim()) {
    props.addTodo({
      title: todoTitle.value,
      description: todoDescription.value,
      priority: todoPriority.value,
      dueDate: todoDueDate.value
    });
    resetForm();
    emit("update:isOpen", false);
  }
};
</script>

<template>
  <Dialog v-model:open="props.isOpen">
    <DialogContent class="sm:max-w-md">
      <DialogHeader>
        <DialogTitle class="flex items-center gap-2">
          <div
            class="w-8 h-8 bg-gradient-primary rounded-lg flex items-center justify-center"
          >
            <Plus class="w-4 h-4 text-black" />
          </div>
          Add New Todo
        </DialogTitle>
      </DialogHeader>

      <form @submit="submitHandle" class="space-y-6">
        <div class="space-y-4">
          <div>
            <label class="text-sm font-medium mb-2 block"> Title * </label>
            <Input
            v-model="todoTitle"
            placeholder="Enter todo title..."
            class="w-full"
            autoFocus
          />
          </div>

          <div>
            <label class="text-sm font-medium mb-2 block"> Description </label>
            <Textarea v-model="todoDescription" placeholder="Type your message here." />
          </div>

          <div class="grid grid-cols-2 gap-4">
            <div>
              <label class="text-sm font-medium mb-2 block"> Priority </label>
              <select
                v-model="todoPriority"
                class="w-full px-3 py-2 border border-input rounded-md bg-background text-sm"
              >
                <option value="low">Low Priority</option>
                <option value="medium">Medium Priority</option>
                <option value="high">High Priority</option>
              </select>
            </div>

            <div>
              <label class="text-sm font-medium mb-2 block"> Due Date </label>
              <DatePicker v-model="todoDueDate" />
            </div>
          </div>
        </div>

        <div class="flex gap-3 pt-4">
          <Button
            type="submit"
            class="flex-1  rounded bg-red-300  hover:bg-red-400 transition-all"
          >
            <Plus class="w-4 h-4 mr-2" />
            Add Todo
          </Button>
          <button
            type="button"
            @click="emit('update:isOpen', false)"
            class="px-4 py-2 border border-input rounded-md"
          >
            Close
          </button>
        </div>
      </form>
    </DialogContent>
  </Dialog>
</template>
<style lang=""></style>
