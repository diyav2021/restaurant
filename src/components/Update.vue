<template>
    <Header />
    <h1>Hai {{name}}, Welcome on Update Restaurant Page</h1>
    <div class="main">
    <form class="add">
        <input type="text" v-model="Restaurants.name" name="name" id="" placeholder="Name">
        <input type="text" v-model="Restaurants.address" name="address" id="" placeholder="Address" >
        <input type="text" v-model="Restaurants.contact" name="contact" id="" placeholder="Contact" >
        <button type="button" v-on:click="updateRestaurant" > Update Restaurant</button>

    </form>
    </div>
</template>
<script>
import Header from './Header.vue'
import axios from 'axios'
export default {
   name:"Update",
   components: {
       Header,
   },
   data(){
       return {
           name:'',
           Restaurants:{
               name:'',
               address:'',
               contact:''
           }
       }
   },
   methods:{
       async updateRestaurant(){
           console.warn(this.Restaurants)
           const result= await axios.put("http://localhost:3000/restaurants/"+this.$route.params.id,{
               name:this.Restaurants.name,
               address:this.Restaurants.address,
               contact:this.Restaurants.contact,

           });
           if(result.status==200){
               this.$router.push({name: 'Home'})
           }
       }
   },
   async mounted(){
        let user = localStorage.getItem("user-info");
        this.name = JSON.parse(user)[0].name;

        if(!user)
        {
            this.$router.push({name: 'SignUp' })
        }
       
        const result = await axios.get("http://localhost:3000/restaurants/"+this.$route.params.id);
        //  console.warn(this.$route.params.id)
        console.warn(result.data)
        this.Restaurants=result.data
    }
}
</script>
