<template>
  <a-table :columns="columns" :data-source="data" row-key="id" bordered>
    <template #bodyCell="{ column, record }">
      <template v-if="column.key === 'overtime'">
        <a-tag :color="record.overtime ? 'red' : 'green'">
          {{ record.overtime ? 'Yes' : 'No' }}
        </a-tag>
      </template>
      <template v-else-if="column.key === 'action'">
        <a-button
          v-if="role === 'admin'"
          type="link"
          danger
          @click="deleteRow(record.id)"
        >
          Delete
        </a-button>
      </template>
      <template v-else>
        {{ record[column.key] }}
      </template>
    </template>
  </a-table>
</template>

<script setup>
const props = defineProps({
  data: { type: Array, required: true }
})
const emit = defineEmits(['update:data'])

const role = localStorage.getItem('role')

const columns = [
  { title: 'ID', dataIndex: 'id', key: 'id' },
  { title: 'Project', dataIndex: 'project', key: 'project' },
  { title: 'Overtime', dataIndex: 'overtime', key: 'overtime' },
  { title: 'Hours', dataIndex: 'hours', key: 'hours' },
  { title: 'Created At', dataIndex: 'created_at', key: 'created_at' },
  { title: 'Action', key: 'action' }
]

const deleteRow = (id) => {
  const newData = props.data.filter(item => item.id !== id)
  emit('update:data', newData)
}
</script>
