<template>
    <Header />
    <h1>Hello {{usern}}, Welcome on Update Restaurant Page</h1>
    <form class="addrest">
        <input type="text" v-model="name" name="name" placeholder="Enter name" />
        <input type="text" v-model="address" name="address" placeholder="Enter address" />
        <input type="tel" v-model="contact" name="contact" placeholder="Enter contact" />
        <button v-on:click="updaterestbtn" type="button">Update Restaurant</button>
    </form>
</template>

<script>
    import Header from './Header.vue';
    import axios from 'axios';
    export default{
        name: 'UpdatePage',
        components:{
            Header
        },
        data()
        {
            return {
                name: "",
                address: "",
                contact: "",
                usern: ""
            }
        },
        methods:{
            async updaterestbtn()
            {
                let res = await axios.put('http://localhost:3000/restaurants/'+this.$route.params.id, {
                    name: this.name,
                    contact: this.contact,
                    address: this.address
                });

                if(res.status === 200){
                    this.$router.push({name: 'Home'})
                }
            }
        },
        async mounted()
        {
            let user = localStorage.getItem('user-info');
            if(!user){
                this.$router.push({name: 'Login'})
            }
            // console.log(this.$route.params.id)
            let result = await axios.get(`http://localhost:3000/restaurants/${this.$route.params.id}`)
            this.name = result.data.name
            this.contact = result.data.contact
            this.address = result.data.address
            this.usern = JSON.parse(user).name
        }
    }
</script>