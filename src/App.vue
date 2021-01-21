<template>
  <Main />
</template>

<script>
import Main from './components/Main.vue'

export default {
  name: 'App',
  components: {
    Main
  }
}
</script>

<style>
  body{
    background: #12c2e9;  
    background: -webkit-linear-gradient(to right, #f64f59, #c471ed, #12c2e9);
    background: linear-gradient(to right, #f64f59, #c471ed, #12c2e9);
  }

  #app {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 97vh;
  }
</style>
