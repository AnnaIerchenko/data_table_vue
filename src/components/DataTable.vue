<script setup>
  import { computed, ref } from "vue"
  import FilterDropDown from "./FilterDropDown.vue"
  import FilterRadio from "./FilterRadio.vue"
  import SearchForm from "./SearchForm.vue"

const props = defineProps({
    items: {
      type: Array,
      required: true
    }
  })
  const searchFilter = ref('')

const filteredItems = computed(() => {
  if(searchFilter.value !== ''){
    return props.items.filter((item) => item.title.includes(searchFilter.value) || item.user.name.includes(searchFilter.value))
  }
  return props.items
})

const handleSearch = (search) => {
  searchFilter.value = search
}
</script>
<template>
  <div class="bg-white relative border rounded-lg">
    <div class="flex items-center justify-between">
      <!-- search bar -->
      <search-form @search="handleSearch"/>
      <div class="flex items-center justify-end text-sm font-semibold">
      <!-- radio buttons -->
        <filter-radio />
      </div>
      <!-- list of filter for status -->
      <filter-drop-down />
    </div>
    
    <table class="w-full text-sm text-left text-gray-500">
      <thead class="text-xs text-gray-700 uppercase bg-gray-50">
        <tr>
          <th class="px-4 py-3">ID</th>
          <th class="px-4 py-3">Assigned To</th>
          <th class="px-4 py-3">Status</th>
          <th class="px-4 py-3">Title</th>
          <th class="px-4 py-3">Due At</th>
          <th class="px-4 py-3">
            <span class="sr-only">Actions</span>
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in filteredItems" :key="item.id" class="border-b">
          <td class="px-4 py-3 font-medium text-gray-900">{{ item.id }}</td>
          <td class="px-4 py-3 font-medium text-gray-900">{{ item.name }}</td>
          <td class="px-4 py-3">{{ item.email }}</td>
          <td class="px-4 py-3">{{ item.address.city }}</td>
          <td class="px-4 py-3">{{ item.company.name }}</td>
          <td class="px-4 py-3 flex items-center justify-end">
            <a href="#" class="text-indigo-500 hover::underline">Details</a>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>