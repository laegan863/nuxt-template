<template>
  <nav class="fixed top-0 right-0 z-50 transition-all duration-300 backdrop-blur-md bg-white/80 dark:bg-gray-900/80 border-b border-gray-200 dark:border-gray-700"
       :style="{ left: isCollapsed ? '70px' : '250px' }">
    <div class="h-16 px-6 flex items-center justify-between">
      <div class="flex items-center gap-4">
        <!-- Mobile Menu Toggle -->
        <button 
          type="button"
          name="toggle"
          @click="$emit('toggle-mobile-menu')"
          class="p-2 rounded-lg hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors text-gray-600 dark:text-gray-300 md:hidden">
          <font-awesome-icon icon="bars" class="text-base" />
        </button>

        <!-- Desktop Sidebar Toggle -->
        <button 
          type="button"
          name="toggle"
          @click="$emit('toggle-sidebar')"
          class="p-2 rounded-lg hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors text-gray-600 dark:text-gray-300 hidden md:block">
          <font-awesome-icon icon="bars" class="text-base" />
        </button>
        <p class="text-sm font-bold text-gray-800 dark:text-white hidden sm:block">Welcome in Admin Dashboard!!!</p>
      </div>
      
      <div class="flex items-center gap-2">
        <!-- Theme Toggle -->
        <button 
          type="button"
          name="toggle"
          @click="toggleTheme"
          class="p-2 rounded-lg hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors text-gray-600 dark:text-gray-300 relative">
          <font-awesome-icon :icon="colorMode === 'dark' ? 'sun' : 'moon'" class="text-base" />
        </button>
        
        <!-- Notifications -->
        <div class="relative">
          <button 
            type="button"
            name="toggle"
            @click="toggleNotifications"
            class="p-2 rounded-lg hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors text-gray-600 dark:text-gray-300 relative">
            <font-awesome-icon icon="bell" class="text-base" />
            <span class="absolute top-1 right-1 w-2 h-2 bg-red-500 rounded-full"></span>
          </button>

          <!-- Notifications Dropdown -->
          <transition
            enter-active-class="transition-all duration-200 ease-out"
            leave-active-class="transition-all duration-150 ease-in"
            enter-from-class="opacity-0 scale-95 -translate-y-2"
            enter-to-class="opacity-100 scale-100 translate-y-0"
            leave-from-class="opacity-100 scale-100 translate-y-0"
            leave-to-class="opacity-0 scale-95 -translate-y-2"
          >
            <div 
              v-if="isNotificationsOpen"
              class="absolute right-0 mt-2 w-80 bg-white dark:bg-gray-800 rounded-xl shadow-lg border border-gray-200 dark:border-gray-700 overflow-hidden"
            >
              <div class="px-4 py-3 border-b border-gray-200 dark:border-gray-700">
                <h3 class="text-xs font-semibold text-gray-900 dark:text-white">Notifications</h3>
              </div>
              <div class="max-h-96 overflow-y-auto">
                <div 
                  v-for="notification in notifications" 
                  :key="notification.id"
                  class="px-4 py-3 hover:bg-gray-50 dark:hover:bg-gray-700/50 transition-colors border-b border-gray-100 dark:border-gray-700 last:border-b-0"
                >
                  <div class="flex items-start gap-3">
                    <div class="w-7 h-7 rounded-lg flex items-center justify-center flex-shrink-0"
                         :class="notification.iconBg">
                      <font-awesome-icon :icon="notification.icon" class="text-xs" :class="notification.iconColor" />
                    </div>
                    <div class="flex-1 min-w-0">
                      <p class="text-xs font-medium text-gray-900 dark:text-white">{{ notification.title }}</p>
                      <p class="text-[10px] text-gray-500 dark:text-gray-400 mt-1">{{ notification.time }}</p>
                    </div>
                    <span v-if="!notification.read" class="w-2 h-2 bg-blue-500 rounded-full flex-shrink-0 mt-2"></span>
                  </div>
                </div>
              </div>
              <div class="px-4 py-2.5 border-t border-gray-200 dark:border-gray-700">
                <button class="w-full text-center text-xs font-medium text-gray-600 dark:text-gray-400 hover:text-gray-900 dark:hover:text-white transition-colors">
                  View All Notifications
                </button>
              </div>
            </div>
          </transition>
        </div>
        
        <!-- User Profile -->
        <div class="relative">
          <button 
            type="button"
            name="toggle"
            @click="toggleUserMenu"
            class="flex items-center gap-2 p-1.5 rounded-lg hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors">
            <div class="relative">
              <div class="w-8 h-8 rounded-full bg-gradient-to-br from-gray-700 to-gray-900 dark:from-gray-600 dark:to-gray-800 flex items-center justify-center">
                <font-awesome-icon icon="user" class="text-white text-sm" />
              </div>
              <span 
                class="absolute bottom-0 right-0 w-2.5 h-2.5 rounded-full border-2 border-white dark:border-gray-900"
                :class="isUserActive ? 'bg-green-500' : 'bg-red-500'"
              ></span>
            </div>
            <div class="hidden md:block text-left">
              <p class="text-xs font-medium text-gray-900 dark:text-white">John Doe</p>
              <p class="text-[10px] text-gray-500 dark:text-gray-400">Admin</p>
            </div>
          </button>

          <!-- User Dropdown Menu -->
          <transition
            enter-active-class="transition-all duration-200 ease-out"
            leave-active-class="transition-all duration-150 ease-in"
            enter-from-class="opacity-0 scale-95 -translate-y-2"
            enter-to-class="opacity-100 scale-100 translate-y-0"
            leave-from-class="opacity-100 scale-100 translate-y-0"
            leave-to-class="opacity-0 scale-95 -translate-y-2"
          >
            <div 
              v-if="isUserMenuOpen"
              class="absolute right-0 mt-2 w-56 bg-white dark:bg-gray-800 rounded-xl shadow-lg border border-gray-200 dark:border-gray-700 overflow-hidden"
            >
              <button class="w-full flex items-center gap-3 px-4 py-2.5 text-xs text-gray-700 dark:text-gray-200 hover:bg-gray-50 dark:hover:bg-gray-700 transition-colors">
                <font-awesome-icon icon="user" class="w-3.5 text-gray-500 dark:text-gray-400" />
                <span>Profile</span>
              </button>
              <button class="w-full flex items-center gap-3 px-4 py-2.5 text-xs text-gray-700 dark:text-gray-200 hover:bg-gray-50 dark:hover:bg-gray-700 transition-colors">
                <font-awesome-icon icon="cog" class="w-3.5 text-gray-500 dark:text-gray-400" />
                <span>Settings</span>
              </button>
              <div class="border-t border-gray-200 dark:border-gray-700"></div>
              <button class="w-full flex items-center gap-3 px-4 py-2.5 text-xs text-red-600 dark:text-red-400 hover:bg-red-50 dark:hover:bg-red-900/20 transition-colors">
                <font-awesome-icon icon="sign-out-alt" class="w-3.5" />
                <span>Logout</span>
              </button>
            </div>
          </transition>
        </div>
      </div>
    </div>
  </nav>
</template>

<script setup>
import { ref } from 'vue'

const colorMode = useColorMode()

defineProps({
  isCollapsed: {
    type: Boolean,
    default: false
  }
})

defineEmits(['toggle-sidebar', 'toggle-mobile-menu'])

const isNotificationsOpen = ref(false)
const isUserMenuOpen = ref(false)
const isUserActive = ref(true)

const notifications = ref([
  {
    id: 1,
    title: 'New user registered',
    time: '2 minutes ago',
    icon: 'user-plus',
    iconBg: 'bg-blue-100 dark:bg-blue-900/30',
    iconColor: 'text-blue-600 dark:text-blue-400',
    read: false
  },
  {
    id: 2,
    title: 'Order #1234 completed',
    time: '15 minutes ago',
    icon: 'shopping-bag',
    iconBg: 'bg-green-100 dark:bg-green-900/30',
    iconColor: 'text-green-600 dark:text-green-400',
    read: false
  },
  {
    id: 3,
    title: 'New comment received',
    time: '1 hour ago',
    icon: 'comment',
    iconBg: 'bg-purple-100 dark:bg-purple-900/30',
    iconColor: 'text-purple-600 dark:text-purple-400',
    read: true
  },
  {
    id: 4,
    title: 'Server maintenance scheduled',
    time: '2 hours ago',
    icon: 'cog',
    iconBg: 'bg-orange-100 dark:bg-orange-900/30',
    iconColor: 'text-orange-600 dark:text-orange-400',
    read: true
  }
])

const toggleTheme = () => {
  colorMode.preference = colorMode.value === 'dark' ? 'light' : 'dark'
}

const toggleNotifications = () => {
  isNotificationsOpen.value = !isNotificationsOpen.value
  if (isUserMenuOpen.value) isUserMenuOpen.value = false
}

const toggleUserMenu = () => {
  isUserMenuOpen.value = !isUserMenuOpen.value
  if (isNotificationsOpen.value) isNotificationsOpen.value = false
}
</script>

<style scoped>
@media (max-width: 768px) {
  nav {
    left: 0 !important;
  }
}
</style>
