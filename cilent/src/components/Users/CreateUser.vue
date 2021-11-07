<template>
<div  class="hi" > 
    <h2>สร้างผู้ใช้งาน</h2>
    <form v-on:submit.prevent = "createUser">
        <p>Name : <input type="text" v-model="user.name"></p>
        <p>Lastname : <input type="text" v-model="user.lastname"></p>
        <p>Email : <input type="text" v-model="user.email"></p>
        <p>Password : <input type="text" v-model="user.password"></p>
        <p>
           <button class="button1" type="submit">ตกลง</button>
           <button class=" dis" v-on:click="navigateTo('/users')"> ย้อนกลับ </button> </p>
    </form>
    <hr>
    <div>
        <p>Name : {{user.name}}</p>
        <p>Lastname : {{user.lastname}}</p>
        <p>Email : {{user.email}}</p>
        <p>Password : {{user.password}}</p>
    </div>
</div>
</template>

<script>
import UsersService from '@/services/UsersService'

export default {
    data() {
        return {
            user: {
                name: '',
                lastname: '',
                email: '',
                password: '',
                status: 'active'
            }
        }
    },

    methods: {
         navigateTo (route) {
           this.$router.push(route)
       },

        async createUser() {
            try {
                await UsersService.post(this.user)
                this.$router.push({
                    name: 'users'
                })
            }catch (error) {
                console.log(error)
            }
        }
    }
}
</script>

<style scoped>

.hi {
padding: 0.4em 0.5em;
color: #494949;
background: #f4f4f4;
border-left: solid 15px #1D464F;
border-bottom: solid 10px #1D464F;
}
h2 {
padding: 0.5em;
color: #ffffff;
background: #72a094;
border-bottom: solid 20px #c7d6d2;
}
.button1 {
  background-color: #c98025; /* Green */
  border: none;
  color: white;
  padding: 10px 15px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
}

.dis {
  background-color: #c98025; /* Green */
  border: none;
  color: white;
  padding: 10px 15px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
  opacity: 0.6;
  cursor: not-allowed;
}
</style>