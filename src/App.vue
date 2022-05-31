<template>

  <div id="app">
    <div id="nav">
      <top-nav-bar></top-nav-bar>
    </div >
    <router-view />
    
  </div>

</template>



<script lang="ts">
import Vue from 'vue';
import NavBarTop from "@/components/NavBarTop.vue";
import DondeEstamos from "@/components/DondeEstamos.vue";
export default Vue.extend({
  name: 'App',

  data: () => ({
    //
  }),
  components: {
    "top-nav-bar": NavBarTop,
    "dondeestamos": DondeEstamos,
  }
});
</script>
