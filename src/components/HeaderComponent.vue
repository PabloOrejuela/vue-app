<template>
    <header id="header">
		<div class="center">
			<div id="logo">
				<img src="../assets/images/logo.png" class="app-logo" alt="logotipo" />
				<span id="brand">
					<strong>App </strong>Vue
				</span>
			</div>
			<nav id="menu">
				<ul>
					<li><router-link to="/home" active-class="active">Inicio</router-link></li>
					<li><router-link to="/blog" active-class="active">Blog</router-link></li>
					<li><router-link to="formulario" active-class="active">Formulario</router-link></li>
					<li><router-link to="peliculas" active-class="active">Peliculas</router-link></li>
					<li><router-link to="mi" active-class="active">Mi</router-link></li>
				</ul>
			</nav>
			<!--Limpiar los FLOATS-->
			<div class="clear-fix"></div>
		</div>
	</header>
</template>

<script>

export default {
  name: 'HeaderComponent'
}
</script>
