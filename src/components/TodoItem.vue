<script setup>
import { Trash2, Calendar, Flag } from "lucide-vue-next";
import { DateFormatter, getLocalTimeZone } from "@internationalized/date";
import { Card } from "@/components/ui/card";

const { todo } = defineProps(["todo"]);
const emit = defineEmits(["deleteTodo", "toggleTodo"]);

const deleteTodo = (id) => {
  emit("deleteTodo", id);
};

const toggleTodo = (id) => {
  emit("toggleTodo", id);
};

const df = new DateFormatter("en-US", {
  dateStyle: "medium",
});

const getPriorityColor = (priority) => {
  switch (priority) {
    case "high":
      return "text-red-500";
    case "medium":
      return "text-yellow-500";
    case "low":
      return "text-green-500";
    default:
      return "text-gray-500";
  }
};
</script>

<template>
  <li>
    <Card
      class="p-6 shadow-card hover:shadow-hover transition-all border rounded"
    >
      <div class="flex items-center justify-between">
        <div class="flex gap-4">
          <!-- bind checkbox checked to todo.completed -->
          <input
            class="w-4 h-4 mt-1 border border-gray-300 rounded cursor-pointer"
            type="checkbox"
            :checked="todo.completed"
            @change="toggleTodo(todo.id)"
          />

          <!-- add conditional class for line-through -->
          <div class="flex flex-col gap-2">
            <h3
              :class="[
                'text-lg font-medium leading-tight',
                todo.completed
                  ? 'line-through text-muted-foreground'
                  : 'text-black/80',
              ]"
            >
              {{ todo.label }}
            </h3>
            <!-- Description section -->
            <div
              v-if="todo.description"
              class="text-left text-gray-600 text-sm"
            >
              {{ todo.description }}
            </div>
            <!-- Priority and Due Date section -->
            <div
              class="flex items-center justify-between text-xs text-gray-500"
            >
              <div v-if="todo.priority" class="flex items-center gap-1">
                <Flag :class="[getPriorityColor(todo.priority), 'w-3 h-3']" />
                <span class="capitalize">{{ todo.priority }} Priority</span>
              </div>

              <div v-if="todo.dueDate" class="flex items-center gap-1">
                <Calendar class="w-3 h-3" />
                <span>{{
                  todo.dueDate
                    ? df.format(todo.dueDate.toDate(getLocalTimeZone()))
                    : ""
                }}</span>
              </div>
            </div>
          </div>
        </div>
        <Trash2
          :stroke-width="1"
          @click="deleteTodo(todo.id)"
          class="cursor-pointer text-red-500 hover:text-red-700"
        />
      </div>
    </Card>
  </li>
</template>
