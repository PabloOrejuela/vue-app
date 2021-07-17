<template>
    <section id="content">
        <h2 class="sub-header">{{titulo}}</h2>
        <hr />
        <h1>Este es mi componente</h1>
        <h2> {{subtitulo}} </h2>
        <hr />

        <h2>Reactividad</h2>
        <input type="text" v-model="nombre" />

        {{nombre}}

        <hr />
        <h2>Directivas condicionales</h2>
        <input type="number" v-model="edad" />
        <h4>Mi edad es: <strong> {{edad}} </strong></h4>
        <p class="alert-danger-provisional" v-if="edad && edad >= 18">
            Eres mayor de edad
        </p>
        <p class="alert-success-provisional" v-else>
            Eres menor de edad
        </p>

        <hr />
        <h2>Directiva Iterativa</h2>
        <ol>
            <li v-for="pelicula in peliculas" :key="pelicula"> {{pelicula}} </li>
        </ol>
    </section>
</template>

<script>
export default {
    name: 'MiComponente',
    data() {
        return{
            titulo: 'Mi componente',
            subtitulo: 'Soy un subtitulo',
            nombre: "",
            edad: 18,
            peliculas: ['Batman', 'Rambo', 'Sharknado', 'Spiderman']
        }
    }
    
}
</script>