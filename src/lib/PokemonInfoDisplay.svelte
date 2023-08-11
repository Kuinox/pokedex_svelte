<script>
    import { createEventDispatcher } from 'svelte';
    export let pokeStore;
    export let pokemonId;
    console.log(pokemonId);
    const dispatch = createEventDispatcher();
    let stats = pokeStore.getStatsWithId(pokemonId);
    let color = pokeStore.getPokemonColor(pokemonId);
    let imgSrc = "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/" + pokemonId + ".png";
    const handleClickOutside = (e) => {
        if (e.target === e.currentTarget) {
            dispatch('close');
        }
    }
</script>
<div class="modal" on:click={handleClickOutside}>
    <div class={`modal-content ${color}`}>
        <span class="close" on:click={() => dispatchEvent('close')}>&times;</span>
        <h3>Pokemon Stats</h3>
        <img src={imgSrc} alt="Pokemon sprite" />
        <ul>
            {#each stats as stat, i}
                <li key={i}>
                    {stat.statsName}: {stat.value}
                </li>
            {/each}
        </ul>
    </div>
</div>