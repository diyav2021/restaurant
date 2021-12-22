<template>
<div class="main">
<img class="logo" src="../assets/logo_144.png" alt="logo">
<h1>Sign Up</h1>   
<div class="register">
    <input type="text" v-model="name" placeholder="Enter Name">
    <input type="email" v-model="email" placeholder="Enter Email">
    <input type="password" v-model="password" placeholder="Enter Password">
    <button v-on:click="signUp">SignUp</button>
    <p>
        <router-link to="/login">Login</router-link>
    </p>
</div>
</div>
</template>

<script>
import axios from 'axios' 
export default {
    name: 'SignUp',
    data()
    {
        return {
            name: '',
            email:'',
            password:''
        }
    },
    methods:{
        async signUp()
        {   
            let result = await axios.post("http://localhost:3000/users",{
                name:this.name,
                email: this.email,
                password: this.password
            });
            console.warn(result);
            if (result.status==201)
            {
                // alert("signup done");
                localStorage.setItem("user-info",JSON.stringify(result.data))
                this.$router.push({name: 'Home' })
            }
            // console.warn("signup", this.name, this.email, this.password)
        }
    },
    mounted(){
        let user = localStorage.getItem("user-info");
        if(user)
        {
            this.$router.push({name: 'Home' })
        }
    }
}
</script>
<style>

</style>
