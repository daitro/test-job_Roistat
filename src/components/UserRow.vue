<template>
  <div class="user">
    <div
      :class="['row', 'user__row', { 'row--cursor_pointer': hasSubordinates }]"
      @click="showSubordinates = !showSubordinates">
      <div class="row__item row__item--name">
        <span v-if="hasSubordinates">
          +
        </span>
        {{ user.name }}
      </div>

      <div class="row__item row__item--phone">{{ user.phone }}</div>
    </div>

    <div class="user__subordinates" v-if="hasSubordinates && showSubordinates">
      <UserRow
        v-for="item in user.subordinateUsers"
        :key="item.id"
        :user="item"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: 'UserRow',
  props: {
    user: {
      type: Object,
      required: true
    }
  },
  data () {
    return {
      showSubordinates: false
    }
  },
  computed: {
    hasSubordinates () {
      return this.user.subordinateUsers.length
    }
  }
}
</script>

<style>
.user__row.row--cursor_pointer:hover {
  background-color: lightgray;
  transition: background-color 0.22s;
}
.user__subordinates {
  width: 95%;
  margin-left: 5%;
}
</style>
