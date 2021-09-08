<template>
    <div class="container">
        <div class="row">
            <div :class="{ 'col-md-8': nuevoHeroe, 'col-md-12': !nuevoHeroe }">
                <div class="row">
                    <div class="col-md-12">
                        <h1>Tour de héroes</h1>
                        <Buscador @buscar="buscarHeroePorPoderes"></Buscador>
                    </div>
                    <div class="col-md-12">
                        <button class="btn btn-primary float-right" @click="nuevoHeroe = !nuevoHeroe">Agregar héroe</button>  
                    </div>
                    <div class="col-md-12">
                        <div class="row">
                                <Heroe v-for="(heroe, indice) in heroesFiltrados" 
                                    :indice="indice" 
                                    :nombre="heroe.nombre" 
                                    :url_foto="heroe.url_foto" 
                                    :key="heroe.id"
                                    @eliminarHeroe="eliminarHeroe">
                                </Heroe>
                        </div>
                    </div>
                </div>
            </div>
            <div class="col-md-4" v-if="nuevoHeroe">
                <h1>Nuevo héroe</h1>
                <form @submit.prevent="agregarHeroe">
                    <div class="form-group">
                        <label for="">Id</label>
                        <input type="text" class="form-control" v-model="heroe.id">
                    </div>
                    <div class="form-group">
                        <label for="">Nombre</label>
                        <input type="text" class="form-control" v-model="heroe.nombre">
                    </div>
                    <div class="form-group">
                        <label for="">Poderes</label>
                        <input type="text" class="form-control" v-model="heroe.poderes">
                    </div>
                    <div class="form-group">
                        <label for="">URL_foto</label>
                        <input type="url" class="form-control" v-model="heroe.url_foto">
                    </div>
                    <button class="btn btn-primary" type="submit">Agregar</button>
                </form>
            </div>
        </div>
    </div>
</template>
<script>
import Buscador from './Buscador.vue'
import Heroe from './Heroe.vue'
export default {
    components: { Buscador, Heroe },
    data () {
        return {
            heroe: {
                id: '',
                nombre: '',
                poderes: '',
                url_foto: ''
            },
            heroes: [],
            busqueda: '',
            nuevoHeroe: false
        }
    },
    methods: {
        buscarHeroePorPoderes (valor) {
            this.busqueda = valor
        },
        agregarHeroe () {
            if (!this.heroe.id || !this.heroe.nombre || !this.heroe.poderes || !this.heroe.url_foto ) {
                return alert("Todos los campos son obligatorios")
            }

            let idHeroeDuplicado = this.heroes.find(heroe => heroe.id == this.heroe.id)

            if (idHeroeDuplicado) {
                return alert("El Id ya está tomado")
            }

            this.heroes.push({
                id: this.heroe.id,
                nombre: this.heroe.nombre,
                poderes: this.heroe.poderes,
                url_foto: this.heroe.url_foto,
            }) 

            this.heroe = {
                id: '',
                nombre: '',
                poderes: '',
                url_foto: ''
            }
        },
        eliminarHeroe (indice) {
            this.heroes.splice(indice, 1)
        }
    },
    computed: {
        heroesFiltrados () {
            if (this.busqueda) {
                return this.heroes.filter(heroe => {
                    return heroe.poderes.includes(this.busqueda)
                })
            } else {
                return this.heroes
            }
        }
    }
}
</script>