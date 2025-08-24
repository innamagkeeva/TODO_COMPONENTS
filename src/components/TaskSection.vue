<script setup lang="ts">
import TaskSectionTitle from '@/components/TaskSectionTitle.vue'
import TaskForm from '@/components/TaskForm.vue'
import TaskList from '@/components/TaskList.vue'

interface Task {
  text: string
  status: 'done' | 'notDone'
  priority: 'high' | 'low'
}

const model = defineModel<string>()
// это v-model

const { title, tasks } = defineProps<{
  title: string
  tasks: Task[]
}>()

const emit = defineEmits<{
  'update:modelValue': [value: string]
  submit: []
  'change-status': [task: Task]
  delete: [task: Task]
}>()

function handleSubmit() {
  emit('submit')
}
</script>

<template>
  <TaskSectionTitle :text="title" />
  <TaskForm
    v-model="model"
    :placeholder="'Добавить задачу'"
    @submit="handleSubmit"
  />
  <TaskList
    :tasks="tasks"
    @change-status="(task) => emit('change-status', task)"
    @delete="(task) => emit('delete', task)"
  />
</template>
