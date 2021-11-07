<template>
<div class="hi">
    <div v-if="users.length">
        <h2>ผู้ใช้งานระบบ</h2>
        <h4>จำนวนผู้ใช้งาน {{users.length}}</h4>
        <p><button class="button" v-on:click="navigateTo('/user/create')">เพิ่มผู้ใช้งาน</button></p>
        <div v-for="user in users" v-bind:key="user.id">
            <p>Name : {{user.name}} </p>
            <p>Lastname : {{user.lastname}}</p>
            <p>
                <button class="button1" v-on:click="navigateTo('/user/'+user.id)">แสดงข้อมูล</button>
                <button class=" dis" v-on:click="deleteUser(user)">ลบข้อมูล</button>
            </p>
            <hr>
        </div>
    </div>
</div>
</template>

<script>
import UsersService from '@/services/UsersService'

export default {
    data(){
        return {
            users:[]
        }
    },

    async created() {
        try {
            this.users = (await UsersService.index()).data;
        }catch (error) {
            console.log(error);
        }
    },

    methods:{
        navigateTo(route){
            this.$router.push(route)
        },

        async deleteUser(user){
            let result = confirm("Want to delete")
            if(result){
                try{
                    await UsersService.delete(user)
                    this.refreshData()
                }catch(error){
                    console.log(error)
                }
            }
        },

        async refreshData () {
            this.users = (await UsersService.index()).data
        },

        logout(){
            this.$store.dispatch('setToken',null)
            this.$store.dispatch('setUser',null)
            this.$router.push({
                name: 'login'
            })
        }
    },
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
.button {
  display: inline-block;
  padding: 5px 10px ;
  font-size: 18px;
  cursor: pointer;
  text-align: center;
  text-decoration: none;
  outline: none;
  color: #fff;
  background-color: #4a402e;
  border: 5px;
  border-radius: 5px;
  box-shadow: 0 9px rgb(216, 214, 214);
}

.button:hover {background-color: #4a402e}

.button:active {
  background-color: #4a402e;
  box-shadow: 0 5px #666;
  transform: translateY(4px);
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