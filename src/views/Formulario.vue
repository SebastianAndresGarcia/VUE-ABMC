<!--https://vuetifyjs.com/en/components/text-fields/#custom-validation-->
<template>
    <v-card>
        <v-row justify="center">
            <v-col cols="12" sm="10" md="8" lg="6">
                <v-card ref="form">
                    <form @submit.prevent="submit">
                        <v-card-text>
                            <v-text-field ref="instrumento" v-model="insencontrado.instrumento"
                                :rules="[() => !!instrumento || 'This field is required']"
                                :error-messages="errorMessages" label="instrumento" placeholder="instrumento" required>
                            </v-text-field>
                            <v-text-field ref="marca" id="marca" v-model="insencontrado.marca" :rules="[
                                () => !!marca || 'This field is required',
                                addressCheck
                            ]" label="marca" placeholder="marca" required></v-text-field>
                            <v-text-field ref="modelo" v-model="insencontrado.modelo"
                                :rules="[() => !!modelo || 'This field is required', addressCheck]" label="modelo"
                                placeholder="modelo" required></v-text-field>
                            <v-text-field ref="imagen" v-model="insencontrado.imagen"
                                :rules="[() => !!imagen || 'This field is required', addressCheck]" label="imagen"
                                placeholder="imagen" required></v-text-field>
                            <v-text-field ref="precio" v-model="insencontrado.precio"
                                :rules="[() => !!precio || 'This field is required']" label="precio" required
                                placeholder="precio"></v-text-field>
                            <v-text-field ref="costoEnvio" v-model="insencontrado.costoEnvio"
                                :rules="[() => !!costoEnvio || 'This field is required']" label="costoEnvio" required
                                placeholder="costoEnvio"></v-text-field>
                            <v-text-field ref="cantidadVendida" v-model="insencontrado.cantidadVendida"
                                :rules="[() => !!cantidadVendida || 'This field is required']" label="cantidadVendida"
                                required placeholder="cantidadVendida"></v-text-field>
                            <v-text-field ref="descripcion" v-model="insencontrado.descripcion"
                                :rules="[() => !!descripcion || 'This field is required']" label="descripcion" required
                                placeholder="descripcion"></v-text-field>
                        </v-card-text>
                        <v-divider class="mt-12"></v-divider>
                        <v-card-actions>
                            <v-btn text>
                                Cancel
                            </v-btn>
                            <v-spacer></v-spacer>
                            <v-slide-x-reverse-transition>
                                <v-tooltip v-if="formHasErrors" left>
                                    <template v-slot:activator="{ on, attrs }">
                                        <v-btn icon class="my-0" v-bind="attrs" @click="submit" v-on="on">
                                            <v-icon>mdi-refresh</v-icon>
                                        </v-btn>
                                    </template>
                                    <span>Refresh form</span>
                                </v-tooltip>
                            </v-slide-x-reverse-transition>
                            <v-btn color="primary" type="submit">
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
            insencontrado:
                {
                    "instrumento": "",
                    "marca": "",
                    "modelo": "",
                    "imagen": "",
                    "precio": "",
                    "costoEnvio": "",
                    "cantidadVendida": "",
                    "descripcion": "",
                },
            errorMessages: '',
            formHasErrors: false,
        }
    },
    watch: {
        name() {
            this.errorMessages = ''
        },
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
                console.log(resJson)
                this.insencontrado = resJson
            }

            console.log(this.insencontrado)

        },
        addressCheck() {
            this.errorMessages = this.address && !this.name
                ? `Hey! I'm required`
                : ''

            return true
        },
        resetForm() {
            this.errorMessages = []
            this.formHasErrors = false

            Object.keys(this.form).forEach(f => {
                this.$refs[f].reset()
            })
        },
        async submit() {
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