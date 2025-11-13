<template>
  <NuxtLayout name="admin">
    <div class="space-y-8">
      <!-- Breadcrumbs -->
      <Breadcrumbs :items="[{ label: 'Pages', link: '#' }, { label: 'Form Components' }]" />
      
      <!-- Header with Gradient Background -->
      <div class="relative overflow-hidden">
        <div class="absolute -top-20 -left-20 w-72 h-72 bg-blue-400/10 dark:bg-blue-500/5 rounded-full blur-3xl"></div>
        <div class="absolute -top-20 -right-20 w-72 h-72 bg-purple-400/10 dark:bg-purple-500/5 rounded-full blur-3xl"></div>
        <div class="relative">
          <div class="inline-flex items-center gap-2 px-4 py-2 rounded-full bg-gradient-to-r from-blue-50 to-purple-50 dark:from-blue-900/30 dark:to-purple-900/30 border border-blue-200 dark:border-blue-800 mb-4">
            <font-awesome-icon icon="edit" class="text-blue-600 dark:text-blue-400 text-sm" />
            <span class="text-sm font-semibold bg-gradient-to-r from-blue-600 to-purple-600 dark:from-blue-400 dark:to-purple-400 bg-clip-text text-transparent">UI Components</span>
          </div>
          <h1 class="text-5xl font-black bg-gradient-to-r from-gray-900 via-gray-800 to-gray-600 dark:from-white dark:via-gray-200 dark:to-gray-400 bg-clip-text text-transparent mb-4 leading-tight">
            Form Components
          </h1>
          <p class="text-lg text-gray-600 dark:text-gray-400 max-w-3xl leading-relaxed">
            Beautiful, accessible form components with smooth animations, validation states, and dark mode support
          </p>
        </div>
      </div>

      <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
        <!-- Input Examples -->
        <div class="group relative bg-gradient-to-br from-white via-white to-blue-50/30 dark:from-gray-800 dark:via-gray-800 dark:to-gray-800/50 rounded-3xl shadow-lg hover:shadow-2xl p-8 border border-gray-200/60 dark:border-gray-700/60 transition-all duration-500 hover:-translate-y-1">
          <div class="absolute -inset-[1px] bg-gradient-to-r from-blue-500 via-purple-500 to-pink-500 rounded-3xl opacity-0 group-hover:opacity-20 blur-xl transition duration-500"></div>
          <div class="relative">
            <div class="flex items-center gap-4 mb-6">
              <div class="relative">
                <div class="absolute inset-0 bg-gradient-to-r from-blue-500 to-purple-600 rounded-2xl blur-md opacity-50"></div>
                <div class="relative w-14 h-14 rounded-2xl bg-gradient-to-br from-blue-500 to-purple-600 flex items-center justify-center shadow-xl">
                  <font-awesome-icon icon="keyboard" class="text-white text-xl" />
                </div>
              </div>
              <div>
                <h2 class="text-2xl font-bold text-gray-900 dark:text-white">Input Fields</h2>
                <p class="text-sm text-gray-500 dark:text-gray-400">Text input with icons & validation</p>
              </div>
            </div>
          
          <div class="space-y-4">
            <BaseInput
              v-model="formData.name"
              label="Full Name"
              placeholder="Enter your name"
              required
              hint="Please enter your full name"
            />

            <BaseInput
              v-model="formData.email"
              type="email"
              label="Email Address"
              placeholder="you@example.com"
              prefix-icon="envelope"
              :error="emailError"
            />

            <BaseInput
              v-model="formData.password"
              type="password"
              label="Password"
              placeholder="Enter password"
              suffix-icon="lock"
              required
            />

            <BaseInput
              v-model="formData.phone"
              type="tel"
              label="Phone Number"
              placeholder="+1 (555) 000-0000"
              prefix-icon="phone"
            />

            <BaseInput
              v-model="formData.age"
              type="number"
              label="Age"
              placeholder="18"
              :min="1"
              :max="120"
            />

            <BaseInput
              v-model="formData.website"
              type="url"
              label="Website"
              placeholder="https://example.com"
              prefix-icon="globe"
            />

            <BaseInput
              v-model="formData.disabledField"
              label="Disabled Input"
              placeholder="This is disabled"
              disabled
            />
          </div>
          </div>
        </div>

        <!-- Select Examples -->
        <div class="group relative bg-gradient-to-br from-white via-white to-purple-50/30 dark:from-gray-800 dark:via-gray-800 dark:to-gray-800/50 rounded-3xl shadow-lg hover:shadow-2xl p-8 border border-gray-200/60 dark:border-gray-700/60 transition-all duration-500 hover:-translate-y-1">
          <div class="absolute -inset-[1px] bg-gradient-to-r from-purple-500 via-pink-500 to-rose-500 rounded-3xl opacity-0 group-hover:opacity-20 blur-xl transition duration-500"></div>
          <div class="relative">
            <div class="flex items-center gap-4 mb-6">
              <div class="relative">
                <div class="absolute inset-0 bg-gradient-to-r from-purple-500 to-pink-600 rounded-2xl blur-md opacity-50"></div>
                <div class="relative w-14 h-14 rounded-2xl bg-gradient-to-br from-purple-500 to-pink-600 flex items-center justify-center shadow-xl">
                  <font-awesome-icon icon="list" class="text-white text-xl" />
                </div>
              </div>
              <div>
                <h2 class="text-2xl font-bold text-gray-900 dark:text-white">Select Dropdown</h2>
                <p class="text-sm text-gray-500 dark:text-gray-400">Dropdown selection with options</p>
              </div>
            </div>
          
          <div class="space-y-4">
            <BaseSelect
              v-model="formData.country"
              label="Country"
              :options="countries"
              placeholder="Select your country"
              required
              hint="Choose your country of residence"
            />

            <BaseSelect
              v-model="formData.role"
              label="User Role"
              :options="roles"
              placeholder="Select a role"
            />

            <BaseSelect
              v-model="formData.status"
              label="Status"
              :options="statusOptions"
              :error="statusError"
            />
          </div>
          </div>
        </div>

        <!-- Textarea Example -->
        <div class="group relative bg-gradient-to-br from-white via-white to-green-50/30 dark:from-gray-800 dark:via-gray-800 dark:to-gray-800/50 rounded-3xl shadow-lg hover:shadow-2xl p-8 border border-gray-200/60 dark:border-gray-700/60 transition-all duration-500 hover:-translate-y-1">
          <div class="absolute -inset-[1px] bg-gradient-to-r from-green-500 via-emerald-500 to-teal-500 rounded-3xl opacity-0 group-hover:opacity-20 blur-xl transition duration-500"></div>
          <div class="relative">
            <div class="flex items-center gap-4 mb-6">
              <div class="relative">
                <div class="absolute inset-0 bg-gradient-to-r from-green-500 to-emerald-600 rounded-2xl blur-md opacity-50"></div>
                <div class="relative w-14 h-14 rounded-2xl bg-gradient-to-br from-green-500 to-emerald-600 flex items-center justify-center shadow-xl">
                  <font-awesome-icon icon="align-left" class="text-white text-xl" />
                </div>
              </div>
              <div>
                <h2 class="text-2xl font-bold text-gray-900 dark:text-white">Text Area</h2>
                <p class="text-sm text-gray-500 dark:text-gray-400">Multi-line text with counter</p>
              </div>
            </div>
          
          <div class="space-y-4">
            <BaseTextarea
              v-model="formData.bio"
              label="Biography"
              placeholder="Tell us about yourself..."
              :rows="4"
              hint="Write a brief description"
            />

            <BaseTextarea
              v-model="formData.message"
              label="Message"
              placeholder="Your message here..."
              :rows="3"
              :maxlength="200"
              show-count
              hint="Maximum 200 characters"
            />

            <BaseTextarea
              v-model="formData.notes"
              label="Notes"
              placeholder="Additional notes..."
              :rows="3"
              :resizable="false"
            />
          </div>
          </div>
        </div>

        <!-- Checkbox & Radio Examples -->
        <div class="group relative bg-gradient-to-br from-white via-white to-orange-50/30 dark:from-gray-800 dark:via-gray-800 dark:to-gray-800/50 rounded-3xl shadow-lg hover:shadow-2xl p-8 border border-gray-200/60 dark:border-gray-700/60 transition-all duration-500 hover:-translate-y-1">
          <div class="absolute -inset-[1px] bg-gradient-to-r from-orange-500 via-red-500 to-pink-500 rounded-3xl opacity-0 group-hover:opacity-20 blur-xl transition duration-500"></div>
          <div class="relative">
            <div class="flex items-center gap-4 mb-6">
              <div class="relative">
                <div class="absolute inset-0 bg-gradient-to-r from-orange-500 to-red-600 rounded-2xl blur-md opacity-50"></div>
                <div class="relative w-14 h-14 rounded-2xl bg-gradient-to-br from-orange-500 to-red-600 flex items-center justify-center shadow-xl">
                  <font-awesome-icon icon="check-square" class="text-white text-xl" />
                </div>
              </div>
              <div>
                <h2 class="text-2xl font-bold text-gray-900 dark:text-white">Checkbox & Radio</h2>
                <p class="text-sm text-gray-500 dark:text-gray-400">Toggle and selection controls</p>
              </div>
            </div>
          
          <div class="space-y-6">
            <!-- Checkboxes -->
            <div>
              <p class="text-sm font-medium text-gray-700 dark:text-gray-300 mb-3">Interests (Checkboxes)</p>
              <div class="space-y-2">
                <BaseCheckbox
                  v-model="formData.interests.coding"
                  label="Coding"
                  hint="I enjoy programming"
                />
                <BaseCheckbox
                  v-model="formData.interests.design"
                  label="Design"
                />
                <BaseCheckbox
                  v-model="formData.interests.music"
                  label="Music"
                />
                <BaseCheckbox
                  v-model="formData.newsletter"
                  label="Subscribe to newsletter"
                  required
                />
              </div>
            </div>

            <!-- Radio Buttons -->
            <div>
              <p class="text-sm font-medium text-gray-700 dark:text-gray-300 mb-3">Gender (Radio)</p>
              <div class="space-y-2">
                <BaseRadio
                  v-model="formData.gender"
                  name="gender"
                  value="male"
                  label="Male"
                />
                <BaseRadio
                  v-model="formData.gender"
                  name="gender"
                  value="female"
                  label="Female"
                />
                <BaseRadio
                  v-model="formData.gender"
                  name="gender"
                  value="other"
                  label="Other"
                />
              </div>
            </div>

            <!-- Another Radio Group -->
            <div>
              <p class="text-sm font-medium text-gray-700 dark:text-gray-300 mb-3">Plan (Radio)</p>
              <div class="space-y-2">
                <BaseRadio
                  v-model="formData.plan"
                  name="plan"
                  value="free"
                  label="Free"
                  hint="Basic features"
                />
                <BaseRadio
                  v-model="formData.plan"
                  name="plan"
                  value="pro"
                  label="Pro"
                  hint="Advanced features"
                />
                <BaseRadio
                  v-model="formData.plan"
                  name="plan"
                  value="enterprise"
                  label="Enterprise"
                  hint="Full features"
                />
              </div>
            </div>
          </div>
          </div>
        </div>

        <!-- Button Examples -->
        <div class="group relative bg-gradient-to-br from-white via-white to-indigo-50/30 dark:from-gray-800 dark:via-gray-800 dark:to-gray-800/50 rounded-3xl shadow-lg hover:shadow-2xl p-8 border border-gray-200/60 dark:border-gray-700/60 transition-all duration-500 hover:-translate-y-1 lg:col-span-2">
          <div class="absolute -inset-[1px] bg-gradient-to-r from-indigo-500 via-purple-500 to-pink-500 rounded-3xl opacity-0 group-hover:opacity-20 blur-xl transition duration-500"></div>
          <div class="relative">
            <div class="flex items-center gap-4 mb-8">
              <div class="relative">
                <div class="absolute inset-0 bg-gradient-to-r from-indigo-500 to-purple-600 rounded-2xl blur-md opacity-50"></div>
                <div class="relative w-14 h-14 rounded-2xl bg-gradient-to-br from-indigo-500 to-purple-600 flex items-center justify-center shadow-xl">
                  <font-awesome-icon icon="mouse-pointer" class="text-white text-xl" />
                </div>
              </div>
              <div>
                <h2 class="text-2xl font-bold text-gray-900 dark:text-white">Button Components</h2>
                <p class="text-sm text-gray-500 dark:text-gray-400">Interactive buttons with multiple variants</p>
              </div>
            </div>
          
          <div class="space-y-8">
            <!-- Variants -->
            <div>
              <div class="flex items-center gap-2 mb-4">
                <div class="w-1.5 h-1.5 rounded-full bg-gradient-to-r from-blue-500 to-purple-500"></div>
                <p class="text-sm font-semibold text-gray-700 dark:text-gray-300">Button Variants</p>
              </div>
              <div class="flex flex-wrap gap-3">
                <BaseButton variant="primary" label="Primary" />
                <BaseButton variant="secondary" label="Secondary" />
                <BaseButton variant="success" label="Success" />
                <BaseButton variant="danger" label="Danger" />
                <BaseButton variant="warning" label="Warning" />
                <BaseButton variant="info" label="Info" />
                <BaseButton variant="outline" label="Outline" />
                <BaseButton variant="ghost" label="Ghost" />
                <BaseButton variant="link" label="Link" />
              </div>
            </div>

            <!-- Sizes -->
            <div>
              <div class="flex items-center gap-2 mb-4">
                <div class="w-1.5 h-1.5 rounded-full bg-gradient-to-r from-green-500 to-emerald-500"></div>
                <p class="text-sm font-semibold text-gray-700 dark:text-gray-300">Button Sizes</p>
              </div>
              <div class="flex flex-wrap items-center gap-3">
                <BaseButton size="xs" label="Extra Small" />
                <BaseButton size="sm" label="Small" />
                <BaseButton size="md" label="Medium" />
                <BaseButton size="lg" label="Large" />
                <BaseButton size="xl" label="Extra Large" />
              </div>
            </div>

            <!-- With Icons -->
            <div>
              <div class="flex items-center gap-2 mb-4">
                <div class="w-1.5 h-1.5 rounded-full bg-gradient-to-r from-purple-500 to-pink-500"></div>
                <p class="text-sm font-semibold text-gray-700 dark:text-gray-300">Buttons with Icons</p>
              </div>
              <div class="flex flex-wrap gap-3">
                <BaseButton variant="primary" label="Save" prefix-icon="save" />
                <BaseButton variant="secondary" label="Download" prefix-icon="download" />
                <BaseButton variant="success" label="Next" suffix-icon="arrow-right" />
                <BaseButton variant="danger" label="Delete" prefix-icon="trash" />
                <BaseButton variant="info" label="Settings" prefix-icon="cog" />
              </div>
            </div>

            <!-- States -->
            <div>
              <div class="flex items-center gap-2 mb-4">
                <div class="w-1.5 h-1.5 rounded-full bg-gradient-to-r from-orange-500 to-red-500"></div>
                <p class="text-sm font-semibold text-gray-700 dark:text-gray-300">Button States</p>
              </div>
              <div class="flex flex-wrap gap-3">
                <BaseButton variant="primary" label="Normal" />
                <BaseButton variant="primary" label="Loading" :loading="true" />
                <BaseButton variant="primary" label="Disabled" :disabled="true" />
              </div>
            </div>

            <!-- Block Button -->
            <div>
              <div class="flex items-center gap-2 mb-4">
                <div class="w-1.5 h-1.5 rounded-full bg-gradient-to-r from-cyan-500 to-blue-500"></div>
                <p class="text-sm font-semibold text-gray-700 dark:text-gray-300">Block Button</p>
              </div>
              <BaseButton variant="primary" label="Full Width Button" :block="true" />
            </div>

            <!-- Form Actions -->
            <div>
              <div class="flex items-center gap-2 mb-4">
                <div class="w-1.5 h-1.5 rounded-full bg-gradient-to-r from-pink-500 to-rose-500"></div>
                <p class="text-sm font-semibold text-gray-700 dark:text-gray-300">Form Actions</p>
              </div>
              <div class="flex flex-wrap gap-3">
                <BaseButton 
                  type="submit" 
                  variant="primary" 
                  label="Submit Form" 
                  @click="handleSubmit"
                  :loading="isSubmitting"
                />
                <BaseButton 
                  type="reset" 
                  variant="outline" 
                  label="Reset" 
                  @click="handleReset"
                />
                <BaseButton 
                  variant="ghost" 
                  label="Cancel" 
                  @click="handleCancel"
                />
              </div>
            </div>
          </div>
          </div>
        </div>

        <!-- Form Preview -->
        <div class="group relative bg-gradient-to-br from-gray-900 to-gray-800 dark:from-gray-900 dark:to-black rounded-3xl shadow-2xl p-8 border border-gray-700/50 dark:border-gray-600/50 transition-all duration-500 hover:-translate-y-1 lg:col-span-2">
          <div class="absolute -inset-[1px] bg-gradient-to-r from-cyan-500 via-blue-500 to-purple-500 rounded-3xl opacity-20 group-hover:opacity-30 blur-xl transition duration-500"></div>
          <div class="relative">
            <div class="flex items-center gap-4 mb-6">
              <div class="relative">
                <div class="absolute inset-0 bg-gradient-to-r from-cyan-400 to-blue-500 rounded-2xl blur-md opacity-60"></div>
                <div class="relative w-14 h-14 rounded-2xl bg-gradient-to-br from-cyan-400 to-blue-500 flex items-center justify-center shadow-xl">
                  <font-awesome-icon icon="code" class="text-white text-xl" />
                </div>
              </div>
              <div>
                <h2 class="text-2xl font-bold text-white">Form Data Preview</h2>
                <p class="text-sm text-gray-400">Live JSON output</p>
              </div>
            </div>
            <pre class="bg-black/40 backdrop-blur-sm p-6 rounded-2xl text-xs overflow-auto max-h-96 border border-gray-700/50 text-green-400 font-mono shadow-inner">{{ formData }}</pre>
          </div>
        </div>
      </div>
    </div>
  </NuxtLayout>
</template>

<script setup>
import { ref, computed } from 'vue'

definePageMeta({
  layout: false
})

const isSubmitting = ref(false)

const formData = ref({
  name: '',
  email: '',
  password: '',
  phone: '',
  age: '',
  website: '',
  disabledField: 'Cannot edit this',
  country: '',
  role: '',
  status: '',
  bio: '',
  message: '',
  notes: '',
  interests: {
    coding: false,
    design: false,
    music: false
  },
  newsletter: false,
  gender: 'male',
  plan: 'free'
})

const countries = [
  { label: 'United States', value: 'us' },
  { label: 'Canada', value: 'ca' },
  { label: 'United Kingdom', value: 'uk' },
  { label: 'Australia', value: 'au' },
  { label: 'Germany', value: 'de' },
  { label: 'France', value: 'fr' },
  { label: 'Japan', value: 'jp' }
]

const roles = [
  { label: 'Administrator', value: 'admin' },
  { label: 'Editor', value: 'editor' },
  { label: 'Author', value: 'author' },
  { label: 'Contributor', value: 'contributor' },
  { label: 'Subscriber', value: 'subscriber' }
]

const statusOptions = [
  { label: 'Active', value: 'active' },
  { label: 'Inactive', value: 'inactive' },
  { label: 'Pending', value: 'pending', disabled: true },
  { label: 'Suspended', value: 'suspended' }
]

const emailError = computed(() => {
  if (formData.value.email && !formData.value.email.includes('@')) {
    return 'Please enter a valid email address'
  }
  return ''
})

const statusError = computed(() => {
  if (!formData.value.status) {
    return 'Status is required'
  }
  return ''
})

const handleSubmit = () => {
  isSubmitting.value = true
  console.log('Form submitted:', formData.value)
  
  setTimeout(() => {
    isSubmitting.value = false
    alert('Form submitted successfully!')
  }, 2000)
}

const handleReset = () => {
  formData.value = {
    name: '',
    email: '',
    password: '',
    phone: '',
    age: '',
    website: '',
    disabledField: 'Cannot edit this',
    country: '',
    role: '',
    status: '',
    bio: '',
    message: '',
    notes: '',
    interests: {
      coding: false,
      design: false,
      music: false
    },
    newsletter: false,
    gender: 'male',
    plan: 'free'
  }
}

const handleCancel = () => {
  console.log('Form cancelled')
}
</script>
