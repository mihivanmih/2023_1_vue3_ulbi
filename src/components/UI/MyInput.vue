<template>
  <input type="text" :value="modelValue" @input="updateInput" class="input">
<!--  <input type="text" :value="value" :Myvalue="Myvalue" @input="updateInput" class="input">-->
</template>

<script>
export default {
  name: 'my-input',
  props: {
    //value: [String, Number],
    //Myvalue: [String, Number]
    modelValue: [String, Number]
  },
  methods: {
    updateInput(event) {
      this.$emit('update:modelValue', event.target.value)
      // this.$emit('update:value', event.target.value)
      // this.$emit('update:Myvalue', event.target.value)
    }
  }
}
</script>

<style>

.input {
  width: 100%;
  border: 1px solid teal;
  padding: 10px 15px;
  margin-top: 15px;
}

</style>