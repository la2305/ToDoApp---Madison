<template>
  <div
    class="list__container-item"
    :class="{ 'list__container-item-out': isRemoveActive[item.id] }"
    v-for="item in todos"
    :key="item.id"
  >
    <div
      class="list__container-item-text"
      :class="{ 'list__container-item-text-completed': item.completed }"
    >
      {{ item.text }}
    </div>
    <button class="list__container-item-check" @click="toggleItem(item.id)">
      <i class="list__container-item-check-icon fa-solid fa-check"></i>
    </button>
    <button class="list__container-item-trash" @click="removeItem(item.id)">
      <i class="list__container-item-trash-icon fa-solid fa-trash"></i>
    </button>
  </div>
</template>
<script setup>
import { defineEmits, defineProps, ref } from "vue";

const isRemoveActive = ref([]);
const emit = defineEmits(["update:removeItem"], ["update:toggleItem"]);
defineProps({
  todos: {
    type: Array,
    required: true,
  },
});

// Send event remove item
const removeItem = (itemId) => {
  isRemoveActive.value[itemId] = true;
  setTimeout(() => {
    emit("update:removeItem", itemId);
  }, 500);
};

// Send event toggle complete item
/** @function void
 * @name saveTodosToLocalStorage
 * @param none*/
const toggleItem = (itemId) => {
  emit("update:toggleItem", itemId);
};
</script>
<style scoped src="./ItemComponent.css"></style>
