<template>
    <div class="nav">
        <router-link to="/" >Home</router-link>
        <router-link to="/add">Add Restaurant</router-link>
        <a href="#" v-on:click="logout">Logout</a>
    </div>
</template>

<script>

    export default {
    name: "HeadEr",
    methods: {
        logout() {
            // alert("logout")
            localStorage.clear();
            this.$router.push({ name: 'Login' });
        }
    }
}
</script>

<style>
    div.nav{
        background-color: #333;
        overflow: hidden;
    }
    div.nav > a {
        float: left;
        color: #f2f2f2f2;
        padding: 14px 16px;
        text-align: center;
        font-size: 17px;
        text-decoration: none;
        margin-right: 5px;
    }
    div.nav > a:hover{
        background-color: #ddd;
        color: #333;
    }
</style>