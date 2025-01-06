<template>
  <div id="page">
    <h1>Product Management</h1>
    <div class="add-product">
      <div>
      <input type="text" placeholder="Enter name" v-model="form.name" />
      <input type="number" v-model="form.price" />
      <input type="checkbox" class="checkbox" v-model="form.status">
      <button @click="save">Save</button>
      <button @click="clearForm">Cancel</button>
    </div>
    <div  class="status-shelf">
      <button @click="filter = 'all'">All</button>
      <button @click="filter = 'on_shelf'">On Shelf</button>
      <button @click="filter = 'off_shelf'">Off Shelf</button>
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
          <tr v-for="product in filteredProducts" :key="product.id">
            <td>{{ product.id }}</td>
            <td>{{ product.name }}</td>
            <td>{{ product.price }}</td>
            <td>{{ product.status ? 'On Shelf' : 'Off Shelf' }}</td>
            <td>
              <button @click="editproduct(product.id)">Edit</button>
              <button @click="deleteproduct(product.id)">Delete</button>
            </td>
          </tr>
          <tr v-if="filteredProducts.length === 0">
            <td colspan="5">No Data</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'
interface product {
  id: number
  name: string
  price: number
}

const form = ref<product>({ id: 0, name: '', price: 0, status: true })
const products = ref<product[]>([])
const lastId = ref(1)
const editedIndex = ref<number | null>(null)

const filter = ref<string>('all')

const filteredProducts = computed(() => {
  if (filter.value === 'on_shelf') {
    return products.value.filter((product) => product.status === true)
  }
  if (filter.value === 'off_shelf') {
    return products.value.filter((product) => product.status === false)
  }
  return products.value
})

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
  form.value = { id: 0, name: '', price: 0, status: true }
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

.checkbox {
  margin-left: 10px;
  margin-right: 10px;
}

td,
th {
  padding: 10px;
  text-align: center;
}

.status-shelf {
  margin-top: 20px;
}

h1 {
  margin-bottom: 10px;
}

</style>
