<template>
  <!-- Formulario Login-->
  <section class="color">
    <div class="container">
      <form>
        <div class="form-group">
          <label for="exampleInputEmail1">Email address</label>
          <input v-model="email" type="email" class="form-control" autocomplete="current-email" id="current-email" aria-describedby="emailHelp"/>
        </div>
        <div class="form-group">
          <label for="exampleInputPassword1">Password</label>
          <input v-model="passwordinput" type="password" autocomplete="current-password" class="form-control" id="current-password"/>
        </div>
        <div class="form-group form-check">
          <input type="checkbox" class="form-check-input" id="exampleCheck1" />
          <label class="form-check-label" for="exampleCheck1">Check me out</label>
        </div>
        <button @click.prevent="validar()" type="submit" class="btn btn-primary">
          Ingresar
        </button>
      </form>
    </div>
  </section>
</template>

<script>
export default {
  name: "InicioLogin",

  data() {
    return {
      result2: [],
      email: "",
      passwordinput: "",
    };
  },
  //Validacion de Usuario
  methods: {
    validar() {
      console.log(this.passwordinput);
      console.log(this.email);
      if (
        this.result2[0].password === this.passwordinput &&
        this.result2[0].email === this.email
      ) {
        console.log("Login");
        this.$router.push("/home");
      } else {
        console.log("Datos incorrectos");
      }
    },
  },
  //Funcion asincrona
  async created() {
    try {
      const res = await fetch("servicios/auth.json");
      const data = await res.json();
      this.result2 = data.resultado;
    } catch (error) {
      console.log(error.message);
    }
  },
};
</script>

<style scoped>
.color {
  height: 100vh;
  background: #fc466b; /* fallback for old browsers */
  background: -webkit-linear-gradient(
    to right,
    #3f5efb,
    #fc466b
  ); /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(
    to right,
    #3f5efb,
    #fc466b
  ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */

  padding-top: 12%;
}
.container {
  width: 30%;
}
</style>
