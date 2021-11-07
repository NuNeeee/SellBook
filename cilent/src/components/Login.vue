<template>
    <div class="center" >
        <div class="box" >
        <h1> Login </h1>
        <form v-on:submit.prevent="onLogin">
            <p>Username: <input type="text" v-model="email" /></p>
            <p>Password: <input type="password" v-model="password" /></p>
            <center><p><button class="button" type="submit">Login </button></p></center>
            <dev class = "error" v-if="error">{{error}}</dev>
        </form>
    </div>
    </div>
</template>
<script>
import AuthenService from '@/services/AuthenService'

export default {
    data () {
        return {
            email: '',
            password: ''
        };
    },
    
    methods:{
        async onLogin () {
            try {
                const response = await AuthenService.login({
                    email: this.email,
                    password: this.password,
                    error: null
                });
                this.$store.dispatch('setToken',response.data.token)
                this.$store.dispatch('setUser',response.data.user)
                this.$router.push({
                   name: 'blogs'
                })
                console.log(response)
            }catch (error) {
                console.log(error)
                this.error = error.response.data.error
                this.email = ''
                this.password = ''
            }
        },
    },
}
</script>

<style scoped>
.box {
  background-color: lightgrey;
  margin: auto;  
   width: 30%;  
   padding: 3%;  
}
.center {
    position: absolute;
    left: 0;
    top: 32%;
    width: 100%;
    text-align: center;
    font-size: 18px;
}

.error{
    color: red;
}
.button {
  position: relative;
  display: block;
  width: 200px;
  height: 36px;
  border-radius: 18px;
  background-color: #1D464F;
  border: solid 1px transparent;
  color: #fff;
  font-size: 18px;
  font-weight: 300;
  cursor: pointer;
  transition: all 0.1s ease-in-out;
 justify-content: center;
  align-items: center;
  
}
.button:hover {
  background-color: transparent;
  border-color: #fff;
  transition: all 0.1s ease-in-out;
}

</style>
