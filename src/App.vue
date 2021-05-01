<template>
  <div id="app">
    <NavBar></NavBar>
    <IngresoDatos></IngresoDatos>
    
    
  </div>
</template>

<script>
import IngresoDatos from "./components/IngresoDatos.vue";
import NavBar from "./components/Navbar.vue";
export default {
  name: "App",
  components: {
    IngresoDatos,
    NavBar,
  },
};
</script>

<style>
#appa {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
