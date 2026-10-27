<script setup="">
	import MaterialCatalog from './components/MaterialCatalog.vue'
</script>

<template>
	<div class="app">
		<header class="app__header">
			<h1>Каталог навчальних матеріалів</h1>
			<p>Ткачик Т. А. | Група Ф2-253 | Vue 3 + Vite</p>
		</header>

		<main class="app__main">
			<MaterialCatalog />
		</main>
	</div>
</template>