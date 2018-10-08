<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <Home />
  </div>
</template>

<script>
import Home from './pages/index.vue'

export default {
  name: 'app',
  components: {
    Home
  }
}
</script>
<style src="@/assets/css/app.css"></style>

