<template>
  <div class="list__action-create">
    <input
      class="list__action-create-input"
      type="text"
      v-model="text"
      @keyup.enter="createNote"
    />
    <button
      class="list__action-create-button"
      :class="{ active: isActive }"
      @mousedown="isActive = true"
      @mouseup="isActive = false"
      @click="createNote"
    >
      <div class="list__action-create-button-hover">
        <i class="list__action-create-button-icon fa-solid fa-plus"></i>
      </div>
    </button>
  </div>
</template>
<script setup>
import { defineEmits, ref } from "vue";
const text = ref("");
const isActive = ref(null);
const emit = defineEmits(["update:createNote"]);

const createNote = () => {
  if (!text.value) {
    return;
  } else {
    emit("update:createNote", text.value);
    text.value = "";
  }
};
</script>
<style scoped src="./CreateComponent.css"></style>
