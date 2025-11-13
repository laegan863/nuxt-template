<template>
  <div class="w-full" ref="selectWrapper">
    <label 
      v-if="label" 
      :for="selectId" 
      class="block text-sm font-medium mb-2"
      :class="labelClass || (error ? 'text-red-600 dark:text-red-400' : 'text-gray-700 dark:text-gray-300')"
    >
      {{ label }}
      <span v-if="required" class="text-red-500">*</span>
    </label>
    
    <div class="relative group">
      <!-- Custom Select Button -->
      <button
        type="button"
        @click="toggleDropdown"
        :disabled="disabled"
        class="relative w-full px-4 py-3 pr-10 text-sm rounded-xl border-2 transition-all duration-200 focus:outline-none text-left"
        :class="[
          selectClass,
          {
            'border-red-500 dark:border-red-400 focus:border-red-600 dark:focus:border-red-300 bg-red-50/50 dark:bg-red-950/20': error,
            'border-gray-200 dark:border-gray-700 focus:border-gray-900 dark:focus:border-white hover:border-gray-300 dark:hover:border-gray-600': !error && !disabled,
            'bg-white dark:bg-gray-900 text-gray-900 dark:text-gray-100': !disabled,
            'bg-gray-50 dark:bg-gray-900/50 text-gray-400 dark:text-gray-600 cursor-not-allowed border-gray-100 dark:border-gray-800': disabled
          }
        ]"
      >
        <span v-if="selectedLabel" class="block truncate">{{ selectedLabel }}</span>
        <span v-else class="block truncate text-gray-400 dark:text-gray-500">{{ placeholder }}</span>
      </button>
      
      <!-- Chevron Icon -->
      <div class="absolute right-3 top-1/2 -translate-y-1/2 pointer-events-none flex items-center gap-2 z-10">
        <font-awesome-icon 
          v-if="error" 
          icon="exclamation-circle" 
          class="text-sm text-red-500 dark:text-red-400" 
        />
        <font-awesome-icon 
          icon="chevron-down" 
          class="text-sm transition-all duration-200"
          :class="[
            isOpen ? 'rotate-180' : '',
            error ? 'text-red-500 dark:text-red-400' : 'text-gray-400 dark:text-gray-500',
            isOpen && !error ? 'text-gray-700 dark:text-gray-300' : ''
          ]" 
        />
      </div>

      <!-- Dropdown Menu -->
      <Transition
        enter-active-class="transition duration-200 ease-out"
        enter-from-class="transform scale-95 opacity-0"
        enter-to-class="transform scale-100 opacity-100"
        leave-active-class="transition duration-150 ease-in"
        leave-from-class="transform scale-100 opacity-100"
        leave-to-class="transform scale-95 opacity-0"
      >
        <div
          v-if="isOpen"
          class="absolute z-50 w-full mt-2 bg-white dark:bg-gray-800 border-2 border-gray-200 dark:border-gray-700 rounded-xl shadow-lg max-h-60 overflow-auto"
        >
          <div
            v-for="option in options"
            :key="getOptionValue(option)"
            @click="selectOption(option)"
            class="px-4 py-2.5 text-sm cursor-pointer transition-colors"
            :class="[
              option.disabled ? 'opacity-50 cursor-not-allowed' : 'hover:bg-gray-50 dark:hover:bg-gray-700',
              getOptionValue(option) === modelValue ? 'bg-gray-100 dark:bg-gray-700 font-medium text-gray-900 dark:text-white' : 'text-gray-700 dark:text-gray-300'
            ]"
          >
            {{ getOptionLabel(option) }}
          </div>
        </div>
      </Transition>
    </div>
    
    <p v-if="error" class="mt-1.5 text-xs text-red-600 dark:text-red-400">
      {{ error }}
    </p>
    <p v-else-if="hint" class="mt-1.5 text-xs text-gray-500 dark:text-gray-400">
      {{ hint }}
    </p>
  </div>
</template>

<script setup>
import { computed, ref, onMounted, onBeforeUnmount } from 'vue'

const props = defineProps({
  modelValue: {
    type: [String, Number, Boolean],
    default: ''
  },
  options: {
    type: Array,
    required: true
  },
  label: {
    type: String,
    default: ''
  },
  placeholder: {
    type: String,
    default: 'Select an option'
  },
  error: {
    type: String,
    default: ''
  },
  hint: {
    type: String,
    default: ''
  },
  disabled: {
    type: Boolean,
    default: false
  },
  required: {
    type: Boolean,
    default: false
  },
  selectClass: {
    type: String,
    default: ''
  },
  labelClass: {
    type: String,
    default: ''
  },
  valueKey: {
    type: String,
    default: 'value'
  },
  labelKey: {
    type: String,
    default: 'label'
  }
})

const emit = defineEmits(['update:modelValue'])

const selectId = computed(() => `select-${Math.random().toString(36).substr(2, 9)}`)
const isOpen = ref(false)
const selectWrapper = ref(null)

const getOptionValue = (option) => {
  if (typeof option === 'object' && option !== null) {
    return option[props.valueKey] ?? option.value ?? option
  }
  return option
}

const getOptionLabel = (option) => {
  if (typeof option === 'object' && option !== null) {
    return option[props.labelKey] ?? option.label ?? option.value ?? option
  }
  return option
}

const selectedLabel = computed(() => {
  const selected = props.options.find(opt => getOptionValue(opt) === props.modelValue)
  return selected ? getOptionLabel(selected) : ''
})

const toggleDropdown = () => {
  if (!props.disabled) {
    isOpen.value = !isOpen.value
  }
}

const selectOption = (option) => {
  if (!option.disabled) {
    emit('update:modelValue', getOptionValue(option))
    isOpen.value = false
  }
}

const handleClickOutside = (event) => {
  if (selectWrapper.value && !selectWrapper.value.contains(event.target)) {
    isOpen.value = false
  }
}

onMounted(() => {
  document.addEventListener('click', handleClickOutside)
})

onBeforeUnmount(() => {
  document.removeEventListener('click', handleClickOutside)
})
</script>
