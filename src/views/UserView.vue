<template>
  <div>User View</div>
  <div id="page">
    <h1>User Management</h1>
    <div>
      <input type="text" placeholder="Enter email" v-model="form.email" />
      <input type="password" placeholder="Enter password" v-model="form.password" />
      <button @click="addUser">Save</button>
      <button>cancel</button>
    </div>
    <div>
      <table border="1">
        <thead>
          <th>ID</th>
          <th>Email</th>
          <th>Password</th>
          <th>Action</th>
        </thead>
        <tbody>
          <tr></tr>
          <tr v-for="user in users" :key="user.id">
            <td>{{ user.id }}</td>
            <td>{{ user.email }}</td>
            <td>{{ user.password }}</td>
            <td>
              <button>Edit</button>
              <button>Delete</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, reactive } from 'vue'
interface User {
  id: number
  email: string
  password: string
}

const form = ref<User>({ id: 0, email: '', password: '' })
const users = ref<User[]>([])
const lastId = ref(1)
const editedId = ref<number | null>(null)

function addUser() {
  users.value.push({ ...form.value, id: lastId.value })
  lastId.value++
  clearForm()
}

function clearForm() {
  form.value = { id: 0, email: '', password: '' }
}
</script>

<style scoped></style>
<style scoped>
#page {
  text-align: center;
}

table {
  margin: 20px auto;
  width: 80%;
  border-style: solid;
  border-collapse: collapse;
}

input,
button {
  margin-left: 4px;
  padding: 4px;
}

td,
th {
  padding: 10px;
  text-align: center;
}
</style>
