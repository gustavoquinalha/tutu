<template>
<div id="app">
  <transition name="fade">
    <router-view></router-view>
  </transition>

  <rodape></rodape>
</div>
</template>

<script>
import rodape from './components/rodape'

export default {
  name: 'app',
  components: {
    rodape
  }
}
</script>

<style>
  @import 'assets/css/main.scss';
  @import '../node_modules/the-grid-flexbox/css/the-grid.min.css';
</style>
