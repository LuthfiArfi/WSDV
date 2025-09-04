<template>
    <div>
        <h1>This is service ID page : {{ id }}</h1>
        <div class="px-4 max-w-256 mx-auto">
            <DataTable :data="students" :columns="columns" />
        </div>
    </div>
</template>

<script setup>
import { useRoute } from 'vue-router'

const route = useRoute()
const id = route.params.serviceID

const students = [
    { name: 'Alya', age: 20, major: 'Informatika' },
    { name: 'Rizky', age: 22, major: 'Sistem Informasi' },
    { name: 'Dinda', age: 21, major: 'Teknik Elektro' },
  ]
  
  const columns = [
    { key: 'name', label: 'Nama' },
    { key: 'age', label: 'Umur' },
    { key: 'major', label: 'Jurusan' },
  ]
</script>

  

  