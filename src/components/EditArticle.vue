<template src="../vistas/createArticle.html"></template>
<script>
import SideBar from "./SideBar.vue";
import Global from "../Global";
import Article from "../models/Article";
import axios from "axios";
import { required } from "vuelidate/lib/validators";
import swal from 'sweetalert';

export default {
  name: "EditArticle",
  components: {
    SideBar
  },
  data() {
    return {
      url: Global.url,
      file: "",
      article: new Article("", "", null, ""),
      submited: false,
      isEdit : true
    };
  },
  validations: {
    article: {
      title: {
        required
      },
      content: {
        required
      }
    }
  },
  mounted() {
      var articleId = this.$route.params.id;
      this.getArticle(articleId);
  },
  methods: {
    fileChange(){
      this.file = this.$refs.file.files[0];
      //console.log(this.file);
    },
    getArticle(articleId) {
      axios.get(this.url + "article/" + articleId).then(res => {
        if (res.data.status == "success") {
          this.article = res.data.article;
        }
      });
    },
    save() {
      this.submited = true;

      this.$v.$touch();
      if (this.$v.$invalid) {
        return false;
      } else {

        axios
          .post(this.url + "save", this.article)
          .then(response => {
            if (response.data.status == "success") {
              
              //subida de archivo
              if (
                this.file != null && 
                this.file != 'undefined' && 
                this.file != ""
              ) {


              const formData = new FormData();
              formData.append(
                "file0",
                this.file,
                this.file.name
              );
              var articleId = response.data.article._id;

              axios.post(this.url + "upload-image/" + articleId, formData)
                   .then(response => {
                     if (response.data.article) {
                       swal(
                        'Artículo creado' ,
                        'El artículo se ha creado correctamente',
                        'success'
                       );
                       this.article = response.data.article;
                       this.$router.push("/blog");
                     }else{
                       swal(
                        'Artículo no se a creado bien' ,
                        'Ha habido un error en la creación del artículo',
                        'error'
                       );
                     }
                   }).catch(error => {
                     console.log('ERROR: '+error);
                   });
                }else{

                  swal(
                    'Artículo creado' ,
                    'El artículo se ha creado correctamente 2',
                    'success'
                  );
                  this.article = response.data.article;
                  this.$router.push("/blog");
                }
              }
            })
            .catch(error => {
              console.log(error);
            });
      }
    }
  }
};
</script>
