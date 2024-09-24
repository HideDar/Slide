<template>
  <div id="app">
    <SlideShow />
  </div>
</template>

<script>
import SlideShow from './components/SlideShow.vue'

export default {
  name: 'App',
  components: {
    SlideShow
  }
}
</script>

<style>
@import 'bootstrap/dist/css/bootstrap.min.css';

body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 20px;
  background-color: #f0f0f0;
}

#app {
  max-width: 800px;
  margin: 0 auto;
  background-color: white;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  padding: 20px;
}
</style>