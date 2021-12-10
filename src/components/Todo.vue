<script setup lang="ts">
import {ref} from 'vue';
import TodoInput from './TodoInput.vue';
import TodoList from './TodoList.vue';

export type Todo = {
  id: number;
  content: string;
  completed: boolean;
}

const todoList = ref<Todo[]>([
  {id: 1, content: '밥먹기', completed: false},
  {id: 2, content: '잠자기', completed: false},
  {id: 3, content: '일하기', completed: false},
])

function addTodo(content: string) {
  const newTodo = {
    id: todoList.value.length + 1,
    content: content,
    completed:false
  }
  todoList.value.push(newTodo)
}

function removeTodo(id: number) {
  // const index = todoList.value.findIndex(t => t.id === id)
  // todoList.value.splice(index, 1)
  todoList.value = todoList.value.filter(t => t.id !== id)
}

</script>

<template>
  <span class="text-4xl font-semibold">NEW TODO: </span>
  <TodoInput v-on:add="addTodo" />
  <section class="my-10">
    <h1 class="text-4xl font-semibold">TODOs</h1>

    <TodoList :list="todoList.filter(t => !t.completed)"
              v-on:remove="removeTodo" />
  </section>


  <section class="mb-10">
    <h1 class="text-4xl font-semibold">COMPLETEs</h1>

    <TodoList :list="todoList.filter(t => t.completed)"
              v-on:remove="removeTodo" />
  </section>

</template>

<style scoped>
</style>
