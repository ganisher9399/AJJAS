<template>
  <header>
    <div class="container">
        <nav class="navbar">

           <ul class="menu" v-if="!isMobile">
               <li class="menu-item " v-for="(item, ind) in menuArray" :key="item.text"  >
                  <a :href="item.link" class="link" @click="foo(ind)" >{{ item.text }}</a>
               </li>
           </ul>

           <div :class="['logo', { dark: isOpen }]">
              <img :src="logoImage" alt="logo" class="logo-image">
           </div>

            <div class="burger-box">

              <div class="burger-auth" v-if="isMobile"  @click="$router.push({ name: 'Login'})">
                <i class="fas fa-sign-in"></i>
              </div>

              <div class="burger" v-if="isMobile" @click="isOpen = !isOpen">
                <i class="fas fa-bars" v-if="!isOpen"></i>
                <i class="fas fa-times" v-if="isOpen"></i>
              </div>
            </div>

           <div class="actions" v-if="!isMobile">
               <div class="search" @click="$emit('openSearchBar')">
                   <i class="fas fa-search"></i>
                   <span>Search</span>
               </div>
               <div class="auth" @click="$router.push({ name: 'Login'})">
                   <span>Login/Register</span>
               </div>
               <div class="act">
                   <i class="fas fa-user"></i>
                   <i class="fas fa-heart"></i>
               </div>
           </div>



        <!-- Mobile Menu -->
        <div :class="['burger-menu', { active: isOpen }]" v-if="isMobile">
          <ul class="mobile-menu">
            <li class="item " v-for="item in menuArray" :key="item.text" >
              <a :href="item.link" @click="foo(ind)">{{ item.text }}</a>
            </li>
          </ul>

          <div class="block">
            <div class="search-block">
              <i class="fas fa-search"></i>
              <input type="text" placeholder="search...">
            </div>

            <div class="box">
              <i class="fas fa-user"></i>
              <i class="fas fa-heart"></i>
            </div>

          </div>
        </div>

        </nav>
    </div>
  </header>
</template>


<script>
export default {
  data() {
    return {
      alTop: 0,
      isMobile: false,
      isOpen: false,
      logoImage: require('../assets/images/logos/logo.png'),  
      menuArray: [
        {
          text: 'Home/me',
          link: '/'
        },
        {
          text: 'About/me',
          link: '/blog'
        },
        {
          text: 'Contact',
          link: '/contact'
        },                
      ]
    }
  },
  methods: {
    foo(a){
      if(a = 0){
        this.router.push({name: 'Home'})
      }else if(a = 1){
        this.router.push({name: 'Blog'})
      }else{
        this.router.push({name: 'Contact'})
      }
    },
  
    checkScreenWidth(){
      const winWidth = window.innerWidth

      if(winWidth < 970){
        this.isMobile = true
        return
      }
      this.isMobile = false
      this.isOpen = false
    }
  },
  mounted() {
    this.checkScreenWidth()
    window.addEventListener("resize", this.checkScreenWidth)
  }
}
</script>


<style lang="scss">
 @import '../assets/styles/layout_styles/Navbar.scss'
</style>