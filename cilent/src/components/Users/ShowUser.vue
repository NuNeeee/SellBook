<template>
    <div class="hi">
        <h2>แสดงข้อมูล</h2>
        <p>ID : {{ user.id }} </p>
        <p>Name : {{user.name}} </p>
        <p>Lastname : {{user.lastname}}</p>
        <p>Email : {{user.email}}</p>
        <p>Password : {{user.password}}</p>
        <p> 
            <button class="button1" v-on:click="navigateTo('/user/edit/'+user.id)">แก้ไขข้อมูล</button>
            <button class=" dis" v-on:click="navigateTo('/users')"> ย้อนกลับ </button> 
        </p>
    </div>
</template>

<script>
import UsersService from '@/services/UsersService'

export default {
    data() {
        return {
            user: null,
        };
    },

    async created() {
        try {
            let userId = this.$route.params.userId;
            this.user = (await UsersService.show(userId)).data
        }catch (error) {
            console.log(error);
        }
    },
    
    methods: {
       navigateTo (route) {
           this.$router.push(route)
       },
    }
};
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