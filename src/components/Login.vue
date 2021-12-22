<template>
<div class="main">
<img class="logo" src="../assets/logo_144.png" alt="logo">
<h1>Login</h1>   
<div class="login">
    <input type="email" v-model="email" placeholder="Enter Email">
    <input type="password" v-model="password" placeholder="Enter Password">
    <button v-on:click="login">Login</button>
    <p>
        <router-link to="/sign-up">Sign Up</router-link>
    </p>
</div>
</div>
</template>

<script>
import axios from 'axios'
export default {
    name:"Login",
    data()
    { 
    return {
        email:'',
        password:''
    }

    },
    methods:{
        async login(){
            let result = await axios.get(
                `http://localhost:3000/users?email=${this.email}&password=${this.password}`
            ) 
             if (result.status==200 && result.data.length >0)
            {
                // alert("signup done");
                localStorage.setItem("user-info",JSON.stringify(result.data))
                this.$router.push({name: 'Home' })
            }
            console.warn(result)

            // console.warn(this.email,this.password)
        }

    },
    mounted(){
        let user = localStorage.getItem("user-info");
        if(user)
        {
            this.$router.push({name: 'Home' })
        }
    }

};
</script>
