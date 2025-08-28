<template>
    <div class="border-2 border-blue-700 max-w-lg mx-auto p-5 rounded shadow bg-gray-300">
        <h1 class="text-center text-2xl font-bold pb-5">WSDV Reporting System</h1>
        
        <Alert v-if="errorMessage" modelValue="False" type="error" dismissible @dismissed="handleDismissed">{{ errorMessage}}</Alert>
        <form @submit.prevent="handleLogin">
        <InputText label="Username" v-model="username" placeholder="your username" inputclass="bg-white" />
        <InputText label="Password" type="password" placeholder="********" v-model="password" />
        <div class="pt-4 flex justify-center">
          <Button label="Login" variant="primary" type="submit" @click="handleLogin"/>
        </div>
        </form>
    </div>
</template>

<script setup>
import { ref } from 'vue'
import { navigateTo } from 'nuxt/app'

const username = ref('')
const password = ref('')
const errorMessage = ref('')

const handleDismissed = () => {
  errorMessage.value = ''
}

const handleLogin = () => {
  if (!username.value || !password.value) {
    errorMessage.value = 'Email dan password wajib diisi.'
    return
  }

  // Simulasi login (ganti dengan API call)
  // harusnya pakai async
  if (username.value === 'admin' && password.value === '123456') {
    errorMessage.value = ''
    console.log('Login berhasil!')
    // Redirect atau simpan token di sini
    navigateTo('/dashboard')
  } else {
    errorMessage.value = 'Email atau password salah.'
  }
}
</script>