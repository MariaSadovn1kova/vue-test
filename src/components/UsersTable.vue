<template>
  <div class="users-table">

    <div class="users-table__header">
        <div class="users-table__header__item boss">Начальник</div>
        <div class="users-table__header__item name" @click="sortName ()">Имя</div>
        <div class="users-table__header__item telephone" @click="sortNumber ()">Телефон</div>
    </div>

    <div class="users-table__content" :class="{'child': user.child}" v-for="user in userList" :key="user.number"> 
        <div class="users-table__content__item name">{{ user.boss }}</div>
        <div class="users-table__content__item name">{{ user.name }}</div>
        <div class="users-table__content__item telephone">{{ user.number }}</div>
    </div>

  </div>
</template>

<script>
export default {
    name: 'UsersTable',

    props:{
        userList: Array,
    },

    data() {
        return{
            isNameSort: false,
            isNumberSort: false,
        }

    },

    methods: {
        // Пыталась передать как параметр название столбца для сортировки
        // Но не получается передать его в метод sort
        // Поэтому пришлось создать несколько однотипных функций :С
        sortName () {
            if(!this.isNameSort){
                this.userList.sort(function (a, b) {
                    if (a.name > b.name) {
                        return 1;
                    }
                    if (a.name < b.name) {
                        return -1;
                    }
                    return 0;
                })
                this.isNameSort = !this.isNameSort
            } else {
                this.userList.sort(function (a, b) {
                    if (a.name < b.name) {
                        return 1;
                    }
                    if (a.name > b.name) {
                        return -1;
                    }
                    return 0;
                })
                this.isNameSort = !this.isNameSort
            }
        },
        sortNumber () {
            if(!this.isNumberSort){
                this.userList.sort(function (a, b) {
                    if (a.number > b.number) {
                        return 1;
                    }
                    if (a.number < b.number) {
                        return -1;
                    }
                    return 0;
                })
                this.isNumberSort = !this.isNumberSort
            } else {
                this.userList.sort(function (a, b) {
                    if (a.number < b.number) {
                        return 1;
                    }
                    if (a.number > b.number) {
                        return -1;
                    }
                    return 0;
                })
                this.isNumberSort = !this.isNumberSort
            }
        }
    }
}
</script>

<style scoped>
.users-table{
    width: 60%;
    display: flex;
    flex-direction: column;
    margin-top: 5rem;
}

.users-table__header{
    display: flex;
}
.users-table__header__item{
    padding: 0.5rem 2rem;
    text-align: center;
    color: #0F7173;
    font-weight: bold;
    border-radius: 1rem;
}
.users-table__header__item:hover{
    cursor: pointer;
    background-color: #dbecec;
}
.boss{
    width: 20%;
}
.name{
    width: 20%;
}
.telephone{
    width: 60%;
}

.users-table__content{
    background-color: #E7ECEF;
    margin-top: 0.5rem;
    display: flex;
    border-radius: 0.3rem;
    transition: 0.3s;
}
.users-table__content:hover{
    background-color: #d6dbdf;
}
.users-table__content__item{
    padding: 1rem 2rem;
    text-align: center;
}
.child{
    background-color: #BCD8C1;
}
.child:hover{
    background-color: #aac7af;
}
</style>
