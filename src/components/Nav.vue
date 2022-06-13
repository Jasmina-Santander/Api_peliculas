<template>
  <!--Menu-->
  <nav class="navbar navbar-expand-md navbar-light bg-light">
    <div class="container-fluid">
      <a class="navbar-brand" href="#">NEXTFLI</a>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav ms-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <a class="nav-link" href=""><router-link to="/home">Home</router-link></a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href=""><router-link to="/contact">Contacto</router-link></a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href=""><router-link to="/">Cerrar Sesión</router-link></a>
          </li>
          <li class="nav-item">
            <a class="nav-link" v-for="(item, id) in result3" :key="id">
              {{ item.name }}
            </a>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: "Nav",

  data() {
    return {
      result3: [],
    };
  },
//Funcion asincrona 
  async created() {
    try {
      const res = await fetch("servicios/auth.json");
      const data = await res.json();
      this.result3 = data.resultado;
    } catch (error) {
      console.log(error.message);
    }
  },
};
</script>

<style></style>
