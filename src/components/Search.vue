<template>
  <div class="general">
    <Slider :texto="'Busqueda: ' + searchString"></Slider>
    <div class="center">
      <section id="content">
        <h1 class="subheader" v-if="articles">Artículos encontrados:</h1>
        <h1 class="subheader" v-else>Sin resultados</h1>
        <div id="articles" v-if="articles">
          <Articles :articles="articles"></Articles>
        </div>
        <div v-else><h2>No se han encontrado artículos que coincidan con la búsqueda</h2></div>
      </section>
      <SideBar></SideBar>
      <div class="clear-fix"></div>
    </div>
  </div>
</template>

<script>
import Slider from "./Slider.vue";
import SideBar from "./SideBar.vue";
import axios from "axios";
import Global from '../Global';
import Articles from "./Articles.vue";

export default {
  name: "Search",
  components: {
    Slider,
    SideBar,
    Articles
  },
  mounted() {
      this.searchString = this.$route.params.searchString;
      this.getArticlesBySearch(this.searchString);
  },
  data() {
    return {
      articles: null,
      url: Global.url,
      searchString: null
    };
  },
  methods: {
    getArticlesBySearch(searchString) {
      axios.get(this.url +  "search/" +searchString).then((res) => {
        if (res.data.status === "success") {
          this.articles = res.data.articles;
        }
      });
    },
  }
};
</script>
