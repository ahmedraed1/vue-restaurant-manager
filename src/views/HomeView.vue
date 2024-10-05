<template>
  <main>
    <component :is="operations[operation]"></component>
  </main>
</template>
<script setup>
import { ref } from 'vue'
import { onMounted } from 'vue'
import router from '@/router'
import AddRestaurant from '@/components/AddRestaurant.vue'
import DeleteRestaurant from '@/components/DeleteRestaurant.vue'
import UpdateRestaurant from '@/components/UpdateRestaurant.vue'

const operations = {
  AddRestaurant,
  DeleteRestaurant,
  UpdateRestaurant
}
const operation = ref('AddRestaurant')

console.log(router.currentRoute.value)

onMounted(() => {
  if (
    window.localStorage.getItem('user') === null ||
    window.localStorage.getItem('user') === undefined
  ) {
    router.push({ name: 'signup' })
  }
})
</script>
