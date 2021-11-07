<template>
<div>
	<div class="container">
    <div class="row">
        <div class="col-md-6">
            <div class="tab" role="tabpanel">
                <div class="tab-content tabs">
                    <div role="tabpanel" class="tab-pane fade in active" id="Section1">
                        <h2>ข้อมูลหนังสือ</h2>
                            <p>ชื่อเรื่อง: {{ blog.title }}</p>
							<p>ติดต่อ: {{ blog.category }}</p>
		    				<p>ราคา: {{ blog.status }} บาท</p>
            				<p>รูปภาพ: {{ blog.content }}</p>
			    <p>
				    <vue-ckeditor
					v-model.lazy="blog.content"
					:config="config" 
					@blur="onBlur($event)"
					@focus="onFocus($event)"
				/>
			    </p>
					<center><div class="button" v-on:click="navigateTo('/blogs')" >กลับ </div></center>
		    	
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
</div>
</template>

<script>
import BlogsService from "@/services/BlogsService";
import VueCkeditor from 'vue-ckeditor2'

export default {
	data() {
		return {
			blog: {
				title: "",
				thumbnail: "null",
				pictures: "null",
				content: "",
				category: "",
				comment: "",
				status: "",
			},

		    config:{
			    toolbar: [
				    {
				        name: "document",
				        items: [
						    "Source",
						    "-",
						    "Save",
						    "NewPage",
						    "Preview",
						    "Print",
						    "-",
						    "Templates",
					    ],
				    },

				    {
					    name: "clipboard",
					    items: [
						    "Cut",
						    "Copy",
						    "Paste",
					     	"PasteText",
					    	"PasteFromWord",
					    	"-",
						    "Undo",
						    "Redo",
					    ],
				    },

				    {
					    name: "editing",
					    items: ["Find", "Replace", "-", "SelectAll", "-", "Scayt"],
				    },

					{
						name: "forms",
						items: [
							"Form",
							"Checkbox",
							"Radio",
							"TextField",
							"Textarea",
							"Select",
							"Button",
							"ImageButton",
							"HiddenField",
						],
					},
					"/",

					{
						name: "basicstyles",
						items: [
							"Bold",
							"Italic",
							"Underline",
							"Strike",
							"Subscript",
							"Superscript",
							"-",
							"CopyFormatting",
							"RemoveFormat",
						],
					},

					{
						name: "paragraph",
						items: [
							"NumberedList",
							"BulletedList",
							"-",
							"Outdent",
							"Indent",
							"-",
							"Blockquote",
							"CreateDiv",
							"-",
							"JustifyLeft",
							"JustifyCenter",
							"JustifyRight",
							"JustifyBlock",
							"-",
							"BidiLtr",
							"BidiRtl",
							"Language",
						],
					},
					{ name: "links", items: ["Link", "Unlink", "Anchor"] },

					{
						name: "insert",
						items: [
							"Image",
							"Flash",
							"Table",
							"HorizontalRule",
							"Smiley",
							"SpecialChar",
							"PageBreak",
							"Iframe",
							"InsertPre",
						],
					},
					"/",
					{ name: "styles", items: ["Styles", "Format", "Font", "FontSize"] },
					{ name: "colors", items: ["TextColor", "BGColor"] },
					{ name: "tools", items: ["Maximize", "ShowBlocks"] },
					{ name: "about", items: ["About"] },
				],
				height: 300
			}
		};
	},

	async created() {
		try {
			let blogId = this.$route.params.blogId;
			this.blog = (await BlogsService.show(blogId)).data;
		}catch (error) {
			console.log(error);
		}
	},

	methods: {
		navigateTo(route) {
			this.$router.push(route);
		},

        async editBlog() {
			try {
				await BlogsService.put(this.blog);
				this.$router.push({
					name: "blogs",
				});
			}catch (err) {
				console.log(err);
			}
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
	},

	components:{
		VueCkeditor
	}	
};
</script>

<style scoped>

.tab .tab-content{
    padding: 15px;
    margin-top: 20px;
    background: #feefad;
    border-radius: 20px;
    font-size: 15px;
    color: rgb(0, 0, 0);
    line-height: 25px;
    border: 7px dashed #e87eab;
    letter-spacing: 1px;
    position: relative;
}
.tab .tab-content h2{
    font-size: 24px;
    margin-top: 0;
}
body {
  background: radial-gradient(circle, #ccffee, aquamarine);
  background-repeat: no-repeat;
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-flow: row nowrap;
  justify-content: center;
  align-items: center;
}

.button {
  font-family: "Bungee", cursive;
  font-size: 1.2rem;
  position: relative;
  text-transform: uppercase;
  font-weight: bold;
  letter-spacing: 1px;
  cursor: pointer;
  background: palevioletred;
  border: 2px solid #cb3365;
  padding: 30px 60px;
  border-radius: 45px;
  color: white;
  overflow: hidden;
  box-shadow: 0 2px 4px darkgray;
  transition: all 0.2s ease-in;
  z-index: 1;
}
.button .circle {
  position: absolute;
  border-radius: 50%;
  pointer-events: none;
  background-image: radial-gradient(circle closest-side, white, #eaadc1);
  width: 1px;
  height: 1px;
  z-index: 3;
  -webkit-animation-name: ripple;
          animation-name: ripple;
  -webkit-animation-duration: 0.5s;
          animation-duration: 0.5s;
  -webkit-animation-timing-function: ease-in;
          animation-timing-function: ease-in;
}
.button:hover {
  transform: scale(1.01);
  box-shadow: 0 6px 4px darkgray;
}

@-webkit-keyframes ripple {
  0% {
    transform: scale(0, 0);
    opacity: 0;
  }
  75% {
    transform: scale(450, 450);
    opacity: 0.75;
  }
  100% {
    transform: scale(700, 700);
    opacity: 0;
  }
}

@keyframes ripple {
  0% {
    transform: scale(0, 0);
    opacity: 0;
  }
  75% {
    transform: scale(450, 450);
    opacity: 0.75;
  }
  100% {
    transform: scale(700, 700);
    opacity: 0;
  }
}
</style>
