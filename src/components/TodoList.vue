<script setup lang="ts">
import {Todo} from './Todo.vue';

type TodoListProps = {
  list: Todo[]
}

const props = defineProps<TodoListProps>()

type TodoListEmit = {
  (e: 'remove', id: number): void
}

const emit = defineEmits<TodoListEmit>()

function removeTodo(id: number) {
  emit('remove', id)
}
</script>

<template>

  <ul class="flex flex-col gap-4">
    <li v-for="(todo, index) in props.list" :key="todo.id"
        class="bg-indigo-200 py-2 px-8 flex items-center justify-between"
        v-bind:class="{complete: todo.completed}">
      <label>
        <input type="checkbox" v-model="todo.completed">
        {{todo.content}}
      </label>
      <button v-on:click="removeTodo(todo.id)">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-gray-400 hover:text-red-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16" />
        </svg>
      </button>
    </li>
  </ul>
</template>

<style scoped>
.complete {@apply line-through text-gray-500;}
</style>
