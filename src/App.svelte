<script>
	import Tdoll from "./Tdoll.svelte";
	import Hoc from "./Hoc.svelte";
	let display = "t-doll";
</script>

<main>
	<h1>Combat report calculator</h1>

	<button on:click="{() => { display = "t-doll"}}">T-dolls</button>
	<button on:click="{() => { display = "hoc"}}">HOCs</button>

	{#if display == "t-doll"}
		<Tdoll />
	{:else if display == "hoc"}
		<Hoc />
	{/if}
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
		font-size: 1.1rem;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>