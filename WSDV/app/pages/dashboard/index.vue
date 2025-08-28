<template>
  <div class="flex flex-row flex-wrap justify-center w-full p-4 h-[100vh]">
    <client-only>
      <div :class="chartWrapperClass" v-for="i in 4" :key="i">
        <BarChart
          :modelValue="chartData"
          title="Sales Chart"
          wrapperClass="w-full h-full"
        />
      </div>
      <div :class="chartWrapperClass">
        <LineChart
          :modelValue="chartData"
          title="Sales Chart"
          wrapperClass="w-full h-full"
        />
      </div>
      <div :class="chartWrapperClass">
        <PieChart
          :modelValue="chartData"
          title="Sales Chart"
          wrapperClass="w-full h-full"
        />
      </div>
    </client-only>
  </div>
</template>

<script setup>
const chartWrapperClass = 'flex-1 md:flex justify-center h-64 p-2 m-3 mb-5'

const chartData = {
  labels: ['Q1', 'Q2', 'Q3', 'Q4'],
  datasets: [
    {
      label: 'Revenue',
      data: [150, 200, 180, 220],
      backgroundColor: '#3b82f6'
    },
    {
      label: 'Gross Profit',
      data: [200, 150, 110, 250],
      backgroundColor: '#3da916'
    }
  ]
}
</script>
