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
                        <button class="button is-danger" @click="showModalMethod(user.id)">Deletar</button>
                    </td>
                </tr>
            </tbody>
        </table>

        <div :class="{modal: true, 'is-active': showModal}">
            <div class="modal-background"></div>
            <div class="modal-content">
                <div class="card">
                    <header class="card-header">
                        <p class="card-header-title">
                        Deseja realmente deletar esse usuário?
                        </p>
                    </header>
                    <!-- <div class="card-content">
                        <div class="content">
                            
                        </div>
                    </div> -->
                    <footer class="card-footer">
                        <a href="#" class="card-footer-item" @click="hideModal()">Cancelar</a>
                        <a href="#" class="card-footer-item">Deletar</a>
                    </footer>
                </div>
            </div>
            <button class="modal-close is-large" aria-label="close" @click="hideModal()"></button>
        </div>
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
            users: [],
            showModal: false
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
        },
        hideModal(){
            this.showModal = false;
        },
        showModalMethod(id){
            console.log(id)
            this.showModal = true;
        }
    }
}
</script>

<style scoped>

</style>