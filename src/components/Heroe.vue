<template>
    <div class="col-md-4">
        
            <h2>{{ nombre }}</h2>
            <img class="img-fluid" :src="url_foto" alt="">

            <button class="btn btn-danger" @click="eliminarHeroe">Eliminar</button>
    </div>
</template>
<script>
export default {
    props: [ 'indice', 'nombre', 'url_foto'],
    methods: {
        eliminarHeroe () {
            this.$emit('eliminarHeroe', this.indice)
        }
    }
}
</script>