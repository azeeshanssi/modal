<template>
  <Modal v-if="showModal" @close="showModal = false" @submitted="handleSubmit" />
  <div
    v-if="!showModal"
    class="w-screen h-screen bg-gray-100 text-gray-800 flex flex-col items-center py-8"
  >
    <h1 class="text-3xl font-medium mb-4">Welcome! Please Insert User Information</h1>

    <div class="w-full mt-8 flex flex-col items-center">
      <h1 class="text-3xl font-medium mb-2 mx-2">All Users</h1>
      <table class="w-5/6 border-collapse mx-2">
        <thead>
          <tr class="bg-blue-400 w-full">
            <th class="p-4 border">Name</th>
            <th class="p-4 border">Email</th>
            <th class="p-4 border">Phone</th>
            <th class="p-4 border">Address</th>
            <th class="p-4 border">Country</th>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="(user, index) in users"
            :key="user.name"
            :class="[
              index % 2 === 0 ? 'bg-blue-200' : 'bg-white',
              'hover:bg-gray-400',
              'transition duration-300 ease-in-out',
              'w-full max-w-full'
            ]"
          >
            <td class="p-4 border text-center">{{ user.name }}</td>
            <td class="p-4 border text-center">{{ user.email }}</td>
            <td class="p-4 border text-center">{{ user.phone }}</td>
            <td class="p-4 border text-center">{{ user.address }}</td>
            <td class="p-4 border text-center">{{ user.country }}</td>
          </tr>
        </tbody>
      </table>
      <div class="flex justify-center mt-2">
        <button
          @click="showModal = true"
          class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-md transition duration-300 ease-in-out"
        >
          Add User
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Modal from './components/Modal.vue'

//Modal

const showModal = ref(false)

const setModal = () => {
  showModal.value = true
}

const onModalClose = () => {
  showModal.value = false
}

//Table

const users = ref([])
const handleSubmit = (user) => {
  users.value.push(user.value)
}
</script>
