<template>
  <div class="table">
    <div class="row row--bold">
      <div class="row__item row__item--name">Имя</div>
      <div class="row__item row__item--phone">Телефон</div>
    </div>

    <UserRow v-for="item of heads" :key="item.id" :user="item" />
  </div>
</template>

<script>
import UserRow from './UserRow.vue'

export default {
  props: {
    listItems: {
      type: Array
    }
  },
  components: {
    UserRow
  },
  computed: {
    heads () {
      return this.listItems.filter(user => !user.head)
    }
  }
}
</script>

<style>
.table {
  width: 400px;
  margin-right: 24px;
  display: flex;
  flex-direction: column;
}

.row {
  font-size: 16px;
  border: 1px solid rgb(69, 69, 69);
  display: flex;
  margin-top: -1px;
}

.row--bold {
  font-weight: 600;
}

.row--cursor_pointer {
  cursor: pointer;
}

.row__item {
  padding: 8px 12px;
}

.row__item:not(:last-child) {
  border-right: 1px solid rgb(69, 69, 69);
}

.row__item--name {
  width: 40%;
}

.row__item--phone {
  width: 60%;
}
</style>
