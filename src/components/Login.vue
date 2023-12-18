<template>
    <img class="logo" src="../assets/signupimg.png" alt="">
    <h1>Login</h1>
    <div class="login">
        <input type="text" v-model="name" placeholder="Enter Name">
        <input type="password" v-model="password" placeholder="Enter Password">
        <button v-on:click="login">Login</button>
        <p>
            <router-link to="/sign-up">Sign Up</router-link>
        </p>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: "LoginPg",
    data()
    {
        return {
            name: "",
            password: ""
        }
    },
    methods:{
        async login()
        {
            // console.log(this.name, this.password);
            let result = await axios.get(`http://localhost:3000/user?name=${this.name}&password=${this.password}`)

            if(result.data[0])
            {
                localStorage.setItem('user-info', JSON.stringify(result.data[0]))
                this.$router.push({name: 'Home'})
            }
        }
    },
    mounted()
    {
        let user= localStorage.getItem('user-info');
            if(user){
                this.$router.push({name: 'Home'})
            }
    }
}
</script>

<style>

</style>