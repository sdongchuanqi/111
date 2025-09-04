<template>
  <div style="padding: 20px">
    <a-page-header
      title="工单管理系统"
      sub-title="工单列表 & 图表展示"
      @back="goBack"
    />
    <work-table v-model:data="orders" />
    <work-chart :data="orders" />
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'
import { mockOrders } from '../mockData.js'
import WorkTable from '../components/WorkTable.vue'
import WorkChart from '../components/WorkChart.vue'

const router = useRouter()
const orders = ref([...mockOrders])

const goBack = () => {
  localStorage.removeItem('role')
  router.push('/')
}

onMounted(() => {
  // 简单的权限控制展示：若未登录（无 role），回到登录页
  const role = localStorage.getItem('role')
  if (!role) router.push('/')
})
</script>
