<template>
  <section class="list">
    <h1 class="list__header">To-Do List</h1>
    <div class="list__action">
      <create-component @createNote="addItem"></create-component>
      <select-component @update:filterTodosData="selectData"></select-component>
    </div>
    <div class="list__container">
      <list-component
        :todos="filterTodosData"
        @update:removeItem="removeItem"
        @update:toggleItem="toggleItem"
      ></list-component>
    </div>
  </section>
</template>

<script setup>
import { computed, onMounted, reactive, ref } from "vue";
import CreateComponent from "../create/CreateComponent.vue";
import ListComponent from "../list/ListComponent.vue";
import SelectComponent from "../select/SelectComponent.vue";

const todos = reactive([]);
const currentFilter = ref("all");

// Get data from localStorage
onMounted(() => {
  const storageTodos = JSON.parse(localStorage.getItem("todos"));
  if (storageTodos) {
    storageTodos.forEach((item) => {
      todos.push(item);
    });
  }
});

/** @function void
 * @name addItem
 * @param {string} text*/
const addItem = (text) => {
  if (text.length > 0) {
    const newItem = {
      text: text,
      completed: false,
      id: Math.random(),
    };
    todos.push(newItem);
    saveTodosToLocalStorage();
  }
};

/** @function void
 * @name removeItem
 * @param {string} string*/
const removeItem = (itemId) => {
  const index = todos.findIndex((item) => item.id === itemId);
  if (index > -1) {
    todos.splice(index, 1);
  }
  saveTodosToLocalStorage();
};

/** @function void
 * @name toggleCompletedItem
 * @param {string} string*/
const toggleItem = (itemId) => {
  todos.forEach((item) => {
    if (item.id === itemId) {
      item.completed = !item.completed;
    }
  });
  saveTodosToLocalStorage();
};

/** @function void
 * @name selectData
 * @param {string} string*/
const selectData = (select) => {
  currentFilter.value = select;
};

/** @function Array
 * @name filterTodosData
 * @param none*/
const filterTodosData = computed(() => {
  if (currentFilter.value === "completed") {
    return todos.filter((item) => item.completed == true);
  } else if (currentFilter.value === "uncompleted") {
    return todos.filter((item) => item.completed == false);
  } else {
    return todos;
  }
});

// save data to localStorage
const saveTodosToLocalStorage = () => {
  localStorage.setItem("todos", JSON.stringify(todos));
};
</script>

<style scoped src="./ToDoList.css"></style>
