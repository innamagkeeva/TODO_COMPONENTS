<script setup lang="ts">
import TaskCheckbox from '@/components/TaskCheckbox.vue'
import TaskText from '@/components/TaskText.vue'
import TaskButtonDelete from '@/components/TaskButtonDelete.vue'

interface Task {
  text: string
  status: 'done' | 'notDone'
  priority: 'high' | 'low'
}

const { task } = defineProps<{
  task: Task
}>()
// Эта запись заменяет const props = defineProps...  неявный проп. Иначе проп не используется (предупреждение)

const emit = defineEmits<{
  (e: 'change-status', task: Task): void
  (e: 'delete', task: Task): void
}>()
</script>

<template>
  <li class="list__item">
    <TaskCheckbox
      :checked="task.status === 'done'"
      @change="emit('change-status', task)"
    />
    <TaskText :text="task.text" />
    <TaskButtonDelete @click="emit('delete', task)" />
  </li>
</template>

<style scoped>
.list__item {
  max-width: 100%;
  height: 45px;
  border: 1px solid black;
  margin-bottom: 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 5px;
}
</style>
