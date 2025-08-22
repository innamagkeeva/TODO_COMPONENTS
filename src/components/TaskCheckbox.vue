<script setup lang="ts">
defineProps<{
  checked: boolean
}>()

const emit = defineEmits<{
  change: []
}>()
</script>

<template>
  <input
    class="list__checkbox"
    type="checkbox"
    :checked="checked"
    @change="emit('change')"
  />
</template>

<style scoped>
.list__checkbox {
  margin-right: 10px;
}
</style>

<!-- Для себя :checked="checked" - Это выражение означает: "Установи атрибут checked равным значению переменной checked" -->

<!-- ????? Не пойму как закомментировать строчку для своего комментария в теге template  в нужном мне месте -->
