<template>
  <div class="bg-grey-lighter min-h-screen flex flex-col">
    <div class="container max-w-sm mx-auto flex-1 flex flex-col items-center justify-center px-2">
      <div class="bg-white px-6 py-8 rounded shadow-md text-black w-full">
        <h1 class="mb-8 text-3xl text-center">Sign up</h1>
        <input
          v-model="data.username"
          type="text"
          class="block border border-grey-light w-full p-3 rounded mb-4"
          name="username"
          placeholder="Username"
        />

        <input
          v-model="data.password"
          type="password"
          class="block border border-grey-light w-full p-3 rounded mb-4"
          name="password"
          placeholder="Password"
        />

        <p v-if="error.ShowError" class="text-red-500 text-bold py-3">{{ error.errorMessage }}</p>

        <button
          @click="login()"
          class="w-full bg-green-600 hover:bg-green-700 text-white font-bold py-3 rounded p-3"
        >
          Log In
        </button>
        <!-- 
                    <div class="text-center text-sm text-grey-dark mt-4">
                        By signing up, you agree to the 
                        <a class="no-underline border-b border-grey-dark text-grey-dark" href="#">
                            Terms of Service
                        </a> and 
                        <a class="no-underline border-b border-grey-dark text-grey-dark" href="#">
                            Privacy Policy
                        </a>
                    </div> -->
      </div>

      <div class="text-grey-dark mt-6">
        Don't you have an account yet ?
        <RouterLink class="no-underline border-b border-blue text-blue" to="/signup">
          Register
        </RouterLink>
      </div>
    </div>
  </div>
</template>
<script setup>
import { RouterLink } from 'vue-router'
import { ref } from 'vue'
import axios from 'axios'
import router from '@/router'

const data = ref({
  username: '',
  password: ''
})

const error = ref({
  ShowError: false,
  errorMessage: 'Please enter username and password'
})

function login() {
  if (data.value.username === '' || data.value.password === '') {
    error.value.ShowError = true
    return
  }
  axios
    .get(
      'http://localhost:3000/users?username=' +
        data.value.username +
        '&password=' +
        data.value.password
    )
    .then((response) => {
      if (response.status === 200 && response.data.length > 0) {
        localStorage.setItem('user', JSON.stringify(response.data[0]))
        console.log('success')
        console.log(response.data)
        router.push({ name: 'home' })
      }
    })
    .catch((error) => {
      console.log(error)
    })
  error.value.ShowError = false
}
</script>
