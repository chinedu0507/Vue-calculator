<template>
  <div id="app">
    <!-- <Practice msg="Yap"></Practice> -->
    <!-- <Users></Users> -->
    <Calculator></Calculator>
  </div>
</template>

<script>
// import Practice from './components/Practice'
// import Users from './components/Users'
import Calculator from './components/Calculator'

export default {
  name: 'App',
  components: {
    // Practice,
    // Users
    Calculator
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
