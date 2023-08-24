<template>
  <div class="modal" @click.stop="closeAddUserModal()">

    <div class="modal__content"  @click.stop>

        <p class="modal__content__header"> Добавление пользователя </p>
        <div class="modal__warning" v-if="showWarning">Вы не заполнили поля!</div>

        <div class="modal__content-row" >
            <p class="input__header">Имя</p>
            <input class="input__content" type="text" v-model="user.name">
        </div>

        <div class="modal__content-row" >
            <p class="input__header">Телефон</p>
            <input class="input__content" type="number" v-model="user.number">
        </div>

        <div class="modal__content-row" >
            <p class="input__header">Начальник</p>

            <select class="input__content" ref="select" @change="setBoss()" >
                <option selected></option>
                <option 
                    v-for="item in userList" 
                    :key="item.number" 
                    :value="item.name"
                    class="input__content__item"
                >
                    {{ item.name }}
                </option>
            </select>
        </div>

        <div class="modal__content-row btns" >
            <button class="button" @click="addUser()">Добавить</button>
            <button class="button exit" @click="closeAddUserModal()"> Отмена </button>
        </div>
        
    </div>

  </div>
</template>

<script>
export default {
    name: 'AddUserModal',

    props: {
        userList: Array
    },

    data () {
        return {
            showWarning: false,
            user: {
                name: null,
                number: null, 
                child: null,
                boss: null
            }
        }
    },

    methods: {
        closeAddUserModal(){
            this.$emit('setShowAddUserModal')
        },
        addUser(){
            if (!this.user.name && !this.user.number){
                this.showWarning = true
            } else {
                this.showWarning = false
                this.$emit('addNewUser', this.user)
                this.$emit('setShowAddUserModal')
            }
        },
        setBoss(){
            this.user.boss = this.$refs.select.value;
            this.user.child = true;
        }
    }
}
</script>

<style>
.modal{
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
    background: rgba(0,0,0, 0.5);
    position: fixed;
    display: flex;
}
.modal__warning{
    background-color: #ffb8bd;
    padding: 1.5rem;
    border-radius: 1rem;
    margin-bottom: 1rem;
}

.modal__content{
    margin: auto;
    background: white;
    padding: 2rem 3rem;
    border-radius:0.3rem;
    width: 40%;
}
.modal__content__header{
    text-align: start;
}
.modal__content-row{
    display: flex;
    justify-content: space-between;
}
.btns{
    justify-content: start;
}

.input__header{
    color: #0F7173;
    font-weight: bold;
}
.input__content{
    width: 60%;
    height: 1.5rem;
    margin-top: 2%;
}
.input__content__item{
    padding: 1rem;
}

.button{
    margin-top: 2rem;
    padding: 1rem;
    width: 30%;
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
.exit{
    width: 20%;
    background-color: #fff;
    color: #439A86;
}
.exit:hover{
    background-color: #fff;
}
</style>
