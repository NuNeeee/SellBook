<template>
    <div v-if="users.length"><center>
        <div class="hi">
            <h2> หนังสือนิยาย และวรรณกรรมต่างๆ </h2>
            <!-- <p><button v-on:click="logout"> Logout </button></p> -->
            <div class="wrapper">
                <a v-on:click="navigateTo('/blog/create')"><span>ขายหนังสือ</span></a>

            <div v-for="blog in blogs" v-bind:key="blog.id"></div> 
            </div>     
        </div> </center>
    </div>
</template>

<script>
import BlogsService from '@/services/BlogsService'
import UsersService from '@/services/UsersService'
import CommentsService from '@/services/CommentsService'

export default {
    data () {
        return { 
            blogs: []
        }
    },

    data () {
        return{
            users: []
        }      
    },

    async created () {
        this.blogs = (await BlogsService.index()).data
    },

    async created() {
        try {
            this.users = (await UsersService.index()).data;
        }catch (error) {
            console.log(error);
        }
    },

    methods: {
        logout () {
            this.$store.dispatch('setToken', null)
            this.$store.dispatch('setBlog', null)
            this.$router.push({
                name: 'login'
            })
        },

        navigateTo (route) {
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

        async deleteBlog (blog) {
            let result = confirm("Want to delete?")
            if (result) {
                try {
                    await BlogsService.delete(blog)
                    this.refreshData()
                }catch (err) {
                    console.log(err)
                }
            }
        },

        async refreshData () {
            this.users = (await UsersService.index()).data
        },

        async refreshData() {
            this.blogs = (await BlogsService.index()).data
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

a{
  display: block;
  width: 200px;
  height: 40px;
  line-height: 40px;
  font-size: 18px;
  font-family: sans-serif;
  text-decoration: none;
  color: #333;
  border: 2px solid rgb(0, 0, 0);
  letter-spacing: 2px;
  text-align: center;
  position: relative;
  transition: all .35s;
}

a span{
  position: relative;
  z-index: 2;
}

a:after{
  position: absolute;
  content: "";
  top: 0;
  left: 0;
  width: 0;
  height: 100%;
  background: #4F9CAD;
  transition: all .35s;
}

a:hover{
  color: #fff;
}

a:hover:after{
  width: 100%;
}
</style>