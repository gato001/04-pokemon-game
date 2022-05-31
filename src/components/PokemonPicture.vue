<template>
	<div class="pokemon-container">
		<img class="hidden-pokemon" v-bind:src="imagSrc" alt="pokemon" />
		<img
			v-if="showPokemon"
			class="fade-in"
			v-bind:src="imagSrc"
			alt="pokemon"
		/>
	</div>
</template>

<script>
	export default {
		props: {
			pokemonId: {
				required: true,
				type: Number,
			},
			showPokemon: {
				type: Boolean,
				required: true,
				default: false,
			},
		},
		computed: {
			imagSrc: function () {
				return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.pokemonId}.svg`;
			},
		},
	};
</script>

<style scoped>
	.pokemon-container {
		height: 200px;
	}
	img {
		height: 200px;
		position: absolute;
		right: 32%;
		user-select: none;
		-moz-user-select: none;
		-ms-user-select: none;
		-webkit-user-drag: none;
		-webkit-user-select: none;
	}
	.hidden-pokemon {
		filter: brightness(0);
	}
</style>
