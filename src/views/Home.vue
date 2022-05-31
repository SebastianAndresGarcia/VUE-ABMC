<template>
  <!--      <div class="showcase">

            <img src='/images/nro1.jpg' alt="instrumentos" class="bg-image" />

            <h2 class='bg-img-title'> <b>Quienes Somos</b></h2>
            <div class="showcase-box">
                <p><b>Musical Hendrix es una tienda de instrumentos musicales con ya más de 15 años de experiencia.
                        Tenemos el
                        conocimiento y la capacidad como para informarte acerca de las mejores elecciones para tu compra
                        musical.</b>
                </p>
            </div>


            <button class='bg-img-verproductos'>
                <h3 style="text-align: center"><b><i><v-btn href='./Instrumentos'>Nuestros Productos</v-btn></i></b></h3>
            </button>
            <div id='ubicacion'> </div>
        </div>
-->
  <v-parallax class="imagen"  src="https://s03.s3c.es/imag/_v0/770x420/0/b/7/Instrumentos-musicales.jpg" alt="instrumentos">
    <v-row class="rowhome" align="center" justify="center">
      <v-col class="colhome" cols="12">
        <h1 class="h1home">
          <b> Musical Hendrix</b>
        </h1>
        <h2 class="h2home">
          Musical Hendrix es una tienda de instrumentos musicales con ya más de 15 años de experiencia.
          Tenemos el conocimiento y la capacidad como para informarte acerca de las mejores elecciones para tu compra
          musical.
        </h2>
        <h2 style="text-align: center" color="black">
          <v-btn rounded color="success" dark href='./Instrumentos'>
            Nuestros Productos
          </v-btn>
        </h2><br>
        <dondeestamos></dondeestamos>
        
      </v-col>

    </v-row>

  </v-parallax>

</template>

<script lang="ts">
import Vue from 'vue';
import DondeEstamos from "@/components/DondeEstamos.vue";
export default Vue.extend({
  name: 'Home',

  data() {
    return {
      loader: null,
    }
  },

  components: {

    "dondeestamos": DondeEstamos,
  }
})


</script>
<style>
.imagen{ 
    min-height: 100vh;
    max-width: 100%;
    background-color: papayawhip; 
    margin: 0 auto;
}
.rowhome {
  text-align: justify;
  align-items: center;
  /**verticalmente */
  display: flex;
  margin-left: 0 auto;
  padding-left: 25%;
  padding-right: 25%;
  /**para que achique el tamaño del contenido, agrega como un marco */
}

.colhome {
  justify-content: center;
  text-align: justify;
  margin-left: auto;
}

.h1home {
  text-align: center;
  color: rgb(143, 4, 4);
  padding-bottom: 20px;
}

.h2home {
  padding-bottom: 30px;
}
.h2{ 
  color:black;
}
</style>