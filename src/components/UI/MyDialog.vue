<template>
  <div class="dialog" v-if="show" @click.stop="hideDialog">
    <div class="dialog__content" @click.stop>
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "my-dialog",
  props: {
    show: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    hideDialog () {
      this.$emit('update:show', false)
    }
  }
}
</script>

<style scoped>
  .dialog {
    background: rgba(0, 0, 0, 0.5);
    position: fixed;
    display: flex;
    inset: 0;
  }
  .dialog__content {
    margin: auto;
    min-height: 50px;
    background: #fff;
    border-radius: 8px;
    padding: 20px;
    min-width: 300px;
  }
</style>