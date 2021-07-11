<template>
  <div id="app">
    <app-search></app-search>
    <app-footer></app-footer>
  </div>
</template>

<script>
import Search from './components/Search.vue'
import Footer from './components/Footer.vue'

import './assets/scss/main.scss'

export default {
  name: 'App',
  components: {
    'app-search': Search,
    'app-footer': Footer
  }
}
</script>
