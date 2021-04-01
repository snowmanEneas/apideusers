<template>
    <div>
        <h2>Edição de Usuário!</h2>
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
                <hr>
                <button class="button is-success" @click="update">Editar</button>
            </div>    
        </div>        
    </div>
</template>

<script>
import axios from 'axios';
export default{
    created(){

        var req = {
            headers: {
                Authorization: "Bearer " + localStorage.getItem('token')
            }
        }   

        axios.get("http://localhost:8787/user/" + this.$route.params.id, req).then(res => {
            console.log(res);

            this.name = res.data.name;
            this.email = res.data.email;
            this.id = res.data.id;

        }).catch(err =>{
            console.log(err.response);
            this.$router.push({name: 'Users'});
        });

    },
    data(){
        return {
            name: '',
            email: '',
            id: -1,
            error: undefined
        }
    },
    methods: {
        update(){

            var req = {
            headers: {
                Authorization: "Bearer " + localStorage.getItem('token')
            }
            }   

            axios.put("http://localhost:8787/user",req,{
                name: this.name,
                email: this.email,
                id: this.id
            }).then(res => {
                console.log(res);
                this.$router.push({name: 'Users'}) //redireciona para outra rota
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
