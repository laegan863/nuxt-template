<template>
  <div class="w-full space-y-4">
    <!-- Search and Filter Bar -->
    <div v-if="searchable" class="flex items-center justify-between gap-4">
      <div class="flex items-center gap-3">
        <span class="text-sm text-gray-600 dark:text-gray-400">Show</span>
        <div class="w-24">
          <BaseSelect
            v-model="currentPerPage"
            :options="[
              { label: '5', value: 5 },
              { label: '10', value: 10 },
              { label: '25', value: 25 },
              { label: '50', value: 50 },
              { label: '100', value: 100 }
            ]"
          />
        </div>
        <span class="text-sm text-gray-600 dark:text-gray-400">entries</span>
      </div>
      
      <div class="flex items-center gap-2">
        <slot name="search-actions"></slot>
        <div class="w-64">
          <BaseInput 
            v-model="currentSearchQuery"
            :placeholder="searchPlaceholder"
            prefix-icon="search"
          />
        </div>
      </div>
    </div>

    <!-- Table -->
    <slot name="wrapper" :table-class="tableWrapperClass">
      <div :class="tableWrapperClass">
        <table :class="tableClass">
          <slot name="thead">
            <!-- Default thead if not provided -->
          </slot>
          <slot name="tbody" :filtered-data="filteredData" :paginated-data="paginatedData">
            <!-- Default tbody if not provided -->
          </slot>
          <slot name="tfoot">
            <!-- Optional tfoot -->
          </slot>
        </table>
      </div>
    </slot>

    <!-- Pagination -->
    <div v-if="pagination && totalPages > 1" class="flex items-center justify-between">
      <div class="text-sm text-gray-600 dark:text-gray-400">
        Showing {{ startItem }} to {{ endItem }} of {{ filteredData.length }} entries
      </div>
      <div class="flex gap-2">
        <button
          @click="changePage(currentPage - 1)"
          :disabled="currentPage === 1"
          class="px-3 py-1.5 text-sm rounded-lg border-2 transition-all duration-200"
          :class="currentPage === 1 
            ? 'border-gray-200 dark:border-gray-700 text-gray-400 dark:text-gray-600 cursor-not-allowed' 
            : 'border-gray-200 dark:border-gray-700 text-gray-700 dark:text-gray-300 hover:border-gray-900 dark:hover:border-white'"
        >
          Previous
        </button>
        <button
          v-for="page in visiblePages"
          :key="page"
          @click="changePage(page)"
          class="px-3 py-1.5 text-sm rounded-lg border-2 transition-all duration-200"
          :class="page === currentPage 
            ? 'border-gray-900 dark:border-white bg-gray-900 dark:bg-white text-white dark:text-gray-900 font-semibold' 
            : 'border-gray-200 dark:border-gray-700 text-gray-700 dark:text-gray-300 hover:border-gray-900 dark:hover:border-white'"
        >
          {{ page }}
        </button>
        <button
          @click="changePage(currentPage + 1)"
          :disabled="currentPage === totalPages"
          class="px-3 py-1.5 text-sm rounded-lg border-2 transition-all duration-200"
          :class="currentPage === totalPages 
            ? 'border-gray-200 dark:border-gray-700 text-gray-400 dark:text-gray-600 cursor-not-allowed' 
            : 'border-gray-200 dark:border-gray-700 text-gray-700 dark:text-gray-300 hover:border-gray-900 dark:hover:border-white'"
        >
          Next
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed, ref, watch } from 'vue'

const props = defineProps({
  data: {
    type: Array,
    default: () => []
  },
  searchable: {
    type: Boolean,
    default: true
  },
  searchQuery: {
    type: String,
    default: ''
  },
  searchPlaceholder: {
    type: String,
    default: 'Search...'
  },
  perPage: {
    type: Number,
    default: 10
  },
  pagination: {
    type: Boolean,
    default: true
  },
  tableClass: {
    type: String,
    default: 'w-full text-sm text-left'
  },
  tableWrapperClass: {
    type: String,
    default: 'overflow-x-auto rounded-xl border-2 border-gray-200 dark:border-gray-700'
  }
})

const emit = defineEmits(['update:searchQuery', 'update:perPage'])

// Internal state
const internalSearchQuery = ref('')
const internalPerPage = ref(10)
const currentPage = ref(1)

// Use internal state
const currentSearchQuery = computed({
  get: () => internalSearchQuery.value,
  set: (val) => {
    internalSearchQuery.value = val
    emit('update:searchQuery', val)
  }
})

const currentPerPage = computed({
  get: () => internalPerPage.value,
  set: (val) => {
    internalPerPage.value = val
    emit('update:perPage', val)
  }
})

// Initialize from props
watch(() => props.searchQuery, (newVal) => {
  if (newVal !== undefined && newVal !== internalSearchQuery.value) {
    internalSearchQuery.value = newVal
  }
}, { immediate: true })

watch(() => props.perPage, (newVal) => {
  if (newVal !== undefined && newVal !== internalPerPage.value) {
    internalPerPage.value = newVal
  }
}, { immediate: true })

// Filtered data based on search
const filteredData = computed(() => {
  if (!currentSearchQuery.value) {
    return props.data
  }
  
  const query = currentSearchQuery.value.toLowerCase()
  return props.data.filter(row => {
    return Object.values(row).some(value => 
      String(value).toLowerCase().includes(query)
    )
  })
})

// Paginated data
const paginatedData = computed(() => {
  if (!props.pagination) {
    return filteredData.value
  }
  
  const start = (currentPage.value - 1) * currentPerPage.value
  const end = start + currentPerPage.value
  return filteredData.value.slice(start, end)
})

const totalPages = computed(() => Math.ceil(filteredData.value.length / currentPerPage.value))

const startItem = computed(() => {
  if (filteredData.value.length === 0) return 0
  return (currentPage.value - 1) * currentPerPage.value + 1
})

const endItem = computed(() => {
  const end = currentPage.value * currentPerPage.value
  return end > filteredData.value.length ? filteredData.value.length : end
})

const visiblePages = computed(() => {
  const pages = []
  const maxVisible = 5
  let start = Math.max(1, currentPage.value - Math.floor(maxVisible / 2))
  let end = Math.min(totalPages.value, start + maxVisible - 1)
  
  if (end - start + 1 < maxVisible) {
    start = Math.max(1, end - maxVisible + 1)
  }
  
  for (let i = start; i <= end; i++) {
    pages.push(i)
  }
  
  return pages
})

const changePage = (page) => {
  currentPage.value = page
}

// Reset to page 1 when search changes
watch(currentSearchQuery, () => {
  currentPage.value = 1
})

// Reset to page 1 when perPage changes
watch(currentPerPage, () => {
  currentPage.value = 1
})
</script>
