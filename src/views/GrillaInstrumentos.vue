<template>
    <v-card>
        <v-card-title>
            Instrumentos
            <v-spacer></v-spacer>
            <!--  <v-text-field type="number" id="preciomin" v-model="preciomin" placeholder="preciomin">
            </v-text-field>
            <v-text-field type="number" id="preciomax" v-model="preciomax" placeholder="preciomax"></v-text-field>
-->
            <v-row justify="center">
                <form>
                    <v-row>
                        <v-col cols="12" sm="6" md="4">
                            <v-text-field type="number" placeholder="ingresevalor" label="preciomin" v-model="preciomin"
                                required></v-text-field>
                        </v-col>
                        <v-col cols="12" sm="6" md="4">
                            <v-text-field type="number" placeholder="ingresevalor" label="preciomax" v-model="preciomax"
                                required></v-text-field>
                        </v-col>
                        <v-col cols="6" sm="3" md="2">
                            <v-btn dark small @click="filtrarporprecio(preciomin, preciomax)">
                                Filtrar
                            </v-btn>
                            <v-btn dark small :href="'./GrillaInstrumentos'">
                                Limpiar
                            </v-btn>
                        </v-col>
                    </v-row>
                </form>
            </v-row>

            <v-spacer></v-spacer>
            <v-btn color="primary" dark class="mb-2" :href="'/Formulario/0'">
                Cargar Nuevo
            </v-btn>
        </v-card-title>
        <v-simple-table class="tabla">
            <template v-slot:default>
                <thead>
                    <tr>
                        <th class="text-left">
                            <b>ID</b>
                        </th>
                        <th class="text-left">
                            <b>Nombre</b>
                        </th>
                        <th class="text-left">
                            <b>Marca</b>
                        </th>
                        <th class="text-left">
                            <b>Modelo</b>
                        </th>
                        <th class="text-left">
                            <b>Imagen</b>
                        </th>
                        <th class="text-left">
                            <b>Precio</b>
                        </th>
                        <th class="text-left">
                            <b>Costo de Envío</b>
                        </th>
                        <th class="text-left">
                            <b>Vendidos</b>
                        </th>

                        <th class="text-left">

                        </th>
                        <th class="text-left">

                        </th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="instrumento in instrumentosData" :key="instrumento.id" style="padding-top: 5px;">

                        <td>
                            {{ instrumento.id }}
                        </td>
                        <td>
                            {{ instrumento.instrumento }}
                        </td>
                        <td>
                            {{ instrumento.marca }}
                        </td>
                        <td>
                            {{ instrumento.modelo }}
                        </td>
                        <td>
                            <span v-if="instrumento.imagen.indexOf('http') >= 0">
                                <img :src="instrumento.imagen" style="max-width: 60px;" :alt="instrumento.imagen" />
                            </span>
                            <span v-else>
                                <img :src="'/images/' + instrumento.imagen" style="max-width: 60px;"
                                    :alt="instrumento.imagen" />
                            </span>

                        </td>
                        <td>
                            {{ instrumento.precio }}
                        </td>
                        <td>
                            {{ instrumento.costoEnvio }}
                        </td>
                        <td>
                            {{ instrumento.cantidadVendida }}
                        </td>

                        <td>
                            <a :href="'/Formulario/' + instrumento.id">
                                <v-icon small class="mr-2">
                                    mdi-pencil
                                </v-icon>
                            </a>
                        </td>
                        <td>
                            <v-icon small @click="deleteinstrumento(instrumento.id)">
                                mdi-delete
                            </v-icon>
                        </td>

                    </tr>
                </tbody>
            </template>
        </v-simple-table>
    </v-card>
</template>
<script >
import tarjetainstrumento from "@/components/tarjetainstrumento.vue";
export default {
    name: "instrumentos",
    components: {
        "instrumento-item": tarjetainstrumento
    },
    mounted() {
        this.getInstrumentos()
    },
    data() {
        return {
            instrumentosData: [],
            preciomax: undefined,
            preciomin: undefined
        };
    },
    methods: {
        async getInstrumentos() {
            const res = await fetch(
                "http://localhost:3000/instrumentos"
            );
            const resJson = await res.json();
            console.log(resJson);
            this.instrumentosData = resJson;
        },

        async filtrarporprecio(preciomin, preciomax) {

            const res = await fetch(
                "http://localhost:3000/instrumentos"
            );
            console.log("preciomin" + preciomin)
            console.log("preciomax" + Number(preciomax))
            //this.instrumentosData = resJson;
            //if (Number(preciomax) != null && Number(preciomax) != NaN && Number(preciomax) != 0) {
            //this.instrumentosData = resJson;
            if (Number(preciomax) > 0&&Number(preciomin)>0) {
                const resJson = await res.json();
                console.log("funcion filtrar ", resJson);
                this.instrumentosData.splice(0, this.instrumentosData.length);
                for (let i of resJson) {
                    if (Number(preciomin) <= Number(i.precio) && Number(preciomax) >= Number(i.precio)) {
                        this.instrumentosData.push(i)
                    }
                }
            } else //if (Number(preciomax) == undefined || Number(preciomax) == 0 || Number(preciomax) == null || this.instrumentosData.length == 0) {
                window.location.reload();
            

        },

        async deleteinstrumento(idinstrumento) {

            let urlServer = `http://localhost:3000/eliminarInstrumento/${idinstrumento}/`;


            await fetch(urlServer, {
                "method": 'DELETE',

                "headers": {
                    "Content-type": 'application/json',
                    'Access-Control-Allow-Origin': '*'
                },
                mode: 'cors'

            });
            window.location.reload();
        },
        /* async editarinstrumento(idinstrumento){
            href('/Formulario/' + instrumento.id),
         */
    }
};
</script>
<style scoped>
.tabla {
    padding: 5%;
}

a {
    text-decoration: none;
}

.form-inline {
    display: flex;
    flex-flow: row wrap;
    align-items: center;
}

.form-inline label {
    margin: 5px 10px 5px 0;
}

/* Style the input fields */
.form-inline input {
    vertical-align: middle;
    margin: 5px 10px 5px 0;
    padding: 10px;
    background-color: #fff;
    border: 1px solid #ddd;
}

/* Style the submit button */
.form-inline button {
    padding: 10px 20px;
    background-color: dodgerblue;
    border: 1px solid #ddd;
    color: white;
}

.form-inline button:hover {
    background-color: royalblue;
}

/* Add responsiveness - display the form controls vertically instead of horizontally on screens that are less than 800px wide */
@media (max-width: 800px) {
    .form-inline input {
        margin: 10px 0;
    }

    .form-inline {
        flex-direction: column;
        align-items: stretch;
    }
}
</style>