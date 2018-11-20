<template>
  <div id="app">
    <Page />
  </div>
</template>

<script>
import Page from './components/AdminListPage.vue'
// import Page from './components/UserListPage.vue'

export default {
  name: 'app',
  components: {
    Page
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
