<template>
  <div class="general">
    <div class="center">
      <section id="content">
        <article class="article-item article-detail" v-if="article">
          <div class="image-wrap" v-if="article.image">
            <img
              :src="url + 'get-image/' + article.image"
              :alt="article.title"
            />
          </div>
          <h1 class="subheader">{{ article.title }}</h1>
          <span class="date">
            {{ article.date | moment("from", "now") }}
          </span>
          <p>
            {{ article.content }}
          </p>
          <div class="clear-fix"></div>
        </article>
      </section>
      <SideBar></SideBar>
      <div class="clear-fix"></div>
    </div>
  </div>
</template>

<script>
import SideBar from "./SideBar.vue";
import axios from "axios";
import Global from "../Global";

export default {
  name: "Article",
  components: {
    SideBar,
  },
  data() {
    return {
      url: Global.url,
      article: null,
    };
  },
  mounted() {
    let articleId = this.$route.params.id;
    this.getArticle(articleId);
  },
  methods: {
    getArticle(articleId) {
      axios.get(this.url + "article/" + articleId).then((res) => {
        if (res.data.status === "success") {
          this.article = res.data.article;
        }
      });
    },
  },
};
</script>
