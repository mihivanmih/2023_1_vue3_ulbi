<template>
  <button class="btn">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: 'my-button'
}
</script>

<style>

.btn {
  align-self: end;
  margin-top: 15px;
  padding: 10px 15px;
  color: teal;
  border: 1px solid teal;
  background: none;
  cursor: pointer;
}
</style>