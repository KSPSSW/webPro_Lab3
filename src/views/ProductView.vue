<template>
  <div id="page">
    <h1>Product Management</h1>
    <div>
      <input type="text" placeholder="Enter name" v-model="form.name" />
      <input type="number" v-model="form.price" />
      <input type="checkbox" name="" id="on-shelf" />
      <button @click="save">Save</button>
      <button>cancel</button>
    </div>
    <div>
      <table border="1">
        <thead>
          <th>ID</th>
          <th>Name</th>
          <th>Price</th>
          <th>Status</th>
          <th>Action</th>
        </thead>
        <tbody>
          <tr v-for="product in products" :key="product.id">
            <td>{{ product.id }}</td>
            <td>{{ product.name }}</td>
            <td>{{ product.price }}</td>
            <td></td>
            <td>
              <button @click="editproduct(product.id)">Edit</button>
              <button @click="deleteproduct(product.id)">Delete</button>
            </td>
          </tr>
          <tr v-if="products.length === 0">
            <td colspan="5">No Data</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
interface product {
  id: number
  name: string
  price: number
}

const form = ref<product>({ id: 0, name: '', price: 0 })
const products = ref<product[]>([])
const lastId = ref(1)
const editedIndex = ref<number | null>(null)

function save() {
  if (editedIndex.value !== null) {
    updateproduct()
  } else {
    addproduct()
  }
}

function editproduct(id: number) {
  const index = products.value.findIndex(function (item) {
    return item.id === id
  })
  editedIndex.value = index
  form.value = { ...products.value[index] }
}

function updateproduct() {
  if (editedIndex.value !== null) {
    products.value[editedIndex.value] = { ...form.value }
    clearForm()
    editedIndex.value = null
  }
}

function addproduct() {
  products.value.push({ ...form.value, id: lastId.value })
  lastId.value++
  clearForm()
}

function deleteproduct(id: number) {
  const index = products.value.findIndex(function (item) {
    return item.id === id
  })
  products.value.splice(index, 1)
}

function clearForm() {
  form.value = { id: 0, name: '', price: 0 }
}
</script>

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
