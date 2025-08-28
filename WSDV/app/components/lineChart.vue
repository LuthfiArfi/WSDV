<template>
  <div class="w-full" :class="wrapperClass" :style="wrapperStyle">
    <h2 v-if="title" class="text-lg font-bold mb-2">{{ title }}</h2>
    <canvas
      ref="canvas"
      :class="canvasClass"
      :style="canvasStyle"
    ></canvas>
  </div>
</template>

<script setup>
import { ref, watch, onMounted, onBeforeUnmount } from 'vue'
import {
  Chart,
  LineController,
  LineElement,
  PointElement,
  CategoryScale,
  LinearScale,
  Tooltip,
  Legend
} from 'chart.js'

// ✅ Register semua komponen yang dibutuhkan untuk line chart
Chart.register(LineController, LineElement, PointElement, CategoryScale, LinearScale, Tooltip, Legend)

const props = defineProps({
  title: { type: String, default: 'Line Chart' },
  modelValue: { type: Object, required: true },
  canvasClass: { type: String, default: '' },
  canvasStyle: { type: [String, Object], default: '' },
  wrapperClass: { type: String, default: '' },
  wrapperStyle: { type: [String, Object], default: '' }
})

const canvas = ref(null)
let chartInstance = null

const renderChart = () => {
  if (!canvas.value) return

  const { labels = [], datasets = [] } = props.modelValue || {}

  if (!Array.isArray(labels) || !Array.isArray(datasets)) return

  if (chartInstance) {
    chartInstance.destroy()
  }

  chartInstance = new Chart(canvas.value, {
    type: 'line',
    data: { labels, datasets },
    options: {
      responsive: true,
      maintainAspectRatio: false,
      plugins: {
        legend: { display: true },
        tooltip: { enabled: true }
      },
      scales: {
        y: { beginAtZero: true }
      }
    }
  })
}

onMounted(renderChart)
onBeforeUnmount(() => {
  if (chartInstance) chartInstance.destroy()
})
watch(() => props.modelValue, renderChart, { deep: true })
</script>

<style scoped>
.chart-canvas {
  height: 256px;
}
</style>
