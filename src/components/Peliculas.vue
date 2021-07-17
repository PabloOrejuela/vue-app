<template>
  <div class="general">
    <div class="center">
      <section id="content">
        <h1 class="subheader">Películas</h1>
        <div class="favorita" v-if="favorita">
          La película favorita es:
          <h3>{{ favorita.title | mayusculas}}</h3>
        </div>
        <!--Listado articulos-->
        <div id="articles">
          <!-- v-for="pelicula in peliculas" v-bind:key="pelicula" -->
          <div v-for="pelicula in peliculasMayusculas" v-bind:key="pelicula.id">
            <Pelicula
              :pelicula="pelicula"
              v-on:favorita="peliculaFavorita"
            ></Pelicula>
          </div>
        </div>
      </section>
      <SideBar></SideBar>
      <div class="clear-fix"></div>
    </div>
  </div>
</template>

<script>
import Pelicula from "./Pelicula.vue";
import SideBar from "./SideBar.vue";
export default {
  name: "Peliculas",
  components: {
    Pelicula,
    SideBar,
  },
  methods: {
    peliculaFavorita(favorita) {
      this.favorita = favorita;
    },
  },
  filters: {
    mayusculas(value){
      return value.toUpperCase();
    }
  },
  computed: {
    peliculasMayusculas(){
      let peliculasMod = this.peliculas;
      for (let i = 0; i < this.peliculas.length; i++) {
        peliculasMod[i].title = peliculasMod[i].title.toUpperCase();
        
      }
      return peliculasMod;
    }
  },
  data() {
    return {
      web: "appdvp.com",
      favorita: null,
      peliculas: [
        {
          id: 1,
          title: "Batman vs Superman",
          year: "2018",
          image:
            "https://i.blogs.es/503736/batman-v-superman-la-pelicula-2016-imagen-blogdecine/1366_2000.jpg",
        },
        {
          id: 2,
          title: "Gran Torino",
          year: "2015",
          image:
            "http://razonesparacreer.com/wp-content/uploads/2017/10/grantorino-708x350@2x.jpg",
        },
        {
          id: 3,
          title: "El señor de los anillos",
          year: "2013",
          image:
            "https://estaticos-cdn.elperiodico.com/clip/ebc2f698-ee0e-43fb-ba47-d9c3fe44982f_alta-libre-aspect-ratio_default_0.jpg",
        },
      ],
    };
  },
};
</script>
