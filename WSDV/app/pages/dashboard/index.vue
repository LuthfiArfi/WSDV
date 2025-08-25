<template>
  <div class="p-8 bg-gray-100 min-h-screen">
    <BarChart
      title="Grafik Penjualan"
      v-model="chartData"
    />
    <button
      class="mt-6 px-4 py-2 bg-blue-600 text-white rounded"
      @click="updateData"
    >
      Update Data
    </button>
  </div>
</template>

<script setup>
import { ref } from 'vue'


const chartData = ref({
  labels: ['Jan', 'Feb', 'Mar', 'Apr', 'Mei', 'Jun'],
  dataset: {
    label: 'Sales',
    data: [120, 190, 300, 250, 220, 270]
  }
})

const updateData = () => {
  chartData.value.labels.push('Jul')
  chartData.value.dataset.data.push(310)
}
</script>
