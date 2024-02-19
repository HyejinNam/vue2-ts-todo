<template>
  <div>
    <h1>Vue TODO with Typescript</h1>
    <TodoInput :item="todoText"></TodoInput>
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
});
</script>
