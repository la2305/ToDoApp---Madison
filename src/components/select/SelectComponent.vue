<template>
  <div class="list__action-select">
    <select
      name="format"
      class="list__action-select-item"
      v-model="currentFilter"
      @change="filterTodosData"
    >
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="uncompleted">Uncompleted</option>
    </select>
  </div>
</template>
<script setup>
import { defineEmits, ref } from "vue";

const currentFilter = ref("all");

const emit = defineEmits(["update:filterTodosData"]);

// Send event filter data
const filterTodosData = () => {
  emit("update:filterTodosData", currentFilter.value);
};
</script>
<style scoped src="./SelectComponent.css"></style>
