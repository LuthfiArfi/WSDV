<template>
  <nav class="bg-[#ec1c24] text-white p-4 border-b border-gray-200 shadow-sm">
    <div class="container mx-auto flex justify-between items-center">
      <!-- Logo -->
      <NuxtLink to="/" class="text-2xl font-bold hover:text-gray-700 transition-colors">
        WSDV
      </NuxtLink>

      <!-- Menu + Account -->
      <div class="flex items-center space-x-6">
        <!-- Menu Links -->
        <ul class="flex space-x-4">
          <li>
            <NuxtLink to="/dashboard" class="hover:text-gray-500 transition-colors">
              Dashboard
            </NuxtLink>
          </li>
          <li>
            <NuxtLink to="/report" class="hover:text-gray-500 transition-colors">
              Reports
            </NuxtLink>
          </li>
          <li>
            <NuxtLink to="/about" class="hover:text-gray-500 transition-colors">
              About
            </NuxtLink>
          </li>
        </ul>

        <!-- Akun: Dropdown Menu -->
        <Menu as="div" class="relative">
          <MenuButton class="focus:outline-none">
            <template v-if="user.avatar">
              <img
                :src="user.avatar"
                alt="Avatar"
                class="w-9 h-9 rounded-full object-cover border"
              />
            </template>
            <template v-else>
              <div
                class="w-9 h-9 rounded-full bg-gray-400 text-white flex items-center justify-center font-semibold uppercase"
              >
                {{ user.initials }}
              </div>
            </template>
          </MenuButton>

          <Transition
            enter="transition ease-out duration-100"
            enter-from="transform opacity-0 scale-95"
            enter-to="transform opacity-100 scale-100"
            leave="transition ease-in duration-75"
            leave-from="transform opacity-100 scale-100"
            leave-to="transform opacity-0 scale-95"
          >
            <MenuItems
              class="absolute right-0 mt-2 w-48 origin-top-right rounded-md bg-white shadow-lg ring-1 ring-black/5 focus:outline-none z-50"
            >
              <div class="py-1">
                <MenuItem v-slot="{ active }">
                  <NuxtLink
                    to="/profile"
                    :class="[
                      'block px-4 py-2 text-sm',
                      active ? 'bg-gray-100 text-gray-900' : 'text-gray-700'
                    ]"
                  >
                    Profile
                  </NuxtLink>
                </MenuItem>

                <MenuItem v-slot="{ active }">
                  <NuxtLink
                    to="/settings"
                    :class="[
                      'block px-4 py-2 text-sm',
                      active ? 'bg-gray-100 text-gray-900' : 'text-gray-700'
                    ]"
                  >
                    Settings
                  </NuxtLink>
                </MenuItem>

                <MenuItem v-slot="{ active }">
                  <button
                    @click="logout"
                    :class="[
                      'block w-full text-left px-4 py-2 text-sm',
                      active ? 'bg-gray-100 text-gray-900' : 'text-gray-700'
                    ]"
                  >
                    Logout
                  </button>
                </MenuItem>
              </div>
            </MenuItems>
          </Transition>
        </Menu>
      </div>
    </div>
  </nav>
</template>

<script setup>
import { Menu, MenuButton, MenuItems, MenuItem } from '@headlessui/vue'
import { Transition } from 'vue'

// Simulasi user
const user = {
  name: 'John Doe',
  avatar: null, // bisa diisi url gambar
  initials: 'JD'
}

const logout = () => {
  console.log('Logging out...')
  // tambahkan logika logout
}
</script>
