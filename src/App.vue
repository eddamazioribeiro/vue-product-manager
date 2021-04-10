<template>
  <div id="app">
    <AppHeader />
    <h1>Welcome to Vue.js App</h1>
  </div>
</template>

<script>
import AppHeader from './components/AppHeader.vue'
export default {
  name: 'App',
  components: {
    AppHeader: AppHeader
  }
}
</script>

<style>
</style>
