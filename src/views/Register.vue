<template>
    <div>
        <h2>Registro de usuário</h2>
        <hr>


        <div class="columns is-mobile is-centered">
            <div class="column is-half">
                <p>Nome</p>
                <input type="text" class="input" placeholder="Nome do usuário" v-model="name">
                <p>E-mail</p>
                <input type="email" class="input" placeholder="email@email.com" v-model="email">
                <p>Senha</p>
                <input type="password" class="input" placeholder="*********" v-model="password">
                <br><br>
                <button class="button is-success" @click="register()">Cadastrar</button>

            </div>
        </div>

        
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'RegistroComponent',
    data(){
        return{
            name: '',
            password: '',
            email: ''
        }
    },
    methods: {
        register(){
            axios.post("http://localhost:8686/user", {
                name: this.name,
                email: this.email,
                password: this.password
            }).then(res => {
                console.log(res)
            }).catch(error => {
                console.log(error.response)
            })

        }
    }
}
</script>

<style scoped>

</style>