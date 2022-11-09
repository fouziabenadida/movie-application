<template>
  <div>
 <PopularMovie/>
 <UpCommingMovie/>
</div>
</template>

<script lang="ts">
  import Vue from 'vue'
  import PopularMovie from '../components/PopularMovie.vue'
  import UpCommingMovie from '@/components/UpCommingMovie.vue';


  export default Vue.extend({
    name: 'HomeView',

    components: {
  PopularMovie,
  UpCommingMovie
    },
  })
</script>
