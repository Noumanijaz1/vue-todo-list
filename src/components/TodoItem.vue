<script setup>
import { Trash2, Calendar, Flag } from "lucide-vue-next";
import { DateFormatter, getLocalTimeZone } from "@internationalized/date";
import { Card } from "@/components/ui/card";
import { onMounted } from 'vue';

const props = defineProps({
  todo: {
    type: Object,
    required: true,
  },
  completed: {
    type: Boolean,
    default: false,
  },
});
const emit = defineEmits(["deleteTodo", "toggleTodo"]);



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

// Format due date handling different formats from localStorage
const formatDueDate = (dueDate) => {
  if (!dueDate) return '';
  
  try {
    // If it's already a date object with toDate method
    if (typeof dueDate.toDate === 'function') {
      return df.format(dueDate.toDate(getLocalTimeZone()));
    }
    
    // If it's a string (from localStorage)
    if (typeof dueDate === 'string') {
      return new Date(dueDate).toLocaleDateString();
    }
    
    // If it's a Date object
    if (dueDate instanceof Date) {
      return dueDate.toLocaleDateString();
    }
    
    return String(dueDate);
  } catch (error) {
    console.error('Error formatting date:', error, dueDate);
    return 'Invalid date';
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
            :checked="props.todo.completed"
            @change="emit('toggleTodo', props.todo.id)"
          />

          <!-- add conditional class for line-through -->
          <div class="flex flex-col gap-2">
            <h3
              :class="[
                'text-lg font-medium leading-tight',
                props.todo.completed
                  ? 'line-through text-muted-foreground'
                  : 'text-black/80',
              ]"
            >
              {{ props.todo.label }}
            </h3>
            <!-- Description section -->
            <div
              v-if="props.todo.description"
              class="text-left text-gray-600 text-sm"
            >
              {{ props.todo.description }}
            </div>
            <!-- Priority and Due Date section -->
            <div
              class="flex items-center justify-between text-xs text-gray-500"
            >
              <div v-if="props.todo.priority" class="flex items-center gap-1">
                <Flag :class="[getPriorityColor(props.todo.priority), 'w-3 h-3']" />
                <span class="capitalize">{{ props.todo.priority }} Priority</span>
              </div>

              <div v-if="props.todo.dueDate" class="flex items-center gap-1">
                <Calendar class="w-3 h-3" />
                <span>{{ formatDueDate(props.todo.dueDate) }}</span>
              </div>
            </div>
          </div>
        </div>
        <Trash2
          :stroke-width="1"
          @click="emit('deleteTodo', props.todo.id)"
          class="cursor-pointer text-red-500 hover:text-red-700"
        />
      </div>
    </Card>
  </li>
</template>
