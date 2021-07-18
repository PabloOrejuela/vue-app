<template src="../vistas/article.html"></template>

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
    }
  }
};
</script>
