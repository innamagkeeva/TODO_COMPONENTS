<script setup lang="ts">
//  В этом случае никаких props не требуется, так как кнопка только отображает символ + и ничего не принимает
</script>

<template>
  <button
    class="form__button"
    type="submit"
  >
    +
  </button>
</template>

<style scoped>
.form__button {
  border: none;
  background-color: white;
  padding: 0 10px;
  cursor: pointer;
}
</style>
