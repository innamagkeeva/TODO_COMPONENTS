<script setup lang="ts">
defineProps<{
  text: string
}>()
</script>

<template>
  <p class="list__text">{{ text }}</p>
</template>

<style scoped>
.list__text {
  display: flex;
  flex-grow: 1;
  align-items: center;
  height: 30px;
}
</style>
