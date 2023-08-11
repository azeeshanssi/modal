<template>
  <div
    class="w-screen h-screen flex items-center justify-center bg-gray-500 bg-opacity-70"
    @click="closeModalOutside"
  >
    <div class="w-2/3 bg-white rounded-md shadow-lg h-3/4 flex overflow-hidden">
      <div id="left" class="w-1/3 px-2 flex flex-col bg-gray-100 text-gray-700 justify-center">
        <h1 class="text-2xl font-medium mb-4 text-center">Input your Data</h1>
        <form @submit.prevent="handleSubmit" class="space-y-4">
          <div class="flex flex-col w-full">
            <label for="name" class="mb-1 p-2">Name</label>
            <input
              v-model="user.name"
              id="name"
              type="text"
              placeholder="Your Name"
              class="border rounded-md py-2 px-3"
              required
            />
          </div>
          <div class="flex flex-col w-full">
            <label for="email" class="mb-1 p-2">Email</label>
            <input
              v-model="user.email"
              id="email"
              type="email"
              placeholder="Your Email"
              required
              class="border rounded-md py-2 px-3 h-10"
            />
          </div>
          <div class="flex flex-col w-full">
            <label for="phone" class="mb-1 p-2">Phone Number</label>
            <input
              v-model="user.phone"
              id="phone"
              type="text"
              placeholder="Your Number"
              required
              class="border rounded-md py-2 px-3 h-10"
            />
          </div>
          <div class="flex flex-col w-full">
            <label for="address" class="mb-1 p-2">Address</label>
            <input
              v-model="user.address"
              id="address"
              type="text"
              placeholder="Your Address"
              required
              class="border rounded-md py-2 px-3 h-10"
            />
          </div>
          <div class="flex flex-col w-full">
            <label for="country" class="mb-1 p-2">Country</label>
            <select
              v-model="user.country"
              id="country"
              required
              class="border rounded-md py-2 px-3 h-10"
            >
              <option disabled value="" selected>Please Select One</option>
              <option value="Pakistan">Pakistan</option>
              <option value="Germany">Germany</option>
              <option value="USA">USA</option>
            </select>
          </div>
          <div class="flex flex-col items-center">
            <button
              type="submit"
              class="bg-blue-500 hover:bg-blue-600 text-white font-semibold py-2 px-4 rounded-md h-10 w-20 transition duration-300 ease-in-out"
            >
              Add
            </button>
            <button
              @click.prevent="closeModal"
              class="bg-red-500 hover:bg-red-600 text-white font-semibold py-2 px-4 rounded-md mt-2 h-10 transition duration-300 ease-in-out"
            >
              Cancel
            </button>
          </div>
        </form>
      </div>
      <div id="right" class="w-2/3">
        <div class="w-full h-full flex justify-center items-center">
          <h1 class="text-2xl text-white">This is a Sample Modal</h1>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { defineEmits } from 'vue'

//Modal
const user = ref({
  name: '',
  email: '',
  phone: '',
  address: '',
  country: ''
})
const emit = defineEmits(['close', 'submitted'])

const handleSubmit = () => {
  emit('submitted', user)
  emit('close')
}

const closeModal = () => {
  emit('close')
}
const closeModalOutside = (event) => {
  if (event.target === event.currentTarget) {
    emit('close')
  }
}
</script>
<style>
#right {
  background-image: url('../assets/images/card-side.jpg');
}
</style>
