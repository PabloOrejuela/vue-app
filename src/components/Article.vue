<template src="../vistas/article.html"></template>

<script>
import SideBar from "./SideBar.vue";
import axios from "axios";
import Global from "../Global";
import swal from "sweetalert";

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
    deleteArticle(articleId) {
      swal({
        title: "¿Esta seguro de querer borrar el artículo?",
        text:
          "Una vez borrado no podrá ser recuperado!",
        icon: "warning",
        buttons: true,
        dangerMode: true,
      }).then((willDelete) => {
        if (willDelete) {
          axios.delete(this.url + "article/" + articleId).then((response) => {
            swal(
              "Artículo borrado",
              "El artículo se ha borrado correctamente",
              "success"
            );
            this.$router.push("/blog");
          });
        } else {
          swal("Tu artículo NO ha sido borrado!");
        }
      });
    },
  },
};
</script>
