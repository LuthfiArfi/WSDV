<template>
    <div class="border-2 border-blue-700 max-w-lg mx-auto p-5 rounded shadow bg-gray-300">
        <h1 class="text-center text-2xl font-bold pb-5">WSDV Reporting System</h1>
        <InputText label="Username" v-model="username" placeholder="username@user.com" inputclass="bg-white" />
        <InputText label="Password" type="Password" placeholder="********" v-model="password" />
        <div class="pt-4 flex justify-center">
          <ButtonSubmit label="Login" variant="primary"/>
        </div>
    </div>
</template>

<script>
import { ref } from 'vue'

const username = ref('')
const password = ref('')
const errorMessage = ref('')

const handleLogin = () => {
  if (!email.value || !password.value) {
    errorMessage.value = 'Email dan password wajib diisi.'
    return
  }

  // Simulasi login (ganti dengan API call)
  if (email.value === 'admin@example.com' && password.value === '123456') {
    errorMessage.value = ''
    console.log('Login berhasil!')
    // Redirect atau simpan token di sini
  } else {
    errorMessage.value = 'Email atau password salah.'
  }
}
</script>