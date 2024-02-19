<template>
  <div>
    <label for="todo-input"></label>
    <input type="text" id="todo-input" :value="item" />
    <button @click="addTodo" type="button">add</button>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  props: ["item"],
  methods: {
    addTodo() {
      console.log("todo");
    },
  },
});
</script>
