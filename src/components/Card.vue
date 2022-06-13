<template>
  <!-- Botón del modal de carrito-->

  <button type="button" class="btn btn-primary botonCarrito" data-toggle="modal" data-target="#exampleModal2">
    Carrito {{ contadorCarrito }}
  </button>

  <!-- Modal de carrito  -->
  <div class="modal fade" id="exampleModal2" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">Carrito de compra</h5>
          <button type="button" class="close" data-dismiss="modal" aria-label="Close">
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div class="modal-body">
          <table class="table">
            <thead>
              <tr>
                <th>Pélicula</th>
                <th>Cantidad</th>
                <th></th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(item, id) in carrito" :key="id">
                <td>{{ item.title }}</td>
                <td>{{ item.cantidad }}</td>
                <td>
                  <button type="button" class="btn btn-danger" v-on:click="eliminar(item.id)">
                    <img src="img/delete.svg" />
                  </button>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" data-dismiss="modal" v-on:click="vaciar()">
            Vaciar Carrito
          </button>
        </div>
      </div>
    </div>
  </div>

  <!-- Pasando props al componente Modal -->
  <Modal :dataprops="result" :idprops="id" />

  <!-- Cards  -->
  <div class="container mb-5">
    <h1 class="text-center mt-5 mb-5">Películas en cartelera</h1>
    <div class="row justify-content-center">
      <!-- Buscador -->
      <input type="text" v-model.trim="search" placeholder="Ingresa una película" @keyup="searchData()"/>
      <button class="btn btn-danger">Buscar</button>
    </div>

    <div class="row justify-content-center">
      <div
        class="card text-white bg-light col-12 col-sm-3 m-4 shadow-lg p-3 mb-5 rounded"
        v-for="(item, index) in resultFiltro" :key="index">
        <img class="card-img-top" :src="imagen + item.poster_path" :alt="item.title"/>

        <div class="card-body">
          <h5 class="card-title text-dark">{{ item.title }}</h5>
          <p class="card-text text-dark">Ranking: {{ item.vote_average }}</p>
          <!--Boton ver descripcion  -->
          <button v-on:click="capturarId(item.id)" type="button" class="btn btn-primary" data-toggle="modal" data-target="#exampleModal">
            Ver descripción
          </button>
          <!-- Boton agregar al carrito  -->
          <button v-on:click="addCarrito(item.id)" type="button" class="btn btn-warning mt-4">
            Agregar <img src="img/corazon.svg" />
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Modal from "./Modal";
export default {
  name: "Card",
  components: {
    Modal,
  },

  data() {
    return {
      imagen: "https://image.tmdb.org/t/p/w500",
      result: [],
      id: 0,
      search: "",
      carrito: [],
      producto: [],
      verificador: false,
    };
  },

  methods: {
    capturarId(idc) {
      this.id = idc;
      console.log(this.id);
    },
    searchData() {
      console.log(this.search);
    },
    // Funcion de agregar al carrito, eliminar y vaciar carrito por Id
    addCarrito(idAdd) {
      this.producto = this.result.find((item) => item.id === idAdd);
      //verificar si la película está en array de carrito, sí esta te devuelve true, sino false
      this.verificador = this.carrito.some((item) => item.id === idAdd);
      if (!this.verificador) {
        this.producto.cantidad = 1;
        this.carrito.push(this.producto);
      } else {
        this.producto.cantidad = this.producto.cantidad + 1;
        console.log("el producto ya esta");
      }
      //console.log(this.producto)
      //console.log(this.producto[0])
      console.log(this.carrito);
    },
    eliminar(idEliminar) {
      this.carrito = this.carrito.filter((item) => item.id !== idEliminar);
    },
    vaciar() {
      this.carrito = [];
    },
  },

  //fetch("https://api.themoviedb.org/3/movie/popular?api_key=192e0b9821564f26f52949758ea3c473&language=es-MX&pag")
  //https://api.themoviedb.org/3/search/movie?api_key=192e0b9821564f26f52949758ea3c473&query=Batman
  //Funcion asincrona
  async created() {
    try {
      const res = await fetch("servicios/api.json");
      const data = await res.json();
      this.result = data.results;
    } catch (error) {
      console.log(error.message);
    }
  },
  //Filtro de busqueda
  computed: {
    resultFiltro() {
      return this.result.filter((item) => {
        return item.title.toLowerCase().includes(this.search.toLowerCase());
      });
    },
    //Contador Carrito
    contadorCarrito() {
      let contador = 0;
      this.carrito.forEach((element) => {
        contador += element.cantidad;
      });
      return contador;
    },
  },
};
</script>

<style>
.botonCarrito {
  position: absolute;
  top: 0;
  right: 78px;
  margin-top: 10px;
}
</style>
