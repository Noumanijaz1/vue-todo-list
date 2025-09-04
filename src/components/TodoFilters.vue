<script setup>
import Input from "./ui/input/Input.vue";
import {
  Select,
  SelectContent,
  SelectGroup,
  SelectItem,
  SelectLabel,
  SelectTrigger,
  SelectValue,
} from "@/components/ui/select";
</script>
<template>
  <div>
    <Input type="text" />
    <Select>
      <SelectTrigger class="w-[180px]">
        <SelectValue placeholder="Select a fruit" />
      </SelectTrigger>
      <SelectContent>
        <SelectGroup>
          <SelectItem value="all"> All </SelectItem>
          <SelectItem value="completed"> completed </SelectItem>
          <SelectItem value="pendinf"> pending </SelectItem>
        </SelectGroup>
      </SelectContent>
    </Select>
  </div>
</template>
<style lang=""></style>
