<script setup lang="ts">
import './style.css'
import {reactive, ref} from 'vue';
import Todo from './components/Todo.vue';

let str = ref('abcd')
const num = ref(123)
const arr = ref([1, 2, 3, 4])
const users = ref([
  {id: 1, name: '홍홍홍', age: 33},
  {id: 2, name: '캬캬캬', age: 22},
  {id: 3, name: '코코코', age: 44},
])

function addUser() {
  users.value.push({id: Math.random(), name: '흐흐흐', age:1})
}

function removeUser(user) {
  users.value.splice(users.value.indexOf(user), 1)
}

const obj = reactive({
  key1: 1,
  key2: 'abc',
  key3: true
})

function changeStr() {
  console.log('before str', str)
  str.value = 'asdfasdf'
  console.log('after str', str)
  obj.key2 = 'asdfasdfsdfasd'
}

const newUser = reactive({
  id: '',
  email: '',
  name: '',
  sex: 'F',
  hobbies: [],
})

function saveUser() {
  // validation.......

  console.log('저장하자!!!!!!', newUser)
}

</script>

<template>

  <div class="my-20">
    <Todo />
  </div>





  <div>{{newUser}}</div>
  <button class="bg-indigo-600 text-white" v-on:click="newUser.email = 'abcd@test.com'">change email!!!!</button>
  <button class="bg-yellow-600 text-white" v-on:click="saveUser">save</button>
  <form>
    <div>ID: <input type="text" v-model="newUser.id"></div>
    <div>email: <input type="text" v-model="newUser.email"></div>
    <div>이름: <input type="text" v-model="newUser.name"></div>
    <div class="flex gap-4">
      <div>성별:</div>
      <div class="flex gap-4">
        <label><input type="radio" name="sex" value="M" v-model="newUser.sex">남</label>
        <label><input type="radio" name="sex" value="F" v-model="newUser.sex">여</label>
      </div>
    </div>
    <div class="flex gap-4">
      <div>성별:</div>
      <select v-model="newUser.sex">
        <option value="F">여자</option>
        <option value="M">남자</option>
      </select>
    </div>
    <div class="flex gap-4">
      <div>취미:</div>
      <div class="flex gap-4">
        <label><input type="checkbox" name="hobbies" value="bb" v-model="newUser.hobbies">bb</label>
        <label><input type="checkbox" name="hobbies" value="aa" v-model="newUser.hobbies">aa</label>
        <label><input type="checkbox" name="hobbies" value="농구" v-model="newUser.hobbies">농구</label>
        <label><input type="checkbox" name="hobbies" value="볼링" v-model="newUser.hobbies">볼링</label>
      </div>
    </div>
  </form>


  <div>
    <button class="bg-indigo-600 text-white" v-on:click="addUser">add!!!!</button>
    <ul>
      <li v-for="user in users">
        {{user.id}} / {{user.name}} / {{user.age}}
        / [<button v-on:click="removeUser(user)">x</button>]
      </li>
    </ul>
  </div>
  <div class="p-4 bg-yellow-300">
    <h1>str: {{str}}</h1>
    <h1>num: {{num}}</h1>
    <h1>arr: {{arr}}</h1>
    <h1>obj.key1: {{obj.key1}}</h1>
    <h1>obj.key2: {{obj.key2}}</h1>
    <h1>obj.key3: {{obj.key3}}</h1>
    <button class="bg-indigo-600 text-white" v-on:click="changeStr">change!!!!</button>
  </div>
  <div class="p-4 bg-pink-300">
  </div>








  <img alt="Vue logo" src="./assets/logo.png" />

</template>

<style scoped>
input[type=text] {@apply border border-gray-500 p-2;}
</style>
