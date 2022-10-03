<template>
    <div>
        <HeaderPage/>
        <h1>Hello user welcome on Add Restaurant page</h1>
        <form class="add">
            <input type="text" name="name" placeholder="name" v-model="restaurant.name">
            <input type="text" name="address" placeholder="address" v-model="restaurant.address">
            <input type="text" name="contact" placeholder="contact" v-model="restaurant.contact">
            <button type="button" v-on:click="addRestaurant">Add new restaurant</button>    
        </form>
    </div>
</template>

<script> 
import HeaderPage from './Header.vue'
import axios from 'axios';
export default {
    name:"AddPage",
    components:{
        HeaderPage
    },data(){
        return{
            restaurant:{
                name:'',
                address:'',
                contact:'',

            }
        }
    },
    methods:{
        async addRestaurant(){
            // console.warn(this.restaurant);
            const result=await axios.post(`http://localhost:3000/restaurants`,{
                name:this.restaurant.name,address:this.restaurant.address,contact:this.restaurant.contact
            })
            // console.warn('result:',result);
            if (result.status==201) {
                
                this.$router.push({name:'HomePage'})
            }
        }
    },
    mounted(){
        let user=localStorage.getItem('user-info')
        if (!user) {
            this.$router.push({name:'SignUp'})
        }
    }
}
</script>