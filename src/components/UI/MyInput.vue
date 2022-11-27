<template>
    <input class="input" type="text" :value="modelValue" @input="updateInput" :placeholder="placeholder">
</template>

<script>
    export default {
        name: "my-input",
        props: {
          placeholder: {
            type: String,
            default: ''
          },
          modelValue: [String, Number]
        },
        methods: {
          updateInput(event) {
           this.$emit('update:modelValue', event.target.value)
          }
        }
    }
</script>

<style scoped>
.input {
  width: 100%;
  border: 1px solid teal;
  padding: 10px 15px;
  margin-top: 15px;
}
</style>