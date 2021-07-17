<template>
  <div class="general">
    <Slider texto="Ultimos artículos" home="true"></Slider>
    <div class="center">
      <section id="content">
        <h2 class="subheader">Últimos artículos</h2>
        <!--Listado articulos-->
        <div id="articles">
          <Articles v-bind:articles="articles"></Articles>
         
        </div>
      </section>
      <SideBar></SideBar>
      <div class="clear-fix"></div>
    </div>
  </div>
</template>

<script>
import Slider from './Slider.vue';
import SideBar from './SideBar.vue';
import axios from 'axios';
import Global from '../Global';
import Articles from './Articles.vue';


export default {
  name: "LastArticles",
  components: {
    Slider,
    SideBar,
    Articles
  },
  mounted() {
    this.getLastArticles();
  },
  data() {
    return {
      articles: null,
      url: Global.url
    };
  },
  methods: {
    getLastArticles() {
      axios.get(this.url +  "articles/true").then((res) => {
        if (res.data.status === "success") {
          this.articles = res.data.articles;
        }
      });
    },
  }
};
</script>
