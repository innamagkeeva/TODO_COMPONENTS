<script setup lang="ts">
defineProps<{
  text: string
}>()
</script>

<template>
  <h1 class="title">{{ text }}</h1>
</template>

<style scoped>
.title {
  width: 100px;
  margin: 0 auto;
  margin-bottom: 20px;
}
</style>
