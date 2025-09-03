<template>
    <div>
        <h1>This is service ID page : {{ serviceID }}</h1>
    </div>
</template>

<script setup>
import { useRoute } from 'vue-router'

const route = useRoute()
const id = route.params.serviceID
</script>