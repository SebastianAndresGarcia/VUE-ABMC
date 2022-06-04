<!--https://vuetifyjs.com/en/components/text-fields/#custom-validation-->
<template>
    <v-card>
        <v-row justify="center">
            <v-col cols="12" sm="10" md="8" lg="6">
                <v-card ref="form">
                    <form @submit.prevent="updateinstru">
                        <v-card-text>
                            <v-text-field id="instrumento" v-model="insencontrado.instrumento" label="instrumento"
                                placeholder="instrumento" required>
                            </v-text-field>
                            <v-text-field id="marca" v-model="insencontrado.marca" label="marca" placeholder="marca"
                                required></v-text-field>
                            <v-text-field id="modelo" v-model="insencontrado.modelo" label="modelo" placeholder="modelo"
                                required></v-text-field>
                            <v-text-field id="imagen" v-model="insencontrado.imagen" label="imagen" placeholder="imagen"
                                required></v-text-field>
                            <v-text-field id="precio" v-model="insencontrado.precio" label="precio" required
                                placeholder="precio"></v-text-field>
                            <v-text-field id="costoEnvio" v-model="insencontrado.costoEnvio" label="costoEnvio" required
                                placeholder="costoEnvio"></v-text-field>
                            <v-text-field id="cantidadVendida" v-model="insencontrado.cantidadVendida"
                                label="cantidadVendida" required placeholder="cantidadVendida"></v-text-field>
                            <v-text-field id="descripcion" v-model="insencontrado.descripcion" required
                                placeholder="descripcion"></v-text-field>
                        </v-card-text>
                        <v-divider class="mt-12"></v-divider>
                        <v-card-actions>
                            <v-btn text :href="'../GrillaInstrumentos'">
                                Cancel
                            </v-btn>
                            <v-spacer></v-spacer>

                            <v-btn dark color="primary" type="submit">
                                Guardar
                            </v-btn>
                        </v-card-actions>
                    </form>
                </v-card>
            </v-col>
        </v-row>
    </v-card>
</template>
    
<script>
import router from '@/router';
export default {
    name: 'Formulario',
    components: {},
    mounted() {
        this.getInstrumentoXId()
    },
    updated() {

    },
    data() {
        return {
            insencontrado: {},

        }
    },

    methods: {
        async getInstrumentoXId() {
            const parametroId = this.$route.params.id
            //console.log("parametroid: " + parametroId)
            if (parametroId != 0) {
                const res = await fetch(
                    'http://localhost:3000/instrumentos/' + parametroId
                )
                const resJson = await res.json()
                console.log("resJson ", resJson)
                this.insencontrado = {
                    id: resJson[0].id,
                    instrumento: resJson[0].instrumento,
                    marca: resJson[0].marca,
                    modelo: resJson[0].modelo,
                    imagen: resJson[0].imagen,
                    precio: resJson[0].precio,
                    costoEnvio: resJson[0].costoEnvio,
                    cantidadVendida: resJson[0].cantidadVendida,
                    descripcion: resJson[0].descripcion
                }
            } else {
                this.insencontrado = {
                    id: 0,
                    instrumento: "",
                    marca: "",
                    modelo: "",
                    imagen: "",
                    precio: "",
                    costoEnvio: "",
                    cantidadVendida: "",
                    descripcion: ""
                }
            }
            console.log("this.encontrado en get ", this.insencontrado)
        },

        async updateinstru() {
            const parametroId = this.$route.params.id
            console.log("parametroid dentro de guardar" + parametroId)
            console.log("objeto dentro de guardar" + this.insencontrado)
            // console.log("objeto dentro de guardar" + insencontrado)
            let urlServer = 'http://localhost:3000/crearInstrumento/';
            let method = 'POST';
            if (parametroId != 0) {
                urlServer = 'http://localhost:3000/actualizarInstrumento/' + parametroId;
                method = 'PUT';
            }

            await fetch(urlServer, {
                "method": method,
                "body": JSON.stringify(this.insencontrado),
                "headers": {
                    "Content-type": 'application/json'
                },
                mode: 'cors'
            });
            router.push('/GrillaInstrumentos')
        },
    },
}

</script>
<style>
.row {
    justify-content: center;
    padding-top: 2%;
    padding-bottom: 2%;
    margin: 0 auto;
}
</style>