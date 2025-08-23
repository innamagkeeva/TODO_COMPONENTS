<script setup lang="ts">
const emit = defineEmits<{
  click: []
}>()
</script>

<template>
  <button
    class="list__button-delete"
    @click="emit('click')"
  >
    +
  </button>
</template>

<style scoped>
.list__button-delete {
  rotate: 45deg;
  border: none;
  background-color: white;
  cursor: pointer;
}
</style>
