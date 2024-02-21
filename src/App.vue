<script setup>
  import { onMounted, ref } from 'vue';
import DataTable from './components/DataTable.vue';
 const items = ref([])
  onMounted(async() => {
    const response = await fetch('https://jsonplaceholder.typicode.com/users')
    items.value = await response.json()
  })
</script>

<template>
  <div class="bg-gray-100 p-8 min-h-screen">
    <data-table :items="items"/>
  </div>
</template>

<style scoped>

</style>
