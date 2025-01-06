<template>
  <div>User View</div>
  <div id="page">
    <h1>User Management</h1>
    <div>
      <input type="text" placeholder="Enter email" />
      <input type="text" placeholder="Enter password" />
      <button>Save</button>
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
          <tr>
            <td>1</td>
            <td>email1@mail.com</td>
            <td>password</td>
            <td><button>Edit</button><button>Delete</button></td>
          </tr>
          <tr>
            <td>2</td>
            <td>email2@mail.com</td>
            <td>password</td>
            <td><button>Edit</button><button>Delete</button></td>
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

const form = reactive<User>({ id: 0, email: '', password: '' })
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
}

td,
th {
  padding: 8px;
  text-align: center;
}
</style>
