<template>
  <div v-if="show" class="modal-window">
    <div class="modal-window__header">
      <h1 class="header">Добавление пользователя</h1>
      <img @click="close"
      class="modal-window__close-icon" src="../../public/close-icon.svg" alt="close">
    </div>

    <GuiInput v-model="name.value" :label="name.label"/>
    <GuiInput v-model="phone.value" :label="phone.label"/>
    <GuiSelect v-model="head.value" :label="head.label" :options="headOptions"/>
    <GuiButton
      :disabled="buttonIsDisabled"
      :label="buttonSaveUser.label"
      @click.native="addNewUser"/>
  </div>
</template>

<script>
import GuiInput from '../components/Gui/GuiInput.vue'
import GuiSelect from '../components/Gui/GuiSelect.vue'
import GuiButton from '../components/Gui/GuiButton.vue'
import { nanoid } from 'nanoid'

export default {
  components: {
    GuiInput,
    GuiSelect,
    GuiButton
  },
  props: {
    allUsers: {
      required: true,
      type: Array
    },
    show: {
      type: Boolean
    }
  },
  data () {
    return {
      name: {
        label: 'Имя',
        value: null
      },
      phone: {
        label: 'Телефон',
        value: null
      },
      head: {
        label: 'Начальник',
        value: null
      },
      buttonSaveUser: {
        label: 'Сохранить'
      }
    }
  },
  computed: {
    buttonIsDisabled () {
      return !this.name.value || !this.phone.value
    },
    headOptions () {
      const userOptions = this.allUsers.map(user => {
        return {label: user.name, value: user.id}
      })

      return [{label: 'Не выбрано', value: null}, ...userOptions]
    }
  },

  methods: {
    close () {
      this.$emit('onClose')
    },

    addNewUser () {
      const newUser = {
        name: this.name.value,
        phone: this.phone.value,
        head: this.head.value,
        subordinateUsers: [],
        id: nanoid()
      }

      this.$emit('addUser', newUser)

      this.clearForm()
    },

    clearForm () {
      this.name.value = null
      this.phone.value = null
      this.head.value = null
    }
  }
}
</script>

<style scoped>
.modal-window {
  width: 500px;
  padding: 16px 24px;
  border: 2px solid black;
  margin-top: 65px;
}

.modal-window__header {
  display: flex;
  justify-content: space-between;
  height: 24px;
  margin-bottom: 24px;
}

.modal-window__close-icon {
  cursor: pointer;
}

.header {
  font-size: 18px;
  line-height: 24px;
}
</style>
