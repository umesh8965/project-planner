<template>
  <NavBar></NavBar>
  <router-view/>
</template>

<script>
import NavBar from "./components/NavBar"
export default {
  components:{
    NavBar
  }
}
</script>
<style>
body{
    background-color: #f3f3f3;
    font-size: 12px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin: 0 auto;
  max-width: 600px;
  color: #555;
}

</style>
