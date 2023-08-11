<script>
	import TopBar from "./lib/TopBar.svelte";
	import PokemonListDisplay from "./lib/PokemonListDisplay.svelte";
	import PokemonInfoDisplay from "./lib/PokemonInfoDisplay.svelte";
	import { initializePokemonStore } from "@kuinox/pokedex.js";
	let searchText = "";
	let currentPokemon = -1;
	let loading = true;
	let pokeStore;
	function pokemonChoosedCallback(event) {
		currentPokemon = event.detail;
	}
	loadPokeStore();
	async function loadPokeStore() {
		pokeStore = await initializePokemonStore("");
		loading = false;
	}
</script>

<div class="App">
	<TopBar bind:searchText={searchText} />
	{#if !loading}
		<PokemonListDisplay {pokeStore} {searchText} on:pokemonChoosed={pokemonChoosedCallback} />
	{/if}
	{#if currentPokemon != -1}
		<PokemonInfoDisplay
			{pokeStore}
			pokemonId={currentPokemon}
			on:close={() => (currentPokemon = -1)}
		/>
	{/if}
</div>
