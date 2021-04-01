<template>
    <div>
        <h2>Registro de Usuário!</h2>
        <hr>

        <div class="columns is-centered">
            <div class="column is-half">
                <div v-if="error != undefined">
                    <div class="notification is-danger">
                        <p>{{error}}</p>
                    </div>
                </div>
                <p>Nome</p>
                <input id="name" type="text" placeholder="Nome do Usuário" class="input" v-model="name"> 
                <p>Email</p>
                <input type="email" id="email" placeholder="exemplo@email.com" class="input" v-model="email">
                <p>Senha</p>
                <input type="password" id="password" placeholder="**********" class="input" v-model="password">
                <hr>
                <button class="button is-success" @click="register">Cadastrar</button>
            </div>    
        </div>        
    </div>
</template>

<script>
import axios from 'axios';
export default{
    data(){
        return {
            name: '',
            password: '',
            email: '',
            error: undefined
        }
    },
    methods: {
        register(){
            axios.post("http://localhost:8787/user",{
                name: this.name,
                password: this.password,
                email: this.email
            }).then(res => {
                console.log(res);
                this.$router.push({name: 'Home'}) //redireciona para outra rota
            }).catch(err => {
                var msgErro = err.response.data.err;
                this.error = msgErro;
            })
        }
    }
    
}
</script>

<style scoped>

</style>
