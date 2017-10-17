<template>
<div>

  <div class="relative-menu">
    <div class="menu-full">
      <div class="menu size margin container justify-content-between align-items-center">
        <router-link :to="{ name: 'Home' }">
          <div class="logo-menu container align-items-center">
            <img src="../assets/images/logo-01.svg" width="40" alt="">
          </div>
        </router-link>
        <div class="link-menu">
          <ul class="container">
            <li>
              <router-link :to="{ name: 'Home' }">Home</router-link>
            </li>
          </ul>
        </div>
        <div class="responsive-menu">
          <div class="svg" @click="toggleMenu">
            <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" viewBox="0 0 24 24" enable-background="new 0 0 24 24" width="30" height="30"><g><path d="M24,3c0-0.6-0.4-1-1-1H1C0.4,2,0,2.4,0,3v2c0,0.6,0.4,1,1,1h22c0.6,0,1-0.4,1-1V3z" fill="#2c3e50"/><path d="M24,11c0-0.6-0.4-1-1-1H1c-0.6,0-1,0.4-1,1v2c0,0.6,0.4,1,1,1h22c0.6,0,1-0.4,1-1V11z" fill="#2c3e50"/><path d="M24,19c0-0.6-0.4-1-1-1H1c-0.6,0-1,0.4-1,1v2c0,0.6,0.4,1,1,1h22c0.6,0,1-0.4,1-1V19z" fill="#2c3e50"/></g></svg>
          </div>
        </div>
      </div>
    </div>
    <transition name="slide-fade">
      <div class="responsive-menu-content" v-show="showMenu" v-cloak>
        <ul class="container column">
          <li>
            <router-link :to="{ name: 'Home' }">
              <span @click="showMenu = false">Home</span>
            </router-link>
          </li>
        </ul>
      </div>
    </transition>
  </div>



</div>
</template>

<style scoped>
.responsive-menu-content {
  width: 420px;
  max-width: 90%;
  left: 0px;
  height: calc(100vh - 60px);
  background: #fff;
  bottom: 0;
  border-right: 5px solid #4fc08d;
  box-shadow: 10px 0 30px 10px rgba(0, 0, 0, .2);
  overflow: hidden;
  position: fixed;
  z-index: 9
}

.responsive-menu-content ul {
  padding-top: 20px;
}

.responsive-menu-content ul li a {
  color: #4fc08d;
  font-size: 1rem;
  font-weight: 700;
  cursor: pointer;
  transition: .1s
}

.responsive-menu-content ul li a.router-link-exact-active.router-link-active {
  /*color: #2c3e50;*/
}

.responsive-menu-content ul li a:hover {
  color: #2c3e50;
}

.responsive-menu-content ul li {
  margin-top: 20px
}

.svg {
  cursor: pointer;
  height: 30px;
  width: 30px;
}

.svg svg {
  width: 15px
}

.logo-menu h1,
.logo-menu a {
  font-size: 20px;
  margin-left: 10px;
  font-weight: 500
}

.link-menu ul.container {
  list-style: none;
}

.link-menu ul.container a.router-link-exact-active.router-link-active {
  color: #4fc08d;
  font-weight: 700
}

.link-menu ul.container a {
  text-decoration: none;
  padding: 10px;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  font-size: 14px;
  font-weight: 500;
  transition: .1s
}

.link-menu ul.container a:hover {
  color: #4fc08d
}

.relative-menu {
  height: 60px;
  width: 100%;
  position: relative;
  margin-bottom: 20px
}

.menu-full {
  height: 60px;
  width: 100%;
  position: fixed;
  z-index: 99;
  background: #fff;
}

.menu {
  height: 60px;
}

.responsive-menu {
  display: none
}

@media screen and (max-width: 720px) {
  .logo-menu h1 {
    font-size: 16px!important;
  }
}

@media screen and (max-width: 480px) {
  .link-menu {
    display: none
  }
  .responsive-menu {
    display: block
  }
}

.slide-fade-enter-active {
  transition: all .1s cubic-bezier(.37, .61, .58, .86);
}

.slide-fade-leave-active {
  transition: all .1s cubic-bezier(.37, .61, .58, .86);
}

.slide-fade-enter,
.slide-fade-leave-to {
  transform: translateX(-400px);
}
</style>

<script>
export default {
  data () {
    return {
      showMenu: false
    }
  },
  methods: {
    toggleMenu: function () {
      this.showMenu = !this.showMenu
    }
  }
}
</script>
