<template>
  <div>
    <header>
      <h1>Vue with Typescript</h1>
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
          :index='index'
          :todoItem="todoItem"
          @remove='removeTodoItem(index)'
          @toggle='toggleTodoItemComplete(todoItem, index)'
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
  save(todoItems: Todo[]) {
    const parsed = JSON.stringify(todoItems)
    localStorage.setItem(STORAGE_KEY, parsed)
  },
  fetch(): Todo[] {
    const todoItems = localStorage.getItem(STORAGE_KEY) || '[]'
    const result = JSON.parse(todoItems)
    return result
  },
}

export interface Todo {
  title: string,
  done: boolean,
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
      todoItems: [] as Todo[],
    }
  },
  methods: {
    updateTodoText(value: string) {
      this.todoText = value
    },
    addTodoItem() {
      // 1. input 값에서 value값 가져오기 (TodoInput.vue에서 가져옴)
      const value = this.todoText
      const todo: Todo = {
        title: value,
        done: false
      }
      this.todoItems.push(todo)
      storage.save(this.todoItems)
      this.initTodoText()
    },
    initTodoText() {
      this.todoText = ''
    },
    fetchTodoItems() {
      this.todoItems = storage.fetch().sort((a, b) => {
        if (a.title < b.title) {
          return -1
        }
        if (a.title > b.title) {
          return 1
        }
        return 0
      })
    },
    removeTodoItem(index: number) {
      console.log('remove', index)
      this.todoItems.splice(index, 1)
      storage.save(this.todoItems)
    },
    toggleTodoItemComplete(todoItem: Todo, index: number) {
      this.todoItems.splice(index, 1, {
        title: todoItem.title,
        done: !todoItem.done
      })
      storage.save(this.todoItems)
    }
  },
  created() {
    this.fetchTodoItems()
  },
})
</script>
