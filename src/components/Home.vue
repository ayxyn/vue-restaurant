<template>
    <div>
        <HeaderPage />
        <h1>Hello {{name}} welcome on home page</h1>
        <table border="1">
            <tr>
                <td>Id</td>
                <td>Name</td>
                <td>Contact</td>
                <td>Address</td>
                <td>Actions</td>
            </tr>
            <tr v-for="item in restaurant" :key=item.id>
                <td>{{item.id}}</td>
                <td>{{item.name}}</td>
                <td>{{item.contact}}</td>
                <td>{{item.address}}</td> 
                <td>
                    <router-link :to="'/update/'+item.id"> Update </router-link>
                    <a href="#" v-on:click="deleteRestaurant(item.id)"> Delete </a>
                </td>
            </tr>
        </table>
    </div>
</template>

<script>
import HeaderPage from './Header.vue'
import axios from 'axios'

export default {
    name: "HomePage",
    components: {
        HeaderPage
    },
    data() {
        return {
            name: '',
            restaurant: []
        }
    },
    methods: {
        async deleteRestaurant(resId) {
            
            const result= await axios.delete('http://localhost:3000/restaurants/' + resId);
            
            if (result.status==200) {
                this.restaurant= this.restaurant.filter((item)=>item.id!=resId)  ;
             }
        }
    },
    async mounted() {
        let user = localStorage.getItem('user-info')
        this.name = JSON.parse(user).name;
        // console.log(JSON.parse(user).name);
        if (!user) {
            this.$router.push({ name: 'SignUp' })
        }
        let result = await axios.get(`http://localhost:3000/restaurants`);
        this.restaurant = result.data;
    }
}
</script>

<style>
td {
    width: 160px;
    height: 40px;
}
</style>