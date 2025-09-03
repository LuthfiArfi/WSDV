<template>
    <div>
        This is main layout
        <Button @click="showDialog = true">test</button>
        <FormServiceid />
        <FormBiogasreport />
        <DialogTime
         :isOpen="showDialog"
        title="Notifikasi"
        message="Data berhasil disimpan!"
        :duration="10000"
        @close="showDialog = false"
        />
    </div>
</template>

<script setup>
const showDialog = ref()
</script>