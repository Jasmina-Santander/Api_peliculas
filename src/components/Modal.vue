<template>

<!-- Modal ver descripción  -->
<div v-for="(item, id) in dataprops" :key="id">
  <div v-if="item.id ===idprops" class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header" >
          <h5 class="modal-title" id="exampleModalLabel"> {{item.title}} </h5>
          <button type="button" class="close" data-dismiss="modal" aria-label="Close">
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div class="modal-body">
        <p> {{item.overview}} </p>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" data-dismiss="modal">Cerrar</button>
          <button type="button" class="btn btn-primary">Guardar</button>
        </div>
      </div>
    </div>
  </div>
</div>
</template>

<script>
export default{
  name:'Modal',
  props:{
    dataprops:{
      type:Array,
      required:true
    },
    idprops:{
      type:Number,
      required:true
    },
  },
  mounted (){console.log(this.dataprops)}
}

</script>