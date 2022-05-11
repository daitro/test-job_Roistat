<template>
<div class="select-group">
  <label class="label">{{label}}</label>
  <select class="select" :value="value" @change="onChange">
    <option
      class="select__option"
      v-for="item of options"
      :key="item.value"
      :value="item.value"
    >
      {{ item.label }}
    </option>
  </select>
</div>
</template>

<script>
export default {
  data () {
    return {}
  },
  props: {
    options: {
      type: Array
    },
    value: {
      type: String
    },
    label: {
      type: String
    }
  },
  methods: {
    onChange (event) {
      this.$emit('input', event.target.value)
    }
  }
}
</script>

<style scoped>
.select-group {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 24px 24px 24px 0;
}

.label {
  margin-right: 16px;
}

.select {
  width: 260px;
  border: 1px solid rgb(35, 33, 33);
  padding: 8px;
  cursor: pointer;
}

.select__option {
    color: rgb(53, 53, 53);
  }
</style>
