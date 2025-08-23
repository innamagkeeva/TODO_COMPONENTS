<script setup lang="ts">
import TaskItem from '@/components/TaskItem.vue'

interface Task {
  text: string
  status: 'done' | 'notDone'
  priority: 'high' | 'low'
}

const props = defineProps<{
  tasks: Task[]
}>()

const emit = defineEmits<{
  (e: 'change-status', task: Task): void
  (e: 'delete', task: Task): void
}>()
</script>

<template>
  <ul class="list">
    <TaskItem
      v-for="task in props.tasks"
      :key="task.text"
      :task="task"
      @change-status="emit('change-status', task)"
      @delete="emit('delete', task)"
    />
  </ul>
</template>

<style scoped>
.list {
  padding: 0;
  margin: 0;
}
</style>
