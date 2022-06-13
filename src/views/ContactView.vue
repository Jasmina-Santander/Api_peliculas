<template>
<Nav />
<router-view/>
<Contacto />
<Footer />
</template>

<script>
import Nav from '@/components/Nav.vue'
import Contacto from "../components/Contacto.vue"
import Footer from "../components/Footer.vue"

export default {
  name: 'ContactView',
  components:{
    Nav,
    Contacto,
    Footer,
  }
}
</script>
