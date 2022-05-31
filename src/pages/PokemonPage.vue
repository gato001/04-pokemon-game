<template>
	<div>
		<h1 v-if="!pokemon">Espere por favor ...</h1>

		<div v-else>
			<h1>Quien es este Pokemon?</h1>
			<pokemon-picture
				v-bind:pokemon-id="pokemon.id"
				v-bind:show-pokemon="showPokemon"
			></pokemon-picture>
			<pokemon-options
				v-bind:pokemons="pokemonArr"
				v-on:selection="checkAnswer"
			></pokemon-options>

			<template v-if="showAnswers">
				<h2>{{ message }}</h2>

				<button v-on:click="newGame">nuevo juego</button>
			</template>
		</div>
	</div>
</template>

<script>
	import PokemonOptions from '../components/PokemonOptions.vue';
	import PokemonPicture from '../components/PokemonPicture.vue';
	import getPokemonOptions from '../helpers/getPokemonsOptions';

	export default {
		components: { PokemonPicture, PokemonOptions },
		data() {
			return {
				pokemonArr: [],
				pokemon: null,
				showPokemon: false,
				showAnswers: false,
				message: '',
			};
		},
		methods: {
			mixPokemonArrays: async function () {
				this.pokemonArr = await getPokemonOptions();

				const rdnInt = Math.floor(Math.random() * 4);
				this.pokemon = this.pokemonArr[rdnInt];
			},

			checkAnswer: function (selectedId) {
				this.showPokemon = !this.showPokemon;

				if (selectedId === this.pokemon.id) {
					this.message = `Correcto, ${this.pokemon.name} `;
				} else {
					this.message = `Opps, era  ${this.pokemon.name}`;
				}

				this.showAnswers = true;
			},

			newGame: function () {
				this.showPokemon = !this.showPokemon;
				this.showAnswers = false;
				this.pokemonArr = [];
				this.pokemon = null;
				this.mixPokemonArrays();
			},
		},
		mounted() {
			this.mixPokemonArrays();
		},
	};
</script>
