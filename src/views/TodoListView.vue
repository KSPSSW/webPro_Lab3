<template>
  <div>
    <h1>Todo List</h1>
    <div>
      <input
        type="text"
        v-model="newTodo"
        placeholder="Add a new  task"
        @keyup.enter="addTodo"
      /><button @click="addTodo">Add</button>
    </div>
    <div>
      <button>Completed</button>
      <button>Not Completed</button>
      <button>All</button>
    </div>
    <ul>
      <li v-for="(todo, index) in filterTodos" v-bind:key="index">
        <span :class="{ completed: todo.completed }" @click="toggle(index)">{{ todo.text }}</span>
        <button @click="removeTodo(index)">Remove</button>
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'
interface Todo {
  text: string
  completed: boolean
}
function addTodo() {
  if (newTodo.value.trim() === '') return
  todos.value.push({
    text: newTodo.value.trim(),
    completed: false,
  })
  newTodo.value = ''
}
function removeTodo(index: number) {
  todos.value.splice(index, 1)
}
function toggle(index: number) {
  todos.value[index].completed = !todos.value[index].completed
}
const todos = ref<Todo[]>([
  { text: 'abc', completed: false },
  { text: 'def', completed: true },
  { text: 'ghi', completed: false },
])
const filterTodos = computed(function () {
  return todos.value
})
const newTodo = ref<string>('')
</script>

<style scope>
.completed {
  text-decoration: line-through;
  color: gray;
}
button {
  margin-left: 10px;
}
</style>
