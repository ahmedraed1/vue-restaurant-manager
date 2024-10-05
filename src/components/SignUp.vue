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
          v-model="data.email"
          type="text"
          class="block border border-grey-light w-full p-3 rounded mb-4"
          name="email"
          placeholder="Email"
        />

        <input
          v-model="data.password"
          type="password"
          class="block border border-grey-light w-full p-3 rounded mb-4"
          name="password"
          placeholder="Password"
        />
        <input
          v-model="data.confirm_password"
          type="password"
          class="block border border-grey-light w-full p-3 rounded mb-4"
          name="confirm_password"
          placeholder="Confirm Password"
        />

        <button
          @click="signUp()"
          class="w-full bg-green-600 hover:bg-green-700 text-white font-bold py-3 rounded p-3"
        >
          Create Account
        </button>

        <!-- <div class="text-center text-sm text-grey-dark mt-4">
          By signing up, you agree to the
          <a class="no-underline border-b border-grey-dark text-grey-dark" href="#">
            Terms of Service
          </a>
          and
          <a class="no-underline border-b border-grey-dark text-grey-dark" href="#">
            Privacy Policy
          </a>
        </div> -->
      </div>

      <div class="text-grey-dark mt-6">
        Already have an account?
        <RouterLink class="no-underline border-b border-blue text-blue" to="/login">
          Log in
        </RouterLink>
      </div>
    </div>
  </div>
</template>
<script setup>
import { ref } from 'vue'
import axios from 'axios'
import { RouterLink } from 'vue-router'

const data = ref({
  username: '',
  email: '',
  password: '',
  confirm_password: ''
})

async function signUp() {
  let usersLength
  await axios.get('http://localhost:3000/users').then((response) => {
    usersLength = response.data.length
  })

  if (data.value.password === data.value.confirm_password) {
    await axios
      .post('http://localhost:3000/users', {
        id: usersLength + 1,
        username: data.value.username,
        password: data.value.password
      })
      .then((response) => {
        if (response.status === 201) {
          localStorage.setItem('user', JSON.stringify(response.data))
          console.log('success')
          this.$router.push('/')
        }
      })
  }
}
</script>
