<script setup>
import Input from "./ui/input/Input.vue";
import Button from "./ui/button/Button.vue";
import {
  Select,
  SelectContent,
  SelectGroup,
  SelectItem,
  SelectTrigger,
  SelectValue,
} from "@/components/ui/select";
import Card from "./ui/card/Card.vue";
const props = defineProps(["isOpen"]);
const emit = defineEmits(["update:isOpen"]);

const openAddModalHandle = () => {
  emit("update:isOpen", !props.isOpen);
};
</script>
<template>
  <Card class="p-6 text-center shadow-card">
    <div class="flex items-center gap-4">
      <Input type="text" placeholder="Seach task" />
      <Select>
        <SelectTrigger class="w-[180px]">
          <SelectValue placeholder="Select One" />
        </SelectTrigger>
        <SelectContent>
          <SelectGroup class="">
            <SelectItem value="all"> All </SelectItem>
            <SelectItem value="Completed"> Completed </SelectItem>
            <SelectItem value="pending"> Pending </SelectItem>
          </SelectGroup>
        </SelectContent>
      </Select>
      <Select>
        <SelectTrigger class="w-[180px]">
          <SelectValue placeholder="Select One" />
        </SelectTrigger>
        <SelectContent>
          <SelectGroup class="">
            <SelectItem value="all"> All </SelectItem>
            <SelectItem value="high"> High </SelectItem>
            <SelectItem value="medium"> Medium</SelectItem>
            <SelectItem value="low"> Low</SelectItem>
          </SelectGroup>
        </SelectContent>
      </Select>
      <Button
        class="bg-red-300 px-4 py-3 text-white rounded min-w-fit hover:bg-red-400"
        @click="openAddModalHandle"
      >
        Add Todo
      </Button>
    </div>
  </Card>
</template>
<style lang=""></style>
