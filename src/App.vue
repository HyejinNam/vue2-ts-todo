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
        <TodoListItem
          v-for="(todoItem, index) in todoItems"
          :key="index"
          :todoItem="todoItem"
        ></TodoListItem>
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
  save(todoItems: any[]) {
    const parsed = JSON.stringify(todoItems)
    localStorage.setItem(STORAGE_KEY, parsed)
  },
  fetch() {
    const todoItems = localStorage.getItem(STORAGE_KEY) || '[]'
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
      todoItems: [] as any[],
    }
  },
  methods: {
    updateTodoText(value: string) {
      this.todoText = value
    },
    addTodoItem() {
      // 1. input 값에서 value값 가져오기 (TodoInput.vue에서 가져옴)
      const value = this.todoText
      this.todoItems.push(value)
      storage.save(this.todoItems)
      this.initTodoText()
    },
    initTodoText() {
      this.todoText = ''
    },
    fetchTodoItems() {
      this.todoItems = storage.fetch()
    },
  },
  created() {
    this.fetchTodoItems()
  },
})
</script>
