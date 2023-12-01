<template>
    <div>
        <h2>Login</h2>
        <hr>

        <div class="columns is-mobile is-centered">
            <div class="column is-half">
                <div v-if="error != undefined">
                    <div class="notification is-danger">
                        <p>{{ error }}</p>
                    </div>
                </div>
                <div v-else-if="success">
                    <div class="notification is-success">
                        <p>{{ success }}</p>
                    </div>
                </div>

                <p>E-mail</p>
                <input type="email" class="input" placeholder="email@email.com" v-model="email">
                <p>Senha</p>
                <input type="password" class="input" placeholder="*********" v-model="password">
                <br><br>
                <button class="button is-success" @click="login()">Logar</button>

            </div>
        </div>

    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'LoginComponent',
    data(){
        return{
            password: '',
            email: '',
            error: undefined,
            success: undefined
        }
    },
    methods: {
        login(){
            axios.post("http://localhost:8686/login", {
                password: this.password,
                email: this.email
            }).then(res => {
                console.log(res.data.token)
                localStorage.setItem('token', res.data.token);
                this.$router.push({name: 'home'})
                
                // var msgSuccess = 'Login efetuado com sucesso!'
                // this.success = msgSuccess;
            }).catch(error => {
                console.log(error)
                var msgErro = error.response.data.error;
                this.error = msgErro;
            })
        }
    },

}
</script>

<style scoped>

</style>