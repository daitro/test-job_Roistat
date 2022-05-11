<template>
  <div class="main-page">
    <div class="main-page__table">
      <GuiButton :label="buttonAddUser" @click.native="openModalWindow"/>
      <TableDataUsers :listItems="users"/>
    </div>
    <AddingUser @onClose="closeModalWindow" @addUser="onAddUser" :allUsers="flattedUsers" :show='modalWindow'/>
  </div>
</template>

<script>
import AddingUser from '../components/AddingUser.vue'
import GuiButton from '../components/Gui/GuiButton.vue'
import TableDataUsers from '../components/TableDataUsers.vue'

export default {
  components: {
    AddingUser,
    TableDataUsers,
    GuiButton
  },

  data () {
    return {
      users: [],
      buttonAddUser: 'Добавить',
      modalWindow: false
    }
  },

  computed: {
    flattedUsers () {
      console.log(this.flatUsers(this.users))
      return this.flatUsers(this.users)
    }
  },

  methods: {
    openModalWindow () {
      this.modalWindow = true
    },
    closeModalWindow () {
      this.modalWindow = false
    },
    flatUsers (users) {
      const nestedUsers = []

      users.forEach(user => {
        nestedUsers.push(user)

        if (user.subordinateUsers.length) {
          const subordinates = this.flatUsers(user.subordinateUsers)
          subordinates.forEach((user) => {
            nestedUsers.push(user)
          })
        }
      })

      return nestedUsers
    },
    onAddUser (user) {
      if (!user.head) {
        this.users.push(user)
      } else {
        const headOfCreatedUser = this.flattedUsers.find((item) => item.id === user.head)

        if (headOfCreatedUser) {
          headOfCreatedUser.subordinateUsers.push(user)
        }
      }

      localStorage.setItem('users', JSON.stringify(this.users))
    }
  },
  created () {
    const usersFromLS = localStorage.getItem('users')

    if (usersFromLS) {
      this.users = JSON.parse(usersFromLS)
    } else {
      localStorage.setItem('users', JSON.stringify(this.users))
    }
  }
}
</script>

<style scoped>
.main-page {
  display: flex;
  justify-content: space-between;
}

.main-page__table {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
}
</style>
