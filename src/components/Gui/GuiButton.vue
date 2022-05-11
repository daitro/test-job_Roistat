<template>
  <button :disabled="disabled" class="button">{{ label }}</button>
</template>

<script>
export default {
  props: {
    label: {
      type: String
    },
    disabled: {
      type: Boolean
    }
  }
}
</script>

<style scoped>
.button {
  width: 200px;
  line-height: 24px;
  padding: 8px;
  border-radius: 20px;
  border: 1px solid black;
  background-color: rgb(123, 108, 218);
  color: white;
  margin: 0 24px 24px 0;
}

.button[disabled] {
    background-color: rgba(141, 141, 141, 0.448);
    color: black;
  }
</style>
