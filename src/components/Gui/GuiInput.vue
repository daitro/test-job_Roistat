<template>
  <div class="input-text">
    <label>{{label}}</label>
    <input
      class="input-text__field"
      type="text"
      :value="value"
      @input="onInput"
    />
  </div>
</template>

<script>
export default {
  methods: {
    onInput (event) {
      this.$emit('input', event.target.value)
    }
  },
  props: {
    value: {
      type: String
    },
    label: {
      type: String
    }
  }
}
</script>

<style scoped>
.input-text {
  margin-top: 24px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.input-text__field {
    width: 260px;
    padding: 8px;
    border: 1px solid rgb(35, 33, 33);
    box-sizing: border-box;
    margin-right: 24px;
  }
</style>
