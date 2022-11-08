<template>
  <v-app>
  <NavBar/>
    <v-main>
      <router-view/>
    </v-main>
  <Footer/>
  </v-app>
</template>

<script lang="ts">
import Vue from 'vue';
import NavBar from './components/NavBar.vue'
import Footer from './components/Footer.vue'

export default Vue.extend({
  name: 'App',

  data: () => ({
    //
  }),
  components: {
    NavBar,
    Footer
  }
});
</script>
