<template>
  <li>
    <span
      class='item'
      :class="this.todoItemClass"
      @click='toggleItem'
    >{{ todoItem.title }}</span>
<!--    emit을 method에서 관리하지 않고 바로 이벤트에 넣을 수 있음 : 잘 사용하지 않음 -->
<!--    <button @click="$emit('remove')">삭제</button>-->
    <button @click="removeItem">삭제</button>
  </li>
</template>

<script lang="ts">
import Vue, { PropType } from 'vue'
import { Todo } from '@/App.vue'
export default Vue.extend({
  props: {
    todoItem: Object as PropType<Todo>,
    index: Number
  },
  computed: {
    // ts 로 computed 의 함수를 정의할 때 '반환 타입을 명시' 해야함
    todoItemClass(): string | null {
      return this.todoItem.done ? 'complete' : null
    }
  },
  methods: {
    removeItem() {
      this.$emit('remove', this.index)
    },
    toggleItem() {
      this.$emit('toggle', this.todoItem, this.index)
    }
  }
})
</script>
<style scoped>
.item {
  cursor: pointer;
}
.complete {
  text-decoration: line-through;
}
</style>