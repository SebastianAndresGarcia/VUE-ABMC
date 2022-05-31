<template>

    <!--   <v-row>
                <v-col class="col" cols="30%">
                    <img style="max-height:400px" :src="urlImage" />
                </v-col>
                <v-col class="col" cols="70%">
                   
                            <h1>{{ insencontrado[0].instrumento }}</h1>
                  <br>
                            <h2>$ {{ insencontrado[0].modelo }}</h2>
                   
                   <br>
                            <h2>{{ insencontrado[0].precio }}</h2>
                      
                </v-col>       
    </v-row>
    <v-row>
        
                        <h3 class="col"><b>Descripción:</b></h3>
                    
                    
                        <h2>{{ insencontrado[0].descripcion }}</h2>
                    
                
                <a href="/home" class="btn btn-success">VOLVER</a>
                
    </v-row>  -->

    <v-container >
        <v-row class="rowdetalle" align="center" justify="center">
            <v-col sm="12" md="8">

                <v-row class="rowinterno">
                    <v-col align="center">
                        <img style="height:100%" :src="urlImage" />
                    </v-col>
                    <v-col cols="4" sm="6">

                        <h2>{{ insencontrado[0].instrumento }}</h2>
                        <br>
                        <h4> {{ insencontrado[0].modelo }}</h4>
                        <br>
                        <h4>${{ insencontrado[0].precio }}</h4>

                    </v-col>
                </v-row>
                <hr><br>
                <h3><b>Descripción</b></h3><br>
                <p align="justify">{{ insencontrado[0].descripcion }}</p>
                <br><br><a href="/home" class="btn btn-success">VOLVER</a>
                <br>
            </v-col>

        </v-row>

    </v-container>
</template>

<script>
export default {
    name: 'DetalleInstrumento',
    components: {},
    mounted() {
        this.getInstrumentoXId()
    },
    updated() {
        if (String(this.insencontrado.imagenPath).indexOf('http') >= 0) {
            this.urlImage = this.insencontrado[0].imagen
        } else {
            this.urlImage = '/images/' + this.insencontrado[0].imagen
        }
    },
    data() {
        return {
            urlImage: String,
            insencontrado: []
        }
    },
    methods: {
        async getInstrumentoXId() {
            const parametroId = this.$route.params.id
            console.log("parametroid: " + parametroId)
            const res = await fetch(
                'http://localhost:3000/instrumentos/' + parametroId
            )
            const resJson = await res.json()
            console.log(resJson)
            this.insencontrado = resJson
            console.log(this.insencontrado)
        }
    }
}
</script>
<style>
.container {
    padding: 2%;
    margin-top: 5%;
    margin-left: 0 auto;
}

* {
    padding: 0;
    margin: 0 auto;
}

.rowdetalle {
    text-align: justify;
}
.rowinterno {
    text-align: justify;
    padding-bottom: 50px;
}
</style>