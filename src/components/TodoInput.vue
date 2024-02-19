<template>
  <div>
    <label for="todo-input">오늘 할 일 : </label>
    <input type="text" id="todo-input" :value="item" @input="handleInput" />
    <button @click="addTodo" type="button">add</button>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  // props: ["item"],
  props: {
    item: {
      type: String,
      required: true,
    },
  },
  methods: {
    addTodo() {
      this.$emit("add");
    },
    handleInput(event: InputEvent) {
      console.warn("event:::", event);
      // InputEvent에 접근하는 방법
      // 1. InputEvent 타입의 value 값에 직접 접근하게 되면 null 체크를 해야함
      // 2. event.target as HTMLInputElement : event.target을 HTMLInputElement 타입으로 캐스팅
      const eventTarget = event.target as HTMLInputElement;
      this.$emit("input", eventTarget.value);
    },
  },
});
</script>
