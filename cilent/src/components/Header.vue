<h1>Lavalamp CSS Menu</h1>
<template>
<div >
        <h1> CATEGORIES OF BOOKS </h1> 
  <nav class="menu">
  <ol>
    <li class="menu-item"><router-link :to="{ name: 'blogs' }">BOOKS</router-link></li>
    <li class="menu-item"><router-link :to="{ name: 'comments' } " >SELL BOOK</router-link></li>
    <li class="menu-item">
      <router-link :to="{ name: 'users' } ">USERS</router-link>
    </li>
    <li class="menu-item">
     <router-link :to="{ name: 'login' }">LOGIN</router-link>
    </li>
    <li class="menu-item"><a v-on:click.prevent="logout" href="#" >LOGOUT</a></li>
  </ol>
</nav>
</div>
</template>
<style>
html {
  background: linear-gradient(45deg, #4F9CAD, #4F9CAD);
  height: 100vh;
  margin: 0;
  background-attachment: fixed;
}
</style>
<script>
export default {
  methods:{
    logout () {
      this.$store.dispatch('setToken', null)
      this.$store.dispatch('setUser', null)
      this.$router.push({
         name: 'login'
      })
    }
  }
}
</script>
<style scoped>

h1 {
	text-align: center;
	margin: 40px 0 40px;
	text-align: center;
	font-size: 30px;
	color: #ecf0f1;
	text-shadow: 2px 2px 4px #000000;
	font-family: 'Cherry Swash', cursive;
}
.menu {
    background: #1D464F;
    height: 4rem;
  }
  .menu ol {
    list-style-type: none;
    margin: 0 auto;
    padding: 0;
  }
  .menu > ol {
    max-width: 1000px;
    padding: 0 2rem;
    display: flex;
  }
  .menu > ol > .menu-item {
    flex: 1;
    padding: 0.75rem 0;
  }
  .menu > ol > .menu-item:after {
    content: "";
    position: absolute;
    width: 4px;
    height: 4px;
    border-radius: 50%;
    bottom: 5px;
    left: calc(50% - 2px);
    background: #FECEAB;
    will-change: transform;
    transform: scale(0);
    transition: transform 0.2s ease;
  }
  .menu > ol > .menu-item:hover:after {
    transform: scale(1);
  }
  .menu-item {
    position: relative;
    line-height: 2.5rem;
    text-align: center;
  }
  .menu-item a {
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
    display: block;
    color: #ffffff;
  }
  .sub-menu .menu-item {
    padding: 0.75rem 0;
    background: #F67280;
    opacity: 0;
    transform-origin: bottom;
    animation: enter 0.2s ease forwards;
  }
  .sub-menu .menu-item:nth-child(1) {
    animation-duration: 0.2s;
    animation-delay: 0s;
  }
  .sub-menu .menu-item:nth-child(2) {
    animation-duration: 0.3s;
    animation-delay: 0.1s;
  }
  .sub-menu .menu-item:nth-child(3) {
    animation-duration: 0.4s;
    animation-delay: 0.2s;
  }
  .sub-menu .menu-item:hover {
    background: #F8B195;
  }
  .sub-menu .menu-item a {
    padding: 0 0.75rem;
  }
  @media screen and (max-width: 600px) {
    .sub-menu .menu-item {
      background: #C06C84;
    }
  }
  
  @media screen and (max-width: 600px) {
    .menu {
      position: relative;
    }
    .menu:after {
      content: "";
      position: absolute;
      top: calc(50% - 2px);
      right: 1rem;
      width: 30px;
      height: 4px;
      background: #FFF;
      box-shadow: 0 10px #FFF, 0 -10px #FFF;
    }
    .menu > ol {
      display: none;
      background: #F67280;
      flex-direction: column;
      justify-content: center;
      height: 100vh;
      animation: fade 0.2s ease-out;
    }
    .menu > ol > .menu-item {
      flex: 0;
      opacity: 0;
      animation: enter 0.3s ease-out forwards;
    }
    .menu > ol > .menu-item:nth-child(1) {
      animation-delay: 0s;
    }
    .menu > ol > .menu-item:nth-child(2) {
      animation-delay: 0.1s;
    }
    .menu > ol > .menu-item:nth-child(3) {
      animation-delay: 0.2s;
    }
    .menu > ol > .menu-item:nth-child(4) {
      animation-delay: 0.3s;
    }
    .menu > ol > .menu-item:nth-child(5) {
      animation-delay: 0.4s;
    }
    .menu > ol > .menu-item + .menu-item {
      margin-top: 0.75rem;
    }
    .menu > ol > .menu-item:after {
      left: auto;
      right: 1rem;
      bottom: calc(50% - 2px);
    }
    .menu > ol > .menu-item:hover {
      z-index: 1;
    }
    .menu:hover > ol {
      display: flex;
    }
    .menu:hover:after {
      box-shadow: none;
    }
  }
  
  .sub-menu {
    position: absolute;
    width: 100%;
    top: 100%;
    left: 0;
    display: none;
    z-index: 1;
  }
  .menu-item:hover > .sub-menu {
    display: block;
  }
  
  @media screen and (max-width: 600px) {
    .sub-menu {
      width: 100vw;
      left: -2rem;
      top: 50%;
      transform: translateY(-50%);
    }
  }
  
  html, body {
    font-size: 16px;
    font-family: "Fira Mono", monospace;
    margin: 0;
    background: #2A363B;
  }
  
  * {
    box-sizing: border-box;
  }
  *:before, *:after {
    box-sizing: inherit;
  }
  
  a {
    text-decoration: none;
  }
  
  @keyframes enter {
    from {
      opacity: 0;
      transform: scaleY(0.98) translateY(10px);
    }
    to {
      opacity: 1;
      transform: none;
    }
  }
  @keyframes fade {
    from {
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }

</style scoped>