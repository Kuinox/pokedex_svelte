<script>
	import SearchResult from "./SearchResult.svelte";
	import { createEventDispatcher } from 'svelte';
	const dispatch = createEventDispatcher();
	export let pokeStore;
	export let searchText;
	const pokemons = pokeStore.getPokemonsWithId();
	function onClick(event) {
		dispatch('pokemonChoosed', event.detail);
	}
</script>

<ul class="pokeListUl">
	<div class="pokeList">
		{#each pokemons as p (p.id)}
			<SearchResult
				hidden={p.name.match(new RegExp(".*" + searchText + ".*"))}
				pokemonId={p.id}
				pokemonName={p.name}
				color={p.color}
				generations={p.generations}
				on:pokemonClick={onClick}
				types={p.types}
			/>

		{/each}
	</div>
</ul>
