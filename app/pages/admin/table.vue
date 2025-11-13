<script setup>
definePageMeta({
  layout: false
})
import { ref } from 'vue'

// Sample data
const users = ref([
  { id: 1, name: 'John Doe', email: 'john@example.com', role: 'Admin', status: 'Active' },
  { id: 2, name: 'Jane Smith', email: 'jane@example.com', role: 'Editor', status: 'Active' },
  { id: 3, name: 'Bob Johnson', email: 'bob@example.com', role: 'User', status: 'Inactive' },
  { id: 4, name: 'Alice Williams', email: 'alice@example.com', role: 'Editor', status: 'Active' },
  { id: 5, name: 'Charlie Brown', email: 'charlie@example.com', role: 'User', status: 'Pending' },
  { id: 6, name: 'Diana Prince', email: 'diana@example.com', role: 'Admin', status: 'Active' },
  { id: 7, name: 'Ethan Hunt', email: 'ethan@example.com', role: 'User', status: 'Active' },
  { id: 8, name: 'Fiona Green', email: 'fiona@example.com', role: 'Editor', status: 'Inactive' },
  { id: 9, name: 'George Miller', email: 'george@example.com', role: 'User', status: 'Active' },
  { id: 10, name: 'Hannah Lee', email: 'hannah@example.com', role: 'Editor', status: 'Active' },
  { id: 11, name: 'Ian Malcolm', email: 'ian@example.com', role: 'User', status: 'Pending' },
  { id: 12, name: 'Julia Roberts', email: 'julia@example.com', role: 'Admin', status: 'Active' }
])

// Add actions to users
users.value.forEach(user => {
  user.actions = { view: true, edit: true, delete: true }
})

// Modal states
const showDeleteModal = ref(false)
const showEditModal = ref(false)
const showViewModal = ref(false)
const selectedUser = ref(null)
const showAddUserModal = ref(false);

const handleView = (user) => {
  // selectedUser.value = user
  // showViewModal.value = true
  navigateTo('/dashboard?id=1')
}

const handleEdit = (user) => {
  selectedUser.value = user
  showEditModal.value = true
}

const handleDelete = (user) => {
  selectedUser.value = user
  showDeleteModal.value = true
}

const confirmDelete = () => {
  console.log('Deleting user:', selectedUser.value)
  showDeleteModal.value = false
  selectedUser.value = null
}
const handleAddUser = () => {
//   console.log('Add User button clicked')
    showAddUserModal.value = true;
}
</script>

<template>
  <NuxtLayout name="admin">
    <div class="space-y-8">
      <Breadcrumbs :items="[{ label: 'Pages', link: '#' }, { label: 'Custom Table' }]" />
      
      <BaseCard title="Slot-Based Table (Fully Customizable)">
        <template #header>
          <div class="flex justify-between items-center mb-5">
            <h2 class="text-2xl font-bold text-gray-900 dark:text-white">Slot-Based Table (Fully Customizable)</h2>
            <BaseButton @click="handleAddUser" variant="primary" class="flex items-center gap-2">
              <font-awesome-icon icon="plus" class="text-sm" />
              Add User
            </BaseButton>
          </div>
        </template>
        
        <BaseTableSlot
          :data="users"
          search-placeholder="Search users..."
        >
          <template #thead>
            <BaseThead>
              <tr>
                <BaseTh>ID</BaseTh>
                <BaseTh>Name</BaseTh>
                <BaseTh>Email</BaseTh>
                <BaseTh>Role</BaseTh>
                <BaseTh>Status</BaseTh>
                <BaseTh>Actions</BaseTh>
              </tr>
            </BaseThead>
          </template>
          
          <template #tbody="{ paginatedData }">
            <BaseTbody>
              <tr v-if="!paginatedData || paginatedData.length === 0">
                <td colspan="6" class="px-6 py-12 text-center">
                  <div class="flex flex-col items-center gap-3 text-gray-500 dark:text-gray-400">
                    <font-awesome-icon icon="inbox" class="text-4xl opacity-50" />
                    <p class="text-sm font-medium">No users found</p>
                    <p class="text-xs">Try adjusting your search criteria</p>
                  </div>
                </td>
              </tr>
              
              <!-- Data Rows -->
              <BaseTr v-for="user in paginatedData" :key="user.id">
                <BaseTd>{{ user.id }}</BaseTd>
                <BaseTd>
                  <div class="font-medium">{{ user.name }}</div>
                </BaseTd>
                <BaseTd>{{ user.email }}</BaseTd>
                <BaseTd>
                  <div class="flex items-center gap-2">
                    <font-awesome-icon 
                      :icon="user.role === 'Admin' ? 'crown' : user.role === 'Editor' ? 'pen' : 'user'" 
                      class="text-xs text-gray-400"
                    />
                    <span>{{ user.role }}</span>
                  </div>
                </BaseTd>
                <BaseTd>
                  <span
                    class="inline-flex items-center px-2.5 py-1 rounded-full text-xs font-medium"
                    :class="{
                      'bg-green-100 text-green-800 dark:bg-green-900/30 dark:text-green-400': user.status === 'Active',
                      'bg-gray-100 text-gray-800 dark:bg-gray-700 dark:text-gray-400': user.status === 'Inactive',
                      'bg-yellow-100 text-yellow-800 dark:bg-yellow-900/30 dark:text-yellow-400': user.status === 'Pending'
                    }"
                  >
                    {{ user.status }}
                  </span>
                </BaseTd>
                <BaseTd>
                  <div class="flex gap-2">
                    <button
                      v-if="user.actions.view"
                      @click="handleView(user)"
                      class="p-1.5 rounded-lg hover:bg-blue-50 dark:hover:bg-blue-900/20 text-blue-600 dark:text-blue-400 transition-colors"
                      title="View"
                    >
                      <font-awesome-icon icon="eye" class="text-sm" />
                    </button>
                    <button
                      v-if="user.actions.edit"
                      @click="handleEdit(user)"
                      class="p-1.5 rounded-lg hover:bg-green-50 dark:hover:bg-green-900/20 text-green-600 dark:text-green-400 transition-colors"
                      title="Edit"
                    >
                      <font-awesome-icon icon="edit" class="text-sm" />
                    </button>
                    <button
                      v-if="user.actions.delete"
                      @click="handleDelete(user)"
                      class="p-1.5 rounded-lg hover:bg-red-50 dark:hover:bg-red-900/20 text-red-600 dark:text-red-400 transition-colors"
                      title="Delete"
                    >
                      <font-awesome-icon icon="trash" class="text-sm" />
                    </button>
                  </div>
                </BaseTd>
              </BaseTr>
            </BaseTbody>
          </template>
        </BaseTableSlot>
      </BaseCard>

      <!-- Delete Confirmation Modal -->
      <BaseModal v-model="showAddUserModal" size="lg">
        <ModalHeader 
          title="Add User" 
          subtitle="Fill in the details below to add a new user"
          @close="showAddUserModal = false"
        />
        <ModalBody>
          <p class="text-gray-600 dark:text-gray-400">
              Add User Here...
          </p>
        </ModalBody>
        <ModalFooter>
          <BaseButton variant="ghost" label="Cancel" @click="showAddUserModal = false" />
          <BaseButton type="submit" variant="primary" label="Add User" prefix-icon="check"/>
        </ModalFooter>
      </BaseModal>

      <!-- Delete Confirmation Modal -->
      <BaseModal v-model="showDeleteModal" size="sm">
        <ModalHeader 
          title="Delete User?" 
          subtitle="This action cannot be undone"
          @close="showDeleteModal = false"
        />
        <ModalBody>
          <p class="text-gray-600 dark:text-gray-400">
            Are you sure you want to delete <strong>{{ selectedUser?.name }}</strong>? 
            This action is permanent and cannot be reversed.
          </p>
        </ModalBody>
        <ModalFooter>
          <BaseButton variant="ghost" label="Cancel" @click="showDeleteModal = false" />
          <BaseButton variant="danger" label="Delete" prefix-icon="trash" @click="confirmDelete" />
        </ModalFooter>
      </BaseModal>

      <!-- Edit User Modal -->
      <BaseModal v-model="showEditModal" size="md">
        <ModalHeader 
          title="Edit User" 
          :subtitle="`Update information for ${selectedUser?.name}`"
          @close="showEditModal = false"
        />
        <ModalBody>
          <div class="space-y-4">
            <BaseInput 
              :model-value="selectedUser?.name" 
              label="Name" 
              placeholder="Enter name"
            />
            <BaseInput 
              :model-value="selectedUser?.email" 
              type="email"
              label="Email" 
              placeholder="Enter email"
            />
            <BaseSelect
              :model-value="selectedUser?.role"
              label="Role"
              :options="[
                { label: 'Admin', value: 'Admin' },
                { label: 'Editor', value: 'Editor' },
                { label: 'User', value: 'User' }
              ]"
            />
          </div>
        </ModalBody>
        <ModalFooter>
          <BaseButton variant="ghost" label="Cancel" @click="showEditModal = false" />
          <BaseButton variant="primary" label="Save Changes" @click="showEditModal = false" />
        </ModalFooter>
      </BaseModal>

      <!-- View User Modal -->
      <BaseModal v-model="showViewModal" size="lg">
        <ModalHeader 
          title="User Details"
          @close="showViewModal = false"
        />
        <ModalBody>
          <div class="space-y-4">
            <div class="grid grid-cols-2 gap-4">
              <div>
                <p class="text-xs text-gray-500 dark:text-gray-400 uppercase tracking-wider">ID</p>
                <p class="text-sm font-medium text-gray-900 dark:text-white mt-1">{{ selectedUser?.id }}</p>
              </div>
              <div>
                <p class="text-xs text-gray-500 dark:text-gray-400 uppercase tracking-wider">Name</p>
                <p class="text-sm font-medium text-gray-900 dark:text-white mt-1">{{ selectedUser?.name }}</p>
              </div>
              <div>
                <p class="text-xs text-gray-500 dark:text-gray-400 uppercase tracking-wider">Email</p>
                <p class="text-sm font-medium text-gray-900 dark:text-white mt-1">{{ selectedUser?.email }}</p>
              </div>
              <div>
                <p class="text-xs text-gray-500 dark:text-gray-400 uppercase tracking-wider">Role</p>
                <p class="text-sm font-medium text-gray-900 dark:text-white mt-1">
                  <span class="inline-flex items-center gap-2">
                    <font-awesome-icon 
                      :icon="selectedUser?.role === 'Admin' ? 'crown' : selectedUser?.role === 'Editor' ? 'pen' : 'user'" 
                      class="text-xs"
                    />
                    {{ selectedUser?.role }}
                  </span>
                </p>
              </div>
              <div>
                <p class="text-xs text-gray-500 dark:text-gray-400 uppercase tracking-wider">Status</p>
                <p class="text-sm font-medium mt-1">
                  <span
                    class="inline-flex items-center px-2.5 py-1 rounded-full text-xs font-medium"
                    :class="{
                      'bg-green-100 text-green-800 dark:bg-green-900/30 dark:text-green-400': selectedUser?.status === 'Active',
                      'bg-gray-100 text-gray-800 dark:bg-gray-700 dark:text-gray-400': selectedUser?.status === 'Inactive',
                      'bg-yellow-100 text-yellow-800 dark:bg-yellow-900/30 dark:text-yellow-400': selectedUser?.status === 'Pending'
                    }"
                  >
                    {{ selectedUser?.status }}
                  </span>
                </p>
              </div>
            </div>
          </div>
        </ModalBody>
        <ModalFooter>
          <BaseButton variant="ghost" label="Close" @click="showViewModal = false" />
        </ModalFooter>
      </BaseModal>
    </div>
  </NuxtLayout>
</template>