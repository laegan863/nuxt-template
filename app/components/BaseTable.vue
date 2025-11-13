<template>
  <div class="w-full space-y-4">
    <!-- Search Bar -->
    <div v-if="searchable" class="flex items-center justify-between gap-3">
      <div class="flex items-center gap-2">
        <span class="text-sm text-gray-600 dark:text-gray-400">Show</span>
        <div class="w-24">
          <BaseSelect
            :model-value="perPage"
            @update:model-value="$emit('update:perPage', $event)"
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
        <button
          class="p-3 rounded-xl border-2 border-gray-200 dark:border-gray-700 hover:border-gray-900 dark:hover:border-white text-gray-600 dark:text-gray-400 hover:text-gray-900 dark:hover:text-white transition-all duration-200 bg-white dark:bg-gray-900"
          title="Filter"
        >
          <font-awesome-icon icon="filter" class="text-sm" />
        </button>
        <div class="relative w-64">
          <div class="absolute left-3 top-1/2 -translate-y-1/2 text-gray-400 dark:text-gray-500">
            <font-awesome-icon icon="search" class="text-sm" />
          </div>
          <input
            type="text"
            :value="searchQuery"
            @input="$emit('update:searchQuery', $event.target.value)"
            :placeholder="searchPlaceholder"
            class="w-full pl-10 pr-4 py-3 text-sm rounded-xl border-2 transition-all duration-200 focus:outline-none placeholder:text-gray-400 dark:placeholder:text-gray-500 border-gray-200 dark:border-gray-700 focus:border-gray-900 dark:focus:border-white hover:border-gray-300 dark:hover:border-gray-600 bg-white dark:bg-gray-900 text-gray-900 dark:text-gray-100"
          />
        </div>
      </div>
    </div>

    <div class="overflow-x-auto rounded-xl border-2 border-gray-200 dark:border-gray-700">
      <table class="w-full text-sm text-left">
        <thead class="text-xs uppercase bg-gray-50 dark:bg-gray-800 border-b-2 border-gray-200 dark:border-gray-700">
          <tr>
            <th
              v-for="column in columns"
              :key="column.key"
              :class="column.headerClass"
              class="px-6 py-4 font-semibold text-gray-700 dark:text-gray-300 tracking-wider"
            >
              {{ column.label }}
            </th>
            <th v-if="$slots.actions || hasActions" class="px-6 py-4 font-semibold text-gray-700 dark:text-gray-300 tracking-wider">
              Actions
            </th>
          </tr>
        </thead>
        <tbody class="divide-y divide-gray-200 dark:divide-gray-700">
          <tr
            v-for="(row, index) in paginatedData"
            :key="index"
            class="bg-white dark:bg-gray-900 hover:bg-gray-50 dark:hover:bg-gray-800/50 transition-colors duration-150"
            :class="rowClass"
          >
            <td
              v-for="column in columns"
              :key="column.key"
              :class="column.cellClass"
              class="px-6 py-4 text-gray-900 dark:text-gray-100"
            >
              <slot :name="`cell-${column.key}`" :row="row" :value="row[column.key]">
                {{ row[column.key] }}
              </slot>
            </td>
            <td v-if="$slots.actions || hasActions" class="px-6 py-4">
              <slot name="actions" :row="row" :index="index">
                <!-- Default action buttons if no slot provided -->
                <div v-if="row.actions" class="flex gap-2">
                  <button
                    v-if="row.actions.view"
                    @click="$emit('view', row)"
                    class="p-1.5 rounded-lg hover:bg-blue-50 dark:hover:bg-blue-900/20 text-blue-600 dark:text-blue-400 transition-colors"
                    title="View"
                  >
                    <font-awesome-icon icon="eye" class="text-sm" />
                  </button>
                  <button
                    v-if="row.actions.edit"
                    @click="$emit('edit', row)"
                    class="p-1.5 rounded-lg hover:bg-green-50 dark:hover:bg-green-900/20 text-green-600 dark:text-green-400 transition-colors"
                    title="Edit"
                  >
                    <font-awesome-icon icon="edit" class="text-sm" />
                  </button>
                  <button
                    v-if="row.actions.delete"
                    @click="$emit('delete', row)"
                    class="p-1.5 rounded-lg hover:bg-red-50 dark:hover:bg-red-900/20 text-red-600 dark:text-red-400 transition-colors"
                    title="Delete"
                  >
                    <font-awesome-icon icon="trash" class="text-sm" />
                  </button>
                </div>
              </slot>
            </td>
          </tr>
          <tr v-if="!paginatedData || paginatedData.length === 0">
            <td :colspan="columns.length + ($slots.actions || hasActions ? 1 : 0)" class="px-6 py-12 text-center text-gray-500 dark:text-gray-400">
              <div class="flex flex-col items-center gap-2">
                <font-awesome-icon icon="inbox" class="text-3xl opacity-50" />
                <p>{{ emptyMessage }}</p>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    
    <!-- Pagination -->
    <div v-if="pagination && totalPages > 1" class="flex items-center justify-between mt-4">
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
  columns: {
    type: Array,
    required: true
  },
  data: {
    type: Array,
    default: () => []
  },
  emptyMessage: {
    type: String,
    default: 'No data available'
  },
  rowClass: {
    type: String,
    default: ''
  },
  pagination: {
    type: Boolean,
    default: true
  },
  perPage: {
    type: Number,
    default: 10
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
  }
})

const emit = defineEmits(['update:searchQuery', 'update:perPage', 'view', 'edit', 'delete'])

const currentPage = ref(1)

// Check if any row has actions
const hasActions = computed(() => {
  return props.data.some(row => row.actions && (row.actions.view || row.actions.edit || row.actions.delete))
})

// Filtered data based on search
const filteredData = computed(() => {
  if (!props.searchQuery) {
    return props.data
  }
  
  const query = props.searchQuery.toLowerCase()
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
  
  const start = (currentPage.value - 1) * props.perPage
  const end = start + props.perPage
  return filteredData.value.slice(start, end)
})

const totalPages = computed(() => Math.ceil(filteredData.value.length / props.perPage))

const startItem = computed(() => {
  if (filteredData.value.length === 0) return 0
  return (currentPage.value - 1) * props.perPage + 1
})

const endItem = computed(() => {
  const end = currentPage.value * props.perPage
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
watch(() => props.searchQuery, () => {
  currentPage.value = 1
})

// Reset to page 1 when perPage changes
watch(() => props.perPage, () => {
  currentPage.value = 1
})
</script>
