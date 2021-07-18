<template>
  <div class="general">
    <div class="center">
      <section id="content">
        <h1 class="subheader">Crear Arículo</h1>
        <form class="mid-form" v-on:submit.prevent="save()">
          <div class="form-group">
            <label for="title">Título:</label>
            <input type="text" name="title" v-model="article.title" />
            <div v-if="submited && !$v.article.title.required">
              El campo título no puede estar vacío
            </div>
          </div>
          <div class="form-group">
            <label for="content">Contenido:</label>
            <textarea
              type="text"
              name="content"
              v-model="article.content"
            ></textarea>
            <div v-if="submited && !$v.article.content.required">
              El contenido no puede estar vacío
            </div>
          </div>
          <div class="form-group">
            <label for="image">Imagen:</label>
            <input
              type="file"
              id="file"
              ref="file"
              name="file0"
              @change="fileChange()"
            />
          </div>
          <div class="clear-fix"></div>
          <input type="submit" value="Guardar" class="btn btn-success" />
        </form>
      </section>
      <SideBar></SideBar>
      <div class="clear-fix"></div>
    </div>
  </div>
</template>

<script>
import SideBar from "./SideBar.vue";
import Global from "../Global";
import Article from "../models/Article";
import axios from "axios";
import { required } from "vuelidate/lib/validators";

export default {
  name: "CreateArticle",
  components: {
    SideBar,
  },
  data() {
    return {
      url: Global.url,
      file: '',
      article: new Article('', '', null, ''),
      submited: false,
    };
  },
  validations: {
    article: {
      title: {
        required,
      },
      content: {
        required,
      },
    },
  },
  mounted() {},
  methods: {
    fileChange(){
      this.file = this.$refs.file.files[0];
      console.log(this.file);
    },
    save() {
      this.submited = true;
      this.$v.$touch();
      if (this.$v.$invalid) {
        return false;
      } else {
        /*const formData = new FormData();
        formData.append(
          'file0',
          this.file,
          this.file.name
        );*/
        axios
          .post(this.url + "save", this.article)
          .then(response => {
            if (response.data.status == "success") {
              
              //subida de archivo
              if (this.file != null && this.file != 'undefined' && this.file != '') {
                
              }
              const formData = new FormData();
              formData.append(
                'file0',
                this.file,
                this.file.name
              );
              var articleId = response.data.article._id;
              axios.post(this.url + 'upload-image/' + articleId, formData)
                   .then(res => {
                     if (res.data.article) {
                       this.article = res.data.article;
                       this.$router.push("/blog");
                     }else{
                       //Mostrar alerta de error
                     }
                   }).catch(error => {
                     console.log('ERROR: '+error);
                   });
              }
            })
            .catch(error => {
              console.log(error);
            });
      }
    }
  }
}
</script>
