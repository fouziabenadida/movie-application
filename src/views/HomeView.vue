<template>
 <PopularMovie/>
</template>

<script lang="ts">
  import Vue from 'vue'
  import PopularMovie from '../components/PopularMovie.vue'


  export default Vue.extend({
    name: 'HomeView',

    components: {
  PopularMovie
    },
  })
</script>
