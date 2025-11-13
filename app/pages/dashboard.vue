
<script setup>
// import { useRoute } from 'vue-router';
// definePageMeta({
//   layout: false
// // })
// const route = useRoute()
// console.log(route.query.id)
</script>
<template>
  <NuxtLayout name="admin">
    <div class="space-y-6">
      <!-- Breadcrumbs -->
      <Breadcrumbs :items="[{ label: 'Dashboard' }]" />
      
      <!-- Header -->
      <div>
        <h1 class="text-3xl font-bold text-gray-900 dark:text-white mb-2">Dashboard</h1>
        <p class="text-gray-600 dark:text-gray-400">Welcome back! Here's what's happening today.</p>
      </div>

      <!-- Stats Grid -->
      <div class="grid grid-cols-1 sm:grid-cols-2 xl:grid-cols-4 gap-6">
        <!-- Total Users -->
        <div class="group relative overflow-hidden rounded-2xl bg-white dark:bg-gray-800 p-6 shadow-sm hover:shadow-md transition-all duration-300 border border-gray-200 dark:border-gray-700">
          <div class="flex items-center justify-between">
            <div>
              <p class="text-sm font-medium text-gray-600 dark:text-gray-400 mb-1">Total Users</p>
              <h3 class="text-3xl font-bold text-gray-900 dark:text-white">1,234</h3>
              <p class="text-sm text-green-600 dark:text-green-400 mt-2">↗ +12% from last month</p>
            </div>
            <div class="w-14 h-14 rounded-xl bg-gray-100 dark:bg-gray-700 flex items-center justify-center">
              <font-awesome-icon icon="users" class="text-gray-700 dark:text-gray-300 text-xl" />
            </div>
          </div>
        </div>

        <!-- Revenue -->
        <div class="group relative overflow-hidden rounded-2xl bg-white dark:bg-gray-800 p-6 shadow-sm hover:shadow-md transition-all duration-300 border border-gray-200 dark:border-gray-700">
          <div class="flex items-center justify-between">
            <div>
              <p class="text-sm font-medium text-gray-600 dark:text-gray-400 mb-1">Revenue</p>
              <h3 class="text-3xl font-bold text-gray-900 dark:text-white">$12,345</h3>
              <p class="text-sm text-green-600 dark:text-green-400 mt-2">↗ +8% from last month</p>
            </div>
            <div class="w-14 h-14 rounded-xl bg-gray-100 dark:bg-gray-700 flex items-center justify-center">
              <font-awesome-icon icon="chart-line" class="text-gray-700 dark:text-gray-300 text-xl" />
            </div>
          </div>
        </div>

        <!-- Orders -->
        <div class="group relative overflow-hidden rounded-2xl bg-white dark:bg-gray-800 p-6 shadow-sm hover:shadow-md transition-all duration-300 border border-gray-200 dark:border-gray-700">
          <div class="flex items-center justify-between">
            <div>
              <p class="text-sm font-medium text-gray-600 dark:text-gray-400 mb-1">Orders</p>
              <h3 class="text-3xl font-bold text-gray-900 dark:text-white">567</h3>
              <p class="text-sm text-green-600 dark:text-green-400 mt-2">↗ +23% from last month</p>
            </div>
            <div class="w-14 h-14 rounded-xl bg-gray-100 dark:bg-gray-700 flex items-center justify-center">
              <font-awesome-icon icon="shopping-cart" class="text-gray-700 dark:text-gray-300 text-xl" />
            </div>
          </div>
        </div>

        <!-- Rating -->
        <div class="group relative overflow-hidden rounded-2xl bg-white dark:bg-gray-800 p-6 shadow-sm hover:shadow-md transition-all duration-300 border border-gray-200 dark:border-gray-700">
          <div class="flex items-center justify-between">
            <div>
              <p class="text-sm font-medium text-gray-600 dark:text-gray-400 mb-1">Rating</p>
              <h3 class="text-3xl font-bold text-gray-900 dark:text-white">4.8</h3>
              <p class="text-sm text-green-600 dark:text-green-400 mt-2">↗ +0.3 from last month</p>
            </div>
            <div class="w-14 h-14 rounded-xl bg-gray-100 dark:bg-gray-700 flex items-center justify-center">
              <font-awesome-icon icon="star" class="text-gray-700 dark:text-gray-300 text-xl" />
            </div>
          </div>
        </div>
      </div>

      <!-- Content Grid -->
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
        <!-- Recent Activity -->
        <div class="rounded-2xl bg-white dark:bg-gray-800 shadow-sm border border-gray-200 dark:border-gray-700 overflow-hidden">
          <div class="px-6 py-4 border-b border-gray-200 dark:border-gray-700">
            <h2 class="text-lg font-semibold text-gray-900 dark:text-white">Recent Activity</h2>
          </div>
          <div class="p-6 space-y-4">
            <div class="flex items-start gap-4 p-3 rounded-xl hover:bg-gray-50 dark:hover:bg-gray-700/50 transition-colors">
              <div class="w-10 h-10 rounded-lg bg-gray-100 dark:bg-gray-700 flex items-center justify-center flex-shrink-0">
                <font-awesome-icon icon="user-plus" class="text-gray-700 dark:text-gray-300" />
              </div>
              <div class="flex-1 min-w-0">
                <p class="text-sm font-medium text-gray-900 dark:text-white">New user registered</p>
                <p class="text-xs text-gray-500 dark:text-gray-400 mt-1">2 minutes ago</p>
              </div>
            </div>
            
            <div class="flex items-start gap-4 p-3 rounded-xl hover:bg-gray-50 dark:hover:bg-gray-700/50 transition-colors">
              <div class="w-10 h-10 rounded-lg bg-gray-100 dark:bg-gray-700 flex items-center justify-center flex-shrink-0">
                <font-awesome-icon icon="shopping-bag" class="text-gray-700 dark:text-gray-300" />
              </div>
              <div class="flex-1 min-w-0">
                <p class="text-sm font-medium text-gray-900 dark:text-white">Order #1234 completed</p>
                <p class="text-xs text-gray-500 dark:text-gray-400 mt-1">15 minutes ago</p>
              </div>
            </div>
            
            <div class="flex items-start gap-4 p-3 rounded-xl hover:bg-gray-50 dark:hover:bg-gray-700/50 transition-colors">
              <div class="w-10 h-10 rounded-lg bg-gray-100 dark:bg-gray-700 flex items-center justify-center flex-shrink-0">
                <font-awesome-icon icon="comment" class="text-gray-700 dark:text-gray-300" />
              </div>
              <div class="flex-1 min-w-0">
                <p class="text-sm font-medium text-gray-900 dark:text-white">New comment received</p>
                <p class="text-xs text-gray-500 dark:text-gray-400 mt-1">1 hour ago</p>
              </div>
            </div>
          </div>
        </div>

        <!-- Quick Actions -->
        <div class="rounded-2xl bg-white dark:bg-gray-800 shadow-sm border border-gray-200 dark:border-gray-700 overflow-hidden">
          <div class="px-6 py-4 border-b border-gray-200 dark:border-gray-700">
            <h2 class="text-lg font-semibold text-gray-900 dark:text-white">Quick Actions</h2>
          </div>
          <div class="p-6 space-y-3">
            <button class="w-full flex items-center justify-center gap-3 px-6 py-4 rounded-xl bg-gray-900 dark:bg-gray-700 hover:bg-gray-800 dark:hover:bg-gray-600 text-white font-medium shadow-sm hover:shadow-md transition-all duration-300">
              <font-awesome-icon icon="plus" />
              <span>Add New Item</span>
            </button>
            
            <button class="w-full flex items-center justify-center gap-3 px-6 py-4 rounded-xl bg-gray-100 dark:bg-gray-700 hover:bg-gray-200 dark:hover:bg-gray-600 text-gray-700 dark:text-gray-200 font-medium transition-all duration-300">
              <font-awesome-icon icon="download" />
              <span>Export Data</span>
            </button>
            
            <button class="w-full flex items-center justify-center gap-3 px-6 py-4 rounded-xl bg-gray-100 dark:bg-gray-700 hover:bg-gray-200 dark:hover:bg-gray-600 text-gray-700 dark:text-gray-200 font-medium transition-all duration-300">
              <font-awesome-icon icon="cog" />
              <span>Settings</span>
            </button>
          </div>
        </div>
      </div>
    </div>
  </NuxtLayout>
</template>

