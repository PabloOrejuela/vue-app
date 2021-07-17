<template>
  <div class="general">
    <Slider texto="blog"></Slider>
    <div class="center">
      <section id="content">
        <h1 class="subheader">Blog</h1>
        <div id="articles" v-if="articles">
          <Articles :articles="articles"></Articles>
        </div>
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
  name: "Blog",
  components: {
    Slider,
    SideBar,
    Articles
  },
  mounted() {
    this.getArticles();
  },
  data() {
    return {
      articles: null,
      url: Global.url
    };
  },
  methods: {
    getArticles() {
      axios.get(this.url +  "articles").then((res) => {
        if (res.data.status === "success") {
          this.articles = res.data.articles;
        }
      });
    },
  }
};
</script>
