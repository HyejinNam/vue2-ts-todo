<template>
  <li>
    <span class='item complete' :class="todoItem.done ? 'complete' : null" @click='toggleItem'>{{ todoItem }}</span>
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