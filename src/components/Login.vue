<template>
    <div>
        <img class="logo" src="../assets/resto-logo.png" alt="">
        <h1>Login</h1>
        <div class="login">
            <input type="text" placeholder="email" v-model="email" name="email">
            <input type="password" placeholder="password" v-model="password" name="password">
            <button v-on:click="login">Login</button>
            <p>
                <router-link to="/sign-up">Sign Up</router-link>
            </p>
        </div>
    </div>
</template>
<script>
import axios from 'axios'
export default {
    name: "LogIn",
    data() {
        return {
            email: "",
            password: ""
        }
    },
    methods:{
        async login(){
            let result=await axios.get(
                `http://localhost:3000/users?email=${this.email}&password=${this.password}`
            )
            if (result.status==200 && result.data.length>0) {
                localStorage.setItem("user-info",JSON.stringify(result.data[0]));
                this.$router.push({name:'HomePage'})
            }
        }
    },
    mounted(){
        let user=localStorage.getItem('user-info')
        if (user) {
            this.$router.push({name:'HomePage'})
        }
    }
}
</script>
 