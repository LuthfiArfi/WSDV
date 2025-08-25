<script setup>
import { ref } from 'vue'
import { TabGroup, TabList, Tab, TabPanels, TabPanel } from '@headlessui/vue'

const tabs = ['Informasi Pribadi', 'Detail Pekerjaan', 'Preferensi']
const selectedTab = ref(tabs[0])

const form = ref({
  nama: '',
  email: '',
  posisi: '',
  perusahaan: '',
  bahasa: '',
  tema: 'terang'
})

const submitForm = () => {
  console.log('Data dikirim:', form.value)
}
</script>

<template>
  <div class="max-w-2xl mx-auto p-6 bg-white shadow rounded">
    <TabGroup>
      <TabList class="flex space-x-4 border-b mb-4">
        <Tab
          v-for="tab in tabs"
          :key="tab"
          class="px-4 py-2 focus:outline-none"
          :class="{ 'border-b-2 border-blue-500': selectedTab === tab }"
          @click="selectedTab = tab"
        >
          {{ tab }}
        </Tab>
      </TabList>

      <TabPanels>
        <TabPanel v-if="selectedTab === 'Informasi Pribadi'">
          <div class="space-y-4">
            <InputText label="Nama" v-model="form.nama" inputClass="" />
            <InputText label="Email" type="email" v-model="form.email" />
          </div>
        </TabPanel>

        <TabPanel v-if="selectedTab === 'Detail Pekerjaan'">
          <div class="space-y-4">
            <InputText label="Posisi" v-model="form.posisi" />
            <InputText label="Perusahaan" v-model="form.perusahaan" />
          </div>
        </TabPanel>

        <TabPanel v-if="selectedTab === 'Preferensi'">
          <div class="space-y-4">
            <InputText label="Bahasa Favorit" v-model="form.bahasa" />
            <label>
              Tema:
              <select v-model="form.tema" class="input">
                <option value="terang">Terang</option>
                <option value="gelap">Gelap</option>
              </select>
            </label>
          </div>
        </TabPanel>
      </TabPanels>

      <div class="mt-6 text-right">
        <button @click="submitForm" class="px-4 py-2 bg-blue-600 text-white rounded">Submit</button>
      </div>
    </TabGroup>
  </div>
</template>
