<template>
  <div>
    <header>
      <h1>Vue TODO with Typescript</h1>
    </header>
    <TodoInput
      :item="todoText"
      @input="updateTodoText"
      @add="addTodoItem"
    ></TodoInput>
    <div>
      <ul>
        <TodoListItem></TodoListItem>
      </ul>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import TodoInput from '@/components/TodoInput.vue'
import TodoListItem from '@/components/TodoListItem.vue'

const STORAGE_KEY = 'vue-todo-ts-v1'
const storage = {
  fetch() {
    const todoItems = localStorage.getItem(STORAGE_KEY) || []
    const result = JSON.parse(todoItems)
    return result
  },
}
export default Vue.extend({
  name: 'App',
  components: {
    TodoInput,
    TodoListItem,
  },
  data() {
    return {
      todoText: '',
    }
  },
  methods: {
    updateTodoText(value: string) {
      this.todoText = value
    },
    addTodoItem() {
      const value = this.todoText
      localStorage.setItem(value, value)
      this.initTodoText()
    },
    initTodoText() {
      this.todoText = ''
    },
  },
})
</script>
