<template>
<Nav />
<Carrusel />
<router-view/>

<Card />
<Footer />


</template>

<script>
import Nav from '../components/Nav.vue'
import Carrusel from "../components/Carrusel.vue";
import Card from "../components/Card.vue";
import Footer from "../components/Footer.vue"

// @ is an alias to /src


export default {
  name: 'HomeView',
  components: {
    Nav,
    Carrusel,
    Card,
    Footer,

}
}
</script>


<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
}

nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>

