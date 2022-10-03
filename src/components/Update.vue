<template>
    <div>
        <HeaderPage />
        <h1>Hello user welcome on Update Restaurant page</h1>
        <form class="add">
            <input type="text" name="id" placeholder="id" v-model="restaurant.id">
            <input type="text" name="name" placeholder="name" v-model="restaurant.name">
            <input type="text" name="address" placeholder="address" v-model="restaurant.address">
            <input type="text" name="contact" placeholder="contact" v-model="restaurant.contact">
            <button type="button" v-on:click="updateRestaurant">Update restaurant</button>
        </form>
    </div>
</template>

<script>
import HeaderPage from './Header.vue'
import axios from 'axios'

export default {
    name: "UpdatePage",
    components: {
        HeaderPage
    }, data() {
        return {
            restaurant: {
                id:'',
                name: '',
                address: '',
                contact: '',
            }
        }
    }, methods: {
        async updateRestaurant(){
            const result=await axios.put(`http://localhost:3000/restaurants/${this.restaurant.id}`,{
                name:this.restaurant.name,address:this.restaurant.address,contact:this.restaurant.contact
            })
             if (result.status==200) {
                
                this.$router.push({name:'HomePage'})
            }
        }
    },
    async mounted() {
        let user = localStorage.getItem('user-info')
        if (!user) {
            this.$router.push({ name: 'SignUp' })
        } 
        const result=await axios.get(`http://localhost:3000/restaurants/${this.$route.params.id}`);
        this.restaurant=result.data;
    }
}
</script>