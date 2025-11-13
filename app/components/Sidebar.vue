<script setup>
import { ref, computed } from 'vue'
import { useRoute } from '#app'

const route = useRoute()

defineProps({
  isCollapsed: {
    type: Boolean,
    default: false
  },
  isMobileMenuOpen: {
    type: Boolean,
    default: false
  }
})

defineEmits(['close-mobile-menu'])

const isUserMenuOpen = ref(false)
const isUserActive = ref(true) // Toggle this to change online/offline status

const sidebarData = [
  {
    icon: 'gauge',
    name: 'Dashboard',
    link: '/dashboard'
  },
  {
    icon: 'folder',
    name: 'Pages',
    link: '#',
    children: [
      { icon: 'circle', name: 'Empty Page', link: '/empty' },
      { icon: 'circle', name: 'Analytics', link: '/dashboard' },
      { icon: 'circle', name: 'Form Components', link: '/forms' },
      { icon: 'circle', name: 'UI Components', link: '/components' },
      { icon: 'circle', name: 'Custom Table', link: '/table' }
    ]
  },
  {
    icon: 'cog',
    name: 'Settings',
    link: '/settings'
  }
]

const openDropdowns = ref({})

const toggleDropdown = (index) => {
  openDropdowns.value[index] = !openDropdowns.value[index]
}

const isDropdownOpen = (index) => {
  return openDropdowns.value[index] || false
}

const isMenuItemActive = (item) => {
  if (item.children) {
    return item.children.some(child => route.path === child.link)
  }
  return route.path === item.link
}

const toggleUserMenu = () => {
  isUserMenuOpen.value = !isUserMenuOpen.value
}
</script>

<style scoped>
/* Custom scrollbar for sidebar */
nav::-webkit-scrollbar {
  width: 4px;
}

nav::-webkit-scrollbar-track {
  background: transparent;
}

nav::-webkit-scrollbar-thumb {
  background: rgba(156, 163, 175, 0.5);
  border-radius: 2px;
}

nav::-webkit-scrollbar-thumb:hover {
  background: rgba(107, 114, 128, 0.7);
}
</style>
<template>
  <aside 
    class="fixed left-0 top-0 h-screen z-[100] transition-all duration-300 bg-white dark:bg-gray-800 border-r border-gray-200 dark:border-gray-700 shadow-lg flex flex-col"
    :class="[
      isCollapsed ? 'w-[70px]' : 'w-[250px]',
      isMobileMenuOpen ? 'translate-x-0' : '-translate-x-full md:translate-x-0'
    ]"
  >
    <!-- Logo/Brand -->
    <div class="h-16 px-4 flex items-center justify-between border-b border-gray-200 dark:border-gray-700 flex-shrink-0">
      <div class="flex items-center gap-3">
        <div class="w-10 h-10 rounded-xl bg-gradient-to-br from-gray-700 to-gray-900 dark:from-gray-600 dark:to-gray-800 flex items-center justify-center shadow-md">
          <font-awesome-icon icon="crown" class="text-white text-base" />
        </div>
        <span v-if="!isCollapsed" class="text-base font-bold text-gray-900 dark:text-white">
          Admin
        </span>
      </div>
      <!-- Mobile Close Button -->
      <button 
        @click="$emit('close-mobile-menu')"
        class="md:hidden p-2 rounded-lg hover:bg-gray-100 dark:hover:bg-gray-700 text-gray-600 dark:text-gray-300"
      >
        <font-awesome-icon icon="times" class="text-base" />
      </button>
    </div>
    
    <!-- Navigation -->
    <nav class="p-3 space-y-2 overflow-y-auto flex-1">
      <!-- Dynamic Menu Items -->
      <template v-for="(item, index) in sidebarData" :key="index">
        <!-- Menu Item with Children (Dropdown) -->
        <div v-if="item.children">
          <button
            @click="toggleDropdown(index)"
            class="w-full flex items-center justify-between px-3 py-3 rounded-xl text-gray-600 dark:text-gray-300 hover:text-gray-900 dark:hover:text-white hover:bg-gray-50 dark:hover:bg-gray-700 transition-all text-sm"
            :class="{ '!bg-[#545454] !text-white shadow-sm': isDropdownOpen(index) || isMenuItemActive(item) }"
          >
            <div class="flex items-center gap-3">
              <font-awesome-icon :icon="item.icon" class="text-base min-w-[20px]" />
              <span v-if="!isCollapsed" class="font-medium">{{ item.name }}</span>
            </div>
            <font-awesome-icon 
              v-if="!isCollapsed"
              icon="chevron-down" 
              class="text-xs transition-transform duration-300"
              :class="{ 'rotate-180': isDropdownOpen(index) }"
            />
          </button>
          
          <!-- Dropdown Menu -->
          <transition
            enter-active-class="transition-all duration-300 ease-out"
            leave-active-class="transition-all duration-200 ease-in"
            enter-from-class="opacity-0 -translate-y-2"
            enter-to-class="opacity-100 translate-y-0"
            leave-from-class="opacity-100 translate-y-0"
            leave-to-class="opacity-0 -translate-y-2"
          >
            <div 
              v-if="isDropdownOpen(index) && !isCollapsed"
              class="mt-2 space-y-1 ml-3 pl-4 border-l-2 border-gray-200 dark:border-gray-700"
            >
              <NuxtLink 
                v-for="(child, childIndex) in item.children"
                :key="childIndex"
                :to="child.link" 
                class="flex items-center gap-3 px-3 py-2 rounded-lg text-xs text-gray-500 dark:text-gray-400 hover:text-gray-900 dark:hover:text-white hover:bg-gray-50 dark:hover:bg-gray-700/50 transition-all"
                active-class="!text-white !bg-[#545454]"
              >
                <font-awesome-icon :icon="child.icon" class="text-[6px]" />
                <span>{{ child.name }}</span>
              </NuxtLink>
            </div>
          </transition>
        </div>

        <!-- Menu Item without Children -->
        <NuxtLink 
          v-else
          :to="item.link" 
          class="flex items-center gap-3 px-3 py-3 rounded-xl text-gray-600 dark:text-gray-300 hover:text-gray-900 dark:hover:text-white hover:bg-gray-50 dark:hover:bg-gray-700 transition-all group text-sm"
          active-class="!bg-[#545454] !text-white shadow-sm"
        >
          <font-awesome-icon :icon="item.icon" class="text-base min-w-[20px]" />
          <span v-if="!isCollapsed" class="font-medium">{{ item.name }}</span>
        </NuxtLink>
      </template>
    </nav>

    <!-- User Footer -->
    <div class="border-t border-gray-200 dark:border-gray-700 p-3 flex-shrink-0">
      <div class="relative">
        <button
          @click="toggleUserMenu"
          class="w-full flex items-center gap-3 px-3 py-2 rounded-xl hover:bg-gray-50 dark:hover:bg-gray-700 transition-all"
          :class="{ 'justify-center': isCollapsed }"
        >
          <div class="relative flex-shrink-0">
            <div class="w-10 h-10 rounded-full bg-gradient-to-br from-gray-700 to-gray-900 dark:from-gray-600 dark:to-gray-800 flex items-center justify-center">
              <font-awesome-icon icon="user" class="text-white text-sm" />
            </div>
            <span 
              class="absolute bottom-0 right-0 w-3 h-3 rounded-full border-2 border-white dark:border-gray-800"
              :class="isUserActive ? 'bg-green-500' : 'bg-red-500'"
            ></span>
          </div>
          <div v-if="!isCollapsed" class="flex-1 text-left overflow-hidden">
            <p class="text-xs font-medium text-gray-900 dark:text-white truncate">John Doe</p>
            <p class="text-[10px] text-gray-500 dark:text-gray-400 truncate">Admin</p>
          </div>
          <font-awesome-icon 
            v-if="!isCollapsed"
            icon="chevron-down" 
            class="text-xs text-gray-500 dark:text-gray-400 transition-transform duration-300"
            :class="{ 'rotate-180': isUserMenuOpen }"
          />
        </button>

        <!-- User Dropdown Menu -->
        <transition
          enter-active-class="transition-all duration-200 ease-out"
          leave-active-class="transition-all duration-150 ease-in"
          enter-from-class="opacity-0 scale-95 translate-y-2"
          enter-to-class="opacity-100 scale-100 translate-y-0"
          leave-from-class="opacity-100 scale-100 translate-y-0"
          leave-to-class="opacity-0 scale-95 translate-y-2"
        >
          <div 
            v-if="isUserMenuOpen && !isCollapsed"
            class="absolute bottom-full left-0 right-0 mb-2 bg-white dark:bg-gray-700 rounded-xl shadow-lg border border-gray-200 dark:border-gray-600 overflow-hidden"
          >
            <button class="w-full flex items-center gap-3 px-4 py-3 text-sm text-gray-700 dark:text-gray-200 hover:bg-gray-50 dark:hover:bg-gray-600 transition-colors">
              <font-awesome-icon icon="user" class="text-gray-500 dark:text-gray-400" />
              <span>Profile</span>
            </button>
            <button class="w-full flex items-center gap-3 px-4 py-3 text-sm text-gray-700 dark:text-gray-200 hover:bg-gray-50 dark:hover:bg-gray-600 transition-colors">
              <font-awesome-icon icon="cog" class="text-gray-500 dark:text-gray-400" />
              <span>Settings</span>
            </button>
            <div class="border-t border-gray-200 dark:border-gray-600"></div>
            <button class="w-full flex items-center gap-3 px-4 py-3 text-sm text-red-600 dark:text-red-400 hover:bg-red-50 dark:hover:bg-red-900/20 transition-colors">
              <font-awesome-icon icon="sign-out-alt" class="text-red-500 dark:text-red-400" />
              <span>Logout</span>
            </button>
          </div>
        </transition>
      </div>
    </div>
  </aside>
</template>
