<template>
    <Header />
    <h1>Hai User, Welcome on Add Restaurant Page</h1>
    <div class="main">
    <form class="add">
        <input type="text" v-model="Restaurants.name" name="name" id="" placeholder="Name">
        <input type="text" v-model="Restaurants.address" name="address" id="" placeholder="Address" >
        <input type="text" v-model="Restaurants.contact" name="contact" id="" placeholder="Contact" >
        <button type="button" v-on:click="addRestaurant"> Add New Restaurant</button>

    </form>
    </div>
</template>
<script>
import axios from 'axios'
import Header from './Header.vue'

export default {
   name:"Add",
   components: {
       Header,
   },
   data(){
       return {
        //    name:'',
           Restaurants:{
               name:'',
               address:'',
               contact:''
           }
       }
   },
   methods:{
       async addRestaurant(){
           console.warn(this.Restaurants)
           const result= await axios.post("http://localhost:3000/restaurants",{
               name:this.Restaurants.name,
               address:this.Restaurants.address,
               contact:this.Restaurants.contact,

           });
           if(result.status==201){
               this.$router.push({name: 'Home'})
           }
           console.warn("result", result);
       }
   },
   mounted(){

        let user = localStorage.getItem("user-info");
        // this.name = JSON.parse(user)[0].name;

        
        if(!user)
        {
            this.$router.push({name: 'SignUp' })
        }
    }
}
</script>
