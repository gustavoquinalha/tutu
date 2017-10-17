<template>
<div id="app">
  <!-- <headerMenu></headerMenu> -->
  <transition name="fade">
    <router-view></router-view>
  </transition>

  <rodape></rodape>
</div>
</template>

<script>
import headerMenu from './components/menu'
import rodape from './components/rodape'

export default {
  name: 'app',
  components: {
    headerMenu,
    rodape
  }
}
</script>

<style>
  @import 'assets/css/main.scss';
  @import '../node_modules/the-grid-flexbox/css/the-grid.min.css';
</style>
