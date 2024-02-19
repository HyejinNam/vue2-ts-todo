<template>
  <div>
    <h1>Vue TODO with Typescript</h1>
    <TodoInput
      :item="todoText"
      @input="updateTodoText"
      @add="addTodoItem"
    ></TodoInput>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import TodoInput from "@/components/TodoInput.vue";

export default Vue.extend({
  name: "App",
  components: {
    TodoInput,
  },
  data() {
    return {
      todoText: "",
    };
  },
  methods: {
    updateTodoText(value: string) {
      this.todoText = value;
    },
    addTodoItem() {
      const value = this.todoText;
      localStorage.setItem(value, value);
      this.initTodoText();
    },
    initTodoText() {
      this.todoText = "";
    },
  },
});
</script>
