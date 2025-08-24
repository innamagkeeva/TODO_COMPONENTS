<script setup lang="ts">
import { computed, ref } from 'vue'

import TaskSection from '@/components/TaskSection.vue'

const inputTaskTextHigh = ref('')
const inputTaskTextLow = ref('')

interface Task {
  text: string
  status: 'done' | 'notDone'
  priority: 'high' | 'low'
}

const tasks = ref<Task[]>([])

function addTask(): void {
  const textHigh = inputTaskTextHigh.value.trim()
  const textLow = inputTaskTextLow.value.trim()
  if (textHigh) {
    const capitalizedHighText = textHigh[0].toUpperCase() + textHigh.slice(1)
    tasks.value.push({ text: capitalizedHighText, status: 'notDone', priority: 'high' })
    inputTaskTextHigh.value = ''
    console.log('сработало')
  }
  if (textLow) {
    const capitalizedLowText = textLow[0].toUpperCase() + textLow.slice(1)
    tasks.value.push({ text: capitalizedLowText, status: 'notDone', priority: 'low' })
    inputTaskTextLow.value = ''
  }
}

const highPriorityTasks = computed(() => {
  return tasks.value.filter((task) => task.priority === 'high')
})
const lowPriorityTasks = computed(() => {
  return tasks.value.filter((task) => task.priority === 'low')
})

function changeStatus(task: Task): void {
  task.status = task.status === 'done' ? 'notDone' : 'done'
}

function deleteTask(taskToDelete: Task) {
  const index = tasks.value.findIndex((task) => task === taskToDelete)
  if (index !== -1) {
    tasks.value.splice(index, 1)
  }
}
</script>

<template>
  <div class="tasks">
    <TaskSection
      title="HIGH"
      v-model="inputTaskTextHigh"
      :tasks="highPriorityTasks"
      @submit="addTask"
      @change-status="changeStatus"
      @delete="deleteTask"
    />

    <TaskSection
      title="LOW"
      v-model="inputTaskTextLow"
      :tasks="lowPriorityTasks"
      @submit="addTask"
      @change-status="changeStatus"
      @delete="deleteTask"
    />
  </div>
</template>

<style scoped>
.tasks {
  width: 500px;
  height: 650px;
  border: 2px solid black;
  margin: 0 auto;
  padding: 10px 20px;
  font-size: 16px;
}
</style>
