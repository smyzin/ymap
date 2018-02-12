<template>
    <div id="app">
        <!--<img src="./assets/logo.png">-->
        <div class="hello">
            <h1>Модальное окно для земельных объектов</h1>
            <h2>Кликните на кнопку ниже, чтобы открыть модальное окно</h2>

            <button class="button button__modal" title="Редактировать" @click="openModalWindow(3)">
                <i class="mdi mdi-pencil"></i>
                Редактировать
            </button>
            <modal v-if="openModal" @save="sendData" @close="closeModalWindow"/>
        </div>
    </div>
</template>

<script>
    import modal from './components/modal.vue'

    export default {
    name: 'App',
    components: { modal },
    data () {
        return {
            openModal: false,
            objectID: null,
        }
    },
    methods:{
        sendData(value){
            console.info(value);
            this.openModal = !this.openModal;
        },
        openModalWindow(id) {
            this.openModal = !this.openModal;
            this.objectID = id;
        },
        closeModalWindow() {
            this.openModal = !this.openModal;
        }
    }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css?family=Open+Sans:300,400,700&subset=cyrillic');

#app {
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}

.button{
    background: none;
    border: none;
    outline: none;
    font-size: 18px;
    font-weight: 400;
    font-family: 'Open Sans', sans-serif;
    cursor: pointer;
}
.button__modal{
    border: 2px solid #939496;
    border-radius: 4px;
    padding: 15px 22px;
}
h1, h2 {
    font-weight: normal;
}
a {
    color: #42b983;
}
</style>
