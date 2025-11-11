<template>
  <div class="min-h-screen bg-gray-50 dark:bg-gray-900 transition-colors duration-300">
    <!-- Mobile Overlay -->
    <div 
      v-if="isMobileMenuOpen"
      @click="closeMobileMenu"
      class="fixed inset-0 bg-black/50 z-[90] md:hidden transition-opacity"
    ></div>
    
    <Sidebar 
      :isCollapsed="isSidebarCollapsed" 
      :isMobileMenuOpen="isMobileMenuOpen"
      @close-mobile-menu="closeMobileMenu"
    />
    <div 
      class="transition-all duration-300 flex flex-col min-h-screen ml-0 md:ml-[250px]"
      :class="{ 'md:ml-[70px]': isSidebarCollapsed }"
    >
      <Navbar 
        :isCollapsed="isSidebarCollapsed" 
        @toggle-sidebar="toggleSidebar" 
        @toggle-mobile-menu="toggleMobileMenu"
      />
      <main class="pt-20 p-4 md:p-6 flex-1">
        <slot />
      </main>
      <Footer />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const isSidebarCollapsed = ref(false)
const isMobileMenuOpen = ref(false)

const toggleSidebar = () => {
  isSidebarCollapsed.value = !isSidebarCollapsed.value
}

const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value
}

const closeMobileMenu = () => {
  isMobileMenuOpen.value = false
}
</script>

<style scoped>
@media (max-width: 768px) {
  .ml-\[250px\],
  .ml-\[70px\] {
    margin-left: 0 !important;
  }
}
</style>
