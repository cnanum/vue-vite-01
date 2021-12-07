<script setup lang="ts">
import {ref} from 'vue';

const todo = ref('')

type TodoInputEmit = {
  (e: 'add', content: string): void
}

const emit = defineEmits<TodoInputEmit>()

function saveTodo() {
  emit('add', todo.value)
  todo.value = ''
}
</script>

<template>

  <input type="text" v-model="todo" v-on:keydown.enter="saveTodo">
</template>

<style scoped>
input {@apply border border-gray-400 px-4 py-2 text-lg;}
</style>
