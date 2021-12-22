<template>
    <Header />
    <h1>Hai {{name}}, Welcome Home Page</h1>
    <div class="main">
    <center>
    <table border="1">
        <tr>
            <th>Id</th>
            <th>Name</th>
            <th>Contact</th>
            <th>Address</th>
            <th>Actions</th>


        </tr>
        <tr v-for="item in restaurants" :key="item.id">
            <td>{{item.id}}</td>
            <td>{{item.name}}</td>
            <td>{{item.contact}}</td>
            <td>{{item.address}}</td>
            <td>
                <router-link :to="'/update/'+item.id"  class="updatelink" >Update</router-link>
                <button v-on:click="deleteRestaurant(item.id)"  class="deletebtn" >Delete</button>
            </td>
        </tr>
    </table>
    </center>
    </div>
</template>
<script>
import Header from './Header.vue'
import axios from 'axios';
export default {
   name:'Home',
   data(){
       return {
           name:'',
           restaurants:[],
        
       }
   },
   components: {
       Header,
   },
   methods:{
       async deleteRestaurant(id)
       {
        //    console.warn(id)
        let result = await axios.delete("http://localhost:3000/restaurants/"+id);
        console.warn(result)
        if(result.status==200)
        {
            this.loadData()
        }
       },
       async loadData(){
            let user = localStorage.getItem("user-info");
        this.name = JSON.parse(user)[0].name;

        if(!user)
        {
            this.$router.push({name: 'SignUp' })
        }
        let result = await axios.get("http://localhost:3000/restaurants");
        console.warn(result, "aa");
        this.restaurants=result.data;
       }

   },
   async mounted()
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
.deletebtn{

    margin-left:10px; background-color:red; color:white; border-radius:10px;font-weight:bold;border-color: red;;

}
.updatelink{
    margin-left:10px;
    appearance: auto;
    text-rendering: auto;
     color: white;
    letter-spacing: normal;
    word-spacing: normal;
    line-height: normal;
    text-transform: none;
    text-indent: 0px;
    text-shadow: none;
    display: inline-block;
    text-align: center;
    align-items: flex-start;
    cursor: default;
    box-sizing: border-box;
    background-color:#2977c7;
    margin: 0em;
    padding: 1px 6px;
    border-width: 2px;
    border-style: outset;
    border-color: none;
    border-image: initial;
}
</style>