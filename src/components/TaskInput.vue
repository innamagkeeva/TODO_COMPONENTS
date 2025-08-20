<script setup lang="ts">
defineProps<{
  placeholder: string
}>()
//Для себя: если это не написать, то все равно работает, но писать надо. GPT объяснил почему.

const modelValue = defineModel<string>()
// // defineModel: Позволяет компоненту принимать v-model
// // Автоматически связывает  modelValue и событие update:modelValue, то есть меняет его на нужный из родительского
</script>

<template>
  <input
    class="form__input"
    type="text"
    placeholder="placeholder"
    v-model="modelValue"
  />
</template>

<style scoped>
.form__input {
  flex-grow: 1;
  height: 30px;
  font-size: 16px;
  padding: 5px;
  border: none;
  outline: none;
}
</style>
