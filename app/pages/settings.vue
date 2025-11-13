<template>
  <NuxtLayout name="admin">
    <div class="space-y-6">
      <!-- Breadcrumbs -->
      <Breadcrumbs :items="[{ label: 'Settings' }]" />
      
      <!-- Header -->
      <div>
        <h1 class="text-3xl font-bold text-gray-900 dark:text-white mb-2">Settings</h1>
        <p class="text-gray-600 dark:text-gray-400">Manage your account settings and preferences.</p>
      </div>

      <!-- Settings Cards -->
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
        <!-- Profile Settings -->
        <div class="rounded-2xl bg-white dark:bg-gray-800 shadow-sm border border-gray-200 dark:border-gray-700 p-6">
          <div class="flex items-center gap-3 mb-4">
            <div class="w-10 h-10 rounded-lg bg-gray-100 dark:bg-gray-700 flex items-center justify-center">
              <font-awesome-icon icon="user" class="text-gray-700 dark:text-gray-300" />
            </div>
            <h2 class="text-lg font-semibold text-gray-900 dark:text-white">Profile Settings</h2>
          </div>
          <p class="text-sm text-gray-600 dark:text-gray-400 mb-4">
            Update your profile information and personal details.
          </p>
          <button class="px-4 py-2 rounded-lg bg-gray-900 dark:bg-gray-700 text-white text-sm font-medium hover:bg-gray-800 dark:hover:bg-gray-600 transition-colors">
            Edit Profile
          </button>
        </div>

        <!-- Security Settings -->
        <div class="rounded-2xl bg-white dark:bg-gray-800 shadow-sm border border-gray-200 dark:border-gray-700 p-6">
          <div class="flex items-center gap-3 mb-4">
            <div class="w-10 h-10 rounded-lg bg-gray-100 dark:bg-gray-700 flex items-center justify-center">
              <font-awesome-icon icon="cog" class="text-gray-700 dark:text-gray-300" />
            </div>
            <h2 class="text-lg font-semibold text-gray-900 dark:text-white">Security</h2>
          </div>
          <p class="text-sm text-gray-600 dark:text-gray-400 mb-4">
            Manage your password and security preferences.
          </p>
          <button class="px-4 py-2 rounded-lg bg-gray-900 dark:bg-gray-700 text-white text-sm font-medium hover:bg-gray-800 dark:hover:bg-gray-600 transition-colors">
            Change Password
          </button>
        </div>
      </div>
    </div>
  </NuxtLayout>
</template>

<script setup>
definePageMeta({
  layout: false
})

useHead({
  title: 'Settings - Admin Panel',
  meta: [
    { name: 'description', content: 'Manage your account settings and preferences. Update profile information, security settings, and personal details.' },
    { name: 'keywords', content: 'settings, account, profile, security, preferences' },
    { property: 'og:title', content: 'Settings - Admin Panel' },
    { property: 'og:description', content: 'Manage your account settings and preferences.' },
    { property: 'og:type', content: 'website' }
  ]
})
</script>
