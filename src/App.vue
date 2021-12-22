<template>
  <v-app>
    <appbar-inicio/>
    <v-main>
      <router-view/>
    </v-main>
    <footer-inicio></footer-inicio>
  </v-app>
</template>

<script>
import Appbar from '../src/components/Appbar.vue';
import Footer from '../src/components/Footer.vue'
export default {
  name: 'App',
  components:{
    'appbar-inicio':Appbar,
    'footer-inicio':Footer
  },
  data: () => ({
    //
  }),
};
</script>
