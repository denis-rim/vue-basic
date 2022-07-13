<template>
  <button class="button">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: 'my-button',
}
</script>

<style scoped>
.button {
  width: 100px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  background-color: blue;
  color: white;
}
</style>
