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
            <div id="dropdown" class="relative">
              <button
                @click.prevent="isOpen = !isOpen"
                class="cursor-pointer border rounded-lg bg-white p-3 h-10 hover:bg-gray-400 flex items-center justify-between"
              >
                <span class="mr-2">{{ user.country != '' ? user.country : 'Please Select' }}</span>
                <svg
                  :class="{ 'transform rotate-180': isOpen }"
                  xmlns="http://www.w3.org/2000/svg"
                  class="h-5 w-5 text-gray-600"
                  fill="none"
                  viewBox="0 0 24 24"
                  stroke="currentColor"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M19 9l-7 7-7-7"
                  />
                </svg>
              </button>
              <div v-if="isOpen" class="absolute mt-2 w-full border bg-white shadow-md rounded-md">
                <span
                  value="Pakistan"
                  class="block p-2 cursor-pointer hover:bg-gray-200"
                  @click="onSelect('Pakistan')"
                >
                  Pakistan
                </span>
                <span
                  value="Germany"
                  class="block p-2 cursor-pointer hover:bg-gray-200"
                  @click="onSelect('Germany')"
                >
                  Germany
                </span>
                <span
                  value="USA"
                  class="block p-2 cursor-pointer hover:bg-gray-200"
                  @click="onSelect('USA')"
                >
                  USA
                </span>
              </div>
            </div>
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
//DROPDOWN
const isOpen = ref(false)
const onSelect = (value) => {
  console.log(value)
  isOpen.value = !isOpen.value
  user.value.country = value
}
</script>
<style>
#right {
  background-image: url('../assets/images/card-side.jpg');
}
</style>
