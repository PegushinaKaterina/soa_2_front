<template>
  <button class="button elementForm">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: "my-button",
};
</script>

<style scoped>
.button {
  margin-top: 5px;
  margin-bottom: 5px;
  width: var(--button-size);
  padding: 5px;
  background-color: #d59e6a;
  border: 1px solid black;
  font-size: var(--element-form-text-size);
}
</style>
