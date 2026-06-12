<template>
  <div ref="chartRef" style="width: 100%; height: 500px;"></div>
</template>

<script lang="ts" setup>
import { ref, onMounted, onUnmounted } from 'vue'
import * as echarts from 'echarts'

const chartRef = ref(null)
let chartInstance = null

// 数据和颜色配置（和你示例的颜色、比例对应）
const data = [
  { name: 'Vue3', value: 95, itemStyle: { color: '#0055AA' } },
  { name: 'Nuxt', value: 75, itemStyle: { color: '#008833' } },
  { name: 'UniApp/原生微信小程序', value: 75, itemStyle: { color: '#C85211' } },
  { name: 'Electron', value: 80, itemStyle: { color: '#E6B800' } },
  { name: 'React', value: 20, itemStyle: { color: '#04a49f' } },
]

onMounted(() => {
  if (!chartRef.value) return
  chartInstance = echarts.init(chartRef.value)

  const option = {
    tooltip: {
      trigger: 'item',
      backgroundColor: 'rgba(0,0,0,0.8)',
      textStyle: { color: '#fff' }
    },
    legend: {
      orient: 'horizontal',
      bottom: 10,
      left: 'center',
      textStyle: {
        color: '#fff',
        fontSize: 20
      },
      icon: 'circle',
      data: data.map(d => d.name)
    },
    series: [
      {
        name: '技术栈',
        type: 'pie',
        radius: ['40%', '70%'], // 环形效果
        avoidLabelOverlap: false,
        itemStyle: {
          borderRadius: 0,
          borderColor: '#000',
          borderWidth: 3
        },
        label: {
          show: false
        },
        emphasis: {
          label: {
            show: false
          }
        },
        labelLine: {
          show: false
        },
        data: data
      }
    ]
  }

  chartInstance.setOption(option)

  // 窗口大小自适应
  const resizeHandler = () => chartInstance?.resize()
  window.addEventListener('resize', resizeHandler)

  onUnmounted(() => {
    window.removeEventListener('resize', resizeHandler)
    chartInstance?.dispose()
  })
})
</script>