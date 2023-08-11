<script>
	export let searchText;
</script>

<div class='topBar'>
	<header>
		<nav>
			<span>Kuinox's Pokedex</span>
			<input
				type="text"
				bind:value={searchText}
				placeholder="Search…"
				aria-label='search'
			/>
			<div id="frameDropped"></div>
		</nav>
	</header>
</div>