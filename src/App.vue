<script setup lang="ts">
import { computed, ref } from 'vue'

import TaskForm from '@/components/TaskForm.vue'

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
    <h1 class="title">HIGH</h1>
    <TaskForm
      v-model="inputTaskTextHigh"
      placeholder="Добавить задачу"
      @submit="addTask"
    />
    <ul class="list">
      <li
        class="list__item"
        v-for="task in highPriorityTasks"
        :key="task.text"
      >
        <input
          class="list__checkbox"
          type="checkbox"
          @click="changeStatus(task)"
        />
        <p class="list__text">{{ task.text }}</p>
        <button
          class="list__button-delete"
          @click="deleteTask(task)"
        >
          +
        </button>
      </li>
    </ul>
    <h1 class="title">LOW</h1>
    <TaskForm
      v-model="inputTaskTextLow"
      placeholder="Добавить задачу"
      @submit="addTask"
    />
    <ul class="list">
      <li
        class="list__item"
        v-for="task in lowPriorityTasks"
        :key="task.text"
      >
        <input
          class="list__checkbox"
          type="checkbox"
          @click="changeStatus(task)"
        />
        <p class="list__text">{{ task.text }}</p>
        <button
          class="list__button-delete"
          @click="deleteTask(task)"
        >
          +
        </button>
      </li>
    </ul>
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

.title {
  width: 100px;
  margin: 0 auto;
  margin-bottom: 20px;
}

.form,
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

.list {
  padding: 0;
  margin: 0;
}

.list__button-delete {
  rotate: 45deg;
}

button {
  border: none;
  background-color: white;
  cursor: pointer;
}

.list__text {
  display: flex;
  flex-grow: 1;
  align-items: center;
  height: 30px;
}
</style>
