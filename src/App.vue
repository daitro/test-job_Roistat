<template>
  <div id="app">
    <main class="container">
      <MainPage/>
    </main>
  </div>
</template>

<script>
import MainPage from './pages/MainPage.vue'

export default {
  name: 'App',
  components: {
    MainPage
  }
}
</script>

<style scoped>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  color: #1b242d;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 24px;
}
</style>
