<template>
  <div class="general">
    <div class="center">
      <section id="content">
        <h2 class="subheader">Formulario</h2>
        <form action="" class="mid-form" v-on:submit.prevent="mostrarUsuario">
          <div class="form-group">
            <label for="nombre">Nombre</label>
            <input type="text" name="nombre" v-model="user.nombre" />
            <div v-if="submited && !$v.user.nombre.required">Este campo es requerido</div>
            <div v-if="submited &&  !$v.user.nombre.minLength">Este campo debe tener mas caracteres</div>
          </div>
          <div class="form-group">
            <label for="apellidos">Apellidos</label>
            <input type="text" name="apellidos" v-model="user.apellidos" />
            <div v-if="submited &&  !$v.user.apellidos.required">Este campo es requerido</div>
            <div v-if="submited &&  !$v.user.apellidos.minLength">Este campo debe tener mas caracteres</div>
          </div>
          <div class="form-group">
            <label for="bio">Biografía</label>
            <textarea name="bio" v-model="user.bio"></textarea>
            <div v-if="submited &&  !$v.user.bio.required">Este campo es requerido</div>
            <div v-if="submited &&  !$v.user.bio.minLength">Este campo debe tener mas caracteres</div>
          </div>
          <div class="form-group radio-buttons">
            <input
              type="radio"
              name="genero"
              value="hombre"
              v-model="user.genero"
              checked
            />Hombre
            <input
              type="radio"
              name="genero"
              value="mujer"
              v-model="user.genero"
            />Mujer
            <input
              type="radio"
              name="genero"
              value="otro"
              v-model="user.genero"
            />Otro
          </div>
          <br />
          <input type="submit" value="enviar" class="btn btn-success" />
        </form>
      </section>
      <SideBar></SideBar>
      <div class="clear-fix"></div>
    </div>
  </div>
</template>

<script>
import SideBar from "./SideBar.vue";
import { required, minLength } from "vuelidate/lib/validators";
export default {
  name: "Formulario",
  components: {
    SideBar,
  },
  validations: {
    user: {
      nombre: {
        required,
        minLength: minLength(5),
      },
      apellidos: {
        required,
        minLength: minLength(5),
      },
      bio: {
        required,
        minLength: minLength(10),
      },
    },
  },
  data() {
    return {
      submited: false,
      user: {
        nombre: "",
        apellidos: "",
        bio: "",
        genero: "",
      },
    };
  },
  methods: {
    mostrarUsuario() {
      this.submited = true;
      this.$v.$touch();
      if (this.$v.$invalid) {
        return false;
      }
      alert("Pasa");
    },
  },
};
</script>
