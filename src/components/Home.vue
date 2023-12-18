<template>
    <Header />
    <h1>Hello {{name}}, Welcome on Home Page</h1>
    <table border="1">
        <tr>
            <td>Id</td>
            <td>Name</td>
            <td>Contact</td>
            <td>Address</td>
        </tr>
        <tr v-for="item in restaurant" :key="item.id">
            <td>{{ item.id }}</td>
            <td>{{ item.name }}</td>
            <td>{{ item.contact }}</td>
            <td>{{ item.address }}</td>
            <td>
                <router-link :to="'/update/'+item.id">Update</router-link>
                <button type="button" v-on:click="deleteitem(item.id)">Delete</button>
            </td>
        </tr>
    </table>
</template>

<script>
    import Header from './Header.vue';
    import axios from 'axios';
    export default{
        name: 'HomePage',
        data(){
            return {
                name: "",
                restaurant: []
            }
        },
        components:{
            Header
        },
        methods:{
            async deleteitem(id)
            {
                let result = await axios.delete(`http://localhost:3000/restaurants/${id}`)
                if(result.status === 200){
                    this.loadData();
                }
            },
            async loadData()
            {
                let user = localStorage.getItem('user-info');
                this.name = JSON.parse(user).name
                if(!user){
                    this.$router.push({name: 'Login'})
                }
                let result = await axios.get('http://localhost:3000/restaurants');
                this.restaurant = result.data;
            }
        },
        mounted()
        {
            this.loadData();
        }
    }
</script>

<style>
    td{
        width: 160px;
        height: 40px;
    }
</style>