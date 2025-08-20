<script setup lang="ts">
import TaskInput from '@/components/TaskInput.vue'
import AddButton from '@/components/AddButton.vue'

const modelValue = defineModel<string>()
// defineModel: Позволяет компоненту принимать v-model
// Автоматически связывает  modelValue и событие update:modelValue, то есть меняет его на нужный из родительского

defineProps<{
  placeholder: string
}>()

const emit = defineEmits<{
  submit: []
}>()

function onSubmit() {
  emit('submit')
}
</script>

<template>
  <form
    class="form"
    @submit.prevent="onSubmit"
  >
    <TaskInput
      v-model="modelValue"
      placeholder="Добавить задачу"
    />
    <AddButton />
  </form>
</template>

<style scoped>
.form {
  max-width: 100%;
  height: 45px;
  border: 1px solid black;
  border-radius: 5px;
  margin-bottom: 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 5px;
}
</style>
