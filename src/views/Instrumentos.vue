<template>
    <div style="margin-top:40px" >
        <div v-for="instrumento in instrumentosData" :key="instrumento.id" >
        <v-row class="tarjetas" >
            <instrumento-item :instrumentoParam="instrumento" ></instrumento-item>
            </v-row>
        </div>
    </div>
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
            instrumentosData: []
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
        }
    }
};
</script>
<style scoped>
.tarjetas {
    justify-content: center;
    
    padding-left:20%;
    padding-right:20%;
    padding-bottom: 1%;
    margin:0 auto;

}
</style>