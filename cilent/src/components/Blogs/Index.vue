<template>
    <div class="hi">
        <h2> หนังสือนิยาย และวรรณกรรมต่างๆ </h2>
        <!-- <p><button v-on:click="logout"> Logout </button></p> -->
        <h4> จำนวนหนังสือ {{blogs.length}} เล่ม</h4>
        <div v-for="blog in blogs" v-bind:key="blog.id">
            <p>ชื่อเรื่อง: {{ blog.title }} </p>
            <p>ติดต่อ: {{ blog.category }} </p>
            <p>ราคา: {{ blog.status }} บาท</p>
            <p>
              <button class="submit-button state-0" v-on:click="navigateTo('/blog/'+ blog.id)"> แสดงข้อมูล </button> 
            </p>
            <hr>
            </div>
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
        return{
            comments: []
        }
         return{
            users: []
        }
    },
    
    async created () {
        this.blogs = (await BlogsService.index()).data
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

.submit-button {
  display: block;
  font-family: "Open Sans", Helvetica, Arial, sans-serif;
  font-weight: 600;
  text-transform: uppercase;
  font-size: 0.75em;
  letter-spacing: 1px;
  height: 38px;
  width: 120px;
  line-height: 38px;
  overflow: hidden;
  background: #c98025;
  border-radius: 3px;
  box-shadow: 0 15px 30px rgba(white, 0.1);
  border: 0;
  cursor: pointer;
  transition: all 0.3s ease;
  color: #ffffff;
}

</style>