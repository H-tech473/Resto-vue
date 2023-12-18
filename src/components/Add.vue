<template>
    <Header />
    <h1>Hello {{usern}}, Welcome on Add Restaurant Page</h1>
    <form class="addrest">
        <input type="text" v-model="restaurant.name" name="name" placeholder="Enter name" />
        <input type="text" v-model="restaurant.address" name="address" placeholder="Enter address" />
        <input type="tel" v-model="restaurant.contact" name="contact" placeholder="Enter contact" />
        <button v-on:click="addrestbtn" type="button">Add Restaurant</button>
    </form>
</template>

<script>
    import Header from './Header.vue';
    import axios from 'axios';
    export default{
        name: 'AddPage',
        components:{
            Header
        },
        data()
        {
            return{
                restaurant: {
                    name: "",
                    contact: "",
                    address: ""
                },
                usern: ""
            }
        },
        methods:
        {
            async addrestbtn()
            {
                let res = await axios.post('http://localhost:3000/restaurants', {
                    name: this.restaurant.name,
                    contact: this.restaurant.contact,
                    address: this.restaurant.address
                });

                if(res.status === 201){
                    this.$router.push({name: 'Home'})
                }

            }
        }
        ,
        mounted()
        {
            let user = localStorage.getItem('user-info');
            if(!user){
                this.$router.push({name: 'Login'})
            }
            this.usern = JSON.parse(user).name
        }
    }
</script>