<template>
  <nav class="bg-white text-black p-4 border-b border-gray-7=500">
    <div class="container mx-auto flex justify-between items-center">
      <NuxtLink to="/" class="text-2xl font-bold hover:text-gray-700 transition-colors">
        WSDV
      </NuxtLink>

      <ul class="flex space-x-4">
        <li>
          <NuxtLink to="/" class="hover:text-gray-500 transition-colors">
            Dashboard
          </NuxtLink>
        </li>
        <li>
          <NuxtLink to="/about" class="hover:text-gray-500 transition-colors">
            Tentang
          </NuxtLink>
        </li>
        <li>
          <NuxtLink to="/contact" class="hover:text-gray-500 transition-colors">
            Kontak
          </NuxtLink>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script setup>
// Tidak ada logika JavaScript yang diperlukan untuk komponen statis ini
</script>