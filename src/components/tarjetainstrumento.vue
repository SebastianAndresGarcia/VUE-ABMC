<template>


    <v-row class="tarjetas">

        <v-col align="center" justify="center">
            <br>
            <h6>{{ instrumentoParam.cantidadVendida }} vendidos</h6>

            <a :href="'./DetalleInstrumento/' + instrumentoParam.id">
                <span v-if="instrumentoParam.imagen.indexOf('http') >= 0">
                    <img :src="this.instrumentoParam.imagen" style="max-width: 160px;" />

                </span>
                <span v-else>
                    <img :src="'/images/' + instrumentoParam.imagen" style="max-width: 160px;" alt="Image" />
                </span>
            </a>
            <br /><br />
        </v-col >
        <v-col cols="6">
            <br />
            <h5>{{ instrumentoParam.instrumento }}</h5>
            <h4>$ {{ instrumentoParam.precio }}</h4>
            <span v-if="instrumentoParam.costoEnvio === 'G'">
                <h6> <img src='/images/camion.png' alt='camion' />Envío gratis a todo el país</h6>
            </span>
            <span v-else>
                <p><img src='/images/camion.png' alt='camion' />Costo de envío: ${{ instrumentoParam.costoEnvio }}</p>
            </span>


        </v-col>

    </v-row>

</template>
<script>

export default {

    data() {
        return {
            urlImage: String
        };
    },
    props: ["instrumentoParam"],
    mounted() {
        if (String(this.instrumentoParam.imagen).indexOf("http") >= 0) {
            this.urlImage = this.instrumentoParam.imagen;
            console.log(this.urlImage)
        } else {
            this.urlImage = "../images/" + this.instrumentoParam.imagen;
            console.log(this.urlImage)
        }
    }
};
</script>
<style scoped>
.tarjetas {
    text-align: justify;
    align-items: center;    /**verticalmente */
    
    margin-left: 0 auto;
    align: center;
    justify: center;
    
    border: 1px solid rgb(82, 3, 3);
}

</style>