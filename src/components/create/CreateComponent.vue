<template>
  <div class="list__action-create">
    <input
      class="list__action-create-input"
      type="text"
      v-model="text"
      @keyup.enter="createNote"
    />
    <button class="list__action-create-button" @click="createNote">
      <div class="list__action-create-button-hover">
        <i class="list__action-create-button-icon fa-solid fa-plus"></i>
      </div>
    </button>
  </div>
</template>
<script setup>
import { defineEmits, ref } from "vue";
const text = ref("");
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
