<template>
    <div>
        <h2>Edição de usuário</h2>
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

                <p>Nome</p>
                <input type="text" class="input" placeholder="Nome do usuário" v-model="name">
                <p>E-mail</p>
                <input type="email" class="input" placeholder="email@email.com" v-model="email">

                <br><br>
                <button class="button is-success" @click="update()">Editar</button>

            </div>
        </div>

        
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'RegistroComponent',
    created(){
        var req = {
            headers: {
                Authorization: "Bearer " + localStorage.getItem('token')
            }
        }

        axios.get("http://localhost:8686/user/" + this.$route.params.id, req).then(res => {
            console.log(res);

            this.id = res.data.id;
            this.email = res.data.email;
            this.name = res.data.name;
        }).catch(error => {
            console.log(error.response);
            this.$router.push({name: 'Users'})
        })
    },
    data(){
        return{
            name: '',
            email: '',
            id: -1,
            error: undefined,
            success: undefined
        }
    },
    methods: {
        update(){
            var req = {
                headers: {
                    Authorization: "Bearer " + localStorage.getItem('token')
                }
            }

            axios.put("http://localhost:8686/user", {
                name: this.name,
                email: this.email,
                id: this.id
            }, req).then(res => {
                console.log(res)
                this.$router.push({name: 'Users'})
            }).catch(error => {
                console.log(error)
                var msgErro = error.response.data.error;
                this.error = msgErro;
            })

        }
    }
}
</script>

<style scoped>

</style>