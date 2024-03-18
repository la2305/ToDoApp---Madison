<template>
  <div class="list__container-item" v-for="item in todos" :key="item.id">
    <div
      class="list__container-item-text"
      :class="{ 'list__container-item-text-completed': item.completed }"
    >
      {{ item.text }}
    </div>
    <div class="list__container-item-check" @click="toggleItem(item.id)">
      <i class="list__container-item-check-icon fa-solid fa-check"></i>
    </div>
    <div class="list__container-item-trash" @click="removeItem(item.id)">
      <i class="list__container-item-trash-icon fa-solid fa-trash"></i>
    </div>
  </div>
</template>
<script setup>
import { defineEmits, defineProps } from "vue";
const emit = defineEmits(["update:removeItem"], ["update:toggleItem"]);

defineProps({
  todos: {
    type: Array,
    required: true,
  },
});
const removeItem = (itemId) => {
  emit("update:removeItem", itemId);
};
const toggleItem = (itemId) => {
  emit("update:toggleItem", itemId);
};
</script>
