<template>
     <article class="article-item" >
        <div class="image-wrap">
          <img
            :src="pelicula.image"
            :alt="pelicula.title"
            :title="pelicula.title"
          />
        </div>
        <h2>{{pelicula.title}}</h2>
        <span 
            class="date" 
            :class="{
                yeargreen: pelicula.year >= 2018,
                yearred: pelicula.year < 2018
            }">
          {{pelicula.year}}
        </span>
        <a href="#">leer mas...</a>
        <input 
          type="button" 
          value="Marcar como favorita" 
          v-on:click="pasarFavoritaAlPadre(pelicula)"
        />
        <div class="clear-fix"></div>
      </article>
</template>

<script>
export default {
    name: 'Pelicula',
    props: ['pelicula'],
    methods: {
      pasarFavoritaAlPadre(pelicula){
        //emito el evento
        this.$emit('favorita', pelicula);
      }
    }
}
</script>