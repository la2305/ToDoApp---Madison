<template>
  <div class="list__container-list">
    <item-component
      :todos="todos"
      @update:removeItem="removeItem"
      @update:toggleItem="toggleItem"
    ></item-component>
  </div>
</template>
<script setup>
import { defineEmits, defineProps } from "vue";
import ItemComponent from "../item/ItemComponent.vue";

const emit = defineEmits(
  ["update:modelValue", "update:removeItem"],
  ["update:toggleItem"]
);
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
