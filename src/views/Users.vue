<template>
    <div>
        <h1>Painel Adm</h1>
        <div>
            
        </div>

        <table class="table">
            <thead>
                <tr>
                    <th>Nome</th>
                    <th>E-mail</th>
                    <th>Cargo</th>
                    <th>Ações</th>            
                </tr>
            </thead>
            <tbody>
                <tr v-for="user in users" :key="user.id">
                    <td>{{ user.name }}</td>
                    <td>{{ user.email }}</td>
                    <td>{{ getRole(user.role) }}</td>
                    <td>
                        <button class="button is-success">Editar</button> |
                        <button class="button is-danger">Deletar</button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: 'UsersAdmin',
    created(){
        var req = {
            headers: {
                Authorization: "Bearer " + localStorage.getItem('token')
            }
        }

        axios.get('http://localhost:8686/user', req).then(res => {
            console.log(res);
            this.users = res.data;
        }).catch(error => {
            console.log(error);
        })
    },
    data(){
        return{
            users: []
        }
    },
    methods: {
        getRole(role) {
            if(role === 0) {
                return "Usuário";
            } else if(role === 1) {
                return "Admin";
            } else {
                return "Outro";
            }
        }
    }
}
</script>

<style scoped>

</style>