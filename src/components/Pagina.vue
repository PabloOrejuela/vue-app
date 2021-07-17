<template>
 <div class="general">
    <Slider></Slider>
    <div class="center">
  <section id="content">
    <h2 class="subheader">Página de pruebas</h2>
    <h3>{{idUrl}}</h3>
    <button @click="redirigirAlBlog()" >Ir al blog</button>
  </section>
  <SideBar></SideBar>
      <div class="clear-fix"></div>
    </div>
  </div>
</template>

<script>
import Slider from './Slider.vue';
import SideBar from './SideBar.vue';
export default {
  name: "Pagina",
  mounted(){
    this.idUrl = this.$route.params.id;
  },
  data(){
    return{
      idUrl: null
    }
  },
  methods:{
    redirigirAlBlog(){
      this.$router.push('/pagina');
    }
  },
  components: {
    Slider,
    SideBar
  }
};
</script>
