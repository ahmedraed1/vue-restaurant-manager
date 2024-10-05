<template>
  <NavBar
    v-if="
      router.currentRoute.value.path == '/login'
        ? false
        : router.currentRoute.value.path == '/signup'
          ? false
          : true
    "
  />

  <RouterView />
</template>

<script setup>
import { RouterView } from 'vue-router'
import NavBar from './components/NavBar.vue'
import router from './router'

console.log('router')
</script>

<style scoped></style>
