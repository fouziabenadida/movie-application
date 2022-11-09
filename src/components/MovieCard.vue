<template>
  
</template>

<script>
export default {
props: {
    movie: {
        required: true
    },
    genres: {
        required: true,
    }
},
computed: {
    posterPath() {
        return "https://image.tmdb.org/t/p/w500/" + this.movie.poster_path
    }
},
methods: {
    genreTypeName(genraId, index) {
      for(const item of this.genres) {
        if(item.id == genraId) {
          if(this.movie.genre_ids.length - 1 == index){
            return item.name ;
          }else {
            return item.name + ",";
          }
          
        }
      }
    }
  }
}
</script>

<style>

</style>