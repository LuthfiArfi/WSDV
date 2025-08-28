<template>
  <div class="max-w-5xl mx-auto p-6 bg-white shadow rounded">
    <h1 class="text-2xl font-bold mb-4 text-center">Biogas Report</h1>

    <TabGroup>
      <TabList
        class="flex overflow-x-auto whitespace-nowrap border-b mb-4 scrollbar-thin justify-center"
      >
        <Tab
          v-for="tab in tabs"
          :key="tab"
          class="px-4 py-2 mb-2 focus:outline-none"
          :class="[
            selectedTab === tab
              ? 'border-b-2 border-blue-500 text-blue-600 font-medium'
              : 'text-gray-600 hover:text-blue-600'
          ]"
          @click="selectedTab = tab"
        >
          {{ tab }}
        </Tab>
      </TabList>

      <TabPanels>
        <TabPanel v-if="selectedTab === 'General'">
          <div class="space-y-4">
            <InputText label="Service ID" v-model="form.nama" disabled="True"/>
            <InputText label="Workshop" type="email" v-model="form.email" />
            <InputText label="Customer" type="email" v-model="form.email" />
            <div class="flex flex-col md:flex-row md:space-x-4 space-y-4 md:space-y-0">
              <InputDate label="Tanggal Mulai" class="w-full" />
              <InputDate label="Tanggal Akhir" class="w-full" />
            </div>
            <InputRepeater label="Attendees" v-model="attendees" />
            <div>{{ attendees }}</div>
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

        <TabPanel v-else>
          <p class="text-gray-500">Konten belum tersedia untuk tab ini.</p>
        </TabPanel>
      </TabPanels>

      <div class="mt-6 text-right">
        <button
          @click="submitForm"
          class="px-4 py-2 bg-blue-600 text-white rounded"
        >
          Submit
        </button>
      </div>
    </TabGroup>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { TabGroup, TabList, Tab, TabPanels, TabPanel } from '@headlessui/vue'

const tabs = [
  'General',
  'Bio Digester',
  'Scrubber',
  'Dryer/Chiller',
  'Gas Blower',
  'Gas Engine',
]

const attendees = ref([])

const selectedTab = ref(tabs[0])

const form = ref({
  nama: 'asdhaoi',
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
