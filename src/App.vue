<template>

  <div id="app">

    <div class="app__container">
      <button class="button" @click="setShowAddUserModal()">Добавить</button>
    </div>

    <div class="app__container">
      <users-table :userList="userList"/>
      <add-user-modal :userList="userList" v-if="showAddUserModal" v-on:setShowAddUserModal = "setShowAddUserModal" v-on:addNewUser = "addNewUser"/>
    </div>

  </div>

</template>

<script>
import AddUserModal from './components/AddUserModal.vue'
import UsersTable from './components/UsersTable.vue'
import { watch } from 'vue'

export default {
  // Код, скорее всего, не самый идеальный, но я быстро учусь (честно честно)
  name: 'App',

  components: {
    UsersTable,
    AddUserModal
  },

  data () {
    return {
      showAddUserModal: false,
      userList: JSON.parse(localStorage.getItem('userList')) || [
        {
          name: 'Уолтер Уайт',
          number: 89347823673,
          child: false,
          boss: null
        },
        {
          name: 'Джесси Пинкман',
          number: 89347820000,
          child: true,
          boss: 'Уолтер Уайт'
        }
      ]
    }
  },

  methods: {
    setShowAddUserModal () {
      this.showAddUserModal = !this.showAddUserModal
    },
    addNewUser (newUser) {
      this.userList.push(newUser)
      localStorage.setItem('userList', JSON.stringify(this.userList))
    },
  }, 
}
</script>


<style scoped>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background-color: #fff;
}
.app__container{
  display: flex;
  justify-content: center;
}

.button{
    padding: 1rem;
    width: 20%;
    border: none;
    background-color: #439A86;
    color: #fff;
    font-weight: bold;
    border-radius: 1rem;
    transition: 0.3s;
}
.button:hover{
    cursor: pointer;
    background-color: #36806e;
}
</style>
