<template>
    <div class="form-inline">
        <div class="form-group mb-2 mr-2">
            <label for="inputPassword2" class="sr-only">BUSCAR POR PODER</label>
            <input type="text" class="form-control" v-model="valor_buscado" 
                @keyup.enter="buscar"
                id="inputPassword2" placeholder="BUSCAR POR PODER">
        </div>
        <button type="submit" @click="buscar" class="btn btn-primary mb-2">Buscar</button>
    </div>
</template>
<script>
export default {
    data () {
        return {
            valor_buscado: ''
        }
    },
    methods: {
        buscar () {
            this.$emit('buscar', this.valor_buscado)
        }
    }
}
</script>