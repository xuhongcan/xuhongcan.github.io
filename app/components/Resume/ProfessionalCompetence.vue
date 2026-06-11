<template>
    <div ref="chartRef" style="width: 100%; height: 600px;"></div>

</template>

<script lang="ts" setup>

import { ref, onMounted, onUnmounted } from 'vue'
import * as echarts from 'echarts'
import ProfessionalCompetence from '~/components/Resume/ProfessionalCompetence.vue'

const chartRef = ref(null)
let chartInstance = null




// 数据配置（和你表格中的数据一致）
const radarData = [90, 95, 90, 100, 80]
const indicator = [
  { name: '前端基础三件套', max: 100 },
  { name: 'Vue3/Nuxt', max: 100 },
  { name: 'Electron/微信小程序原生/uniapp', max: 100 },
  { name: '自学能力', max: 100 },
  { name: '需求分析与产品沟通', max: 100 }
]

onMounted(() => {
  if (!chartRef.value) return
  chartInstance = echarts.init(chartRef.value)

  const option = {
    backgroundColor: 'rgba(255, 255, 255, 0.5)',
    radar: {
      indicator: indicator,
      shape: 'polygon',
      splitNumber: 4,
      axisName: {
        color: '#333',
        fontSize: 18
      },
      splitArea: {
        areaStyle: {
          color: ['#fff', '#fff', '#fff', '#fff']
        }
      },
      axisLine: {
        lineStyle: {
          color: '#e0e0e0'
        }
      },
      splitLine: {
        lineStyle: {
          color: '#e0e0e0'
        }
      }
    },
    series: [
      {
        type: 'radar',
        data: [
          {
            value: radarData,
            name: '个人能力',
            areaStyle: {
              color: 'rgba(59, 130, 246, 0.2)'
            },
            lineStyle: {
              color: '#3b82f6',
              width: 2
            },
            itemStyle: {
              color: '#3b82f6'
            }
          }
        ]
      }
    ]
  }

  chartInstance.setOption(option)

  // 窗口大小变化时自动重绘
  const resizeHandler = () => chartInstance?.resize()
  window.addEventListener('resize', resizeHandler)

  onUnmounted(() => {
    window.removeEventListener('resize', resizeHandler)
    chartInstance?.dispose()
  })
})
</script>
