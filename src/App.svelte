<script>
	import CombatReport from "./CombatReports/CombatReport.svelte";
	import ZeroTwo from "./ZeroTwo/ZeroTwo.svelte";
	import NeuralUpgrade from "./NeuralUpgrade.svelte";

	let menu = "combat-report";
</script>

<main>
	<nav>
		<button class="menu" on:click="{() => { menu = "combat-report" }}" class:selected={menu == "combat-report"}>Combat reports</button>
		<button class="menu" on:click="{() => { menu = "0-2 runs" }}" class:selected={menu == "0-2 runs"}>0-2 runs</button>
		<button class="menu" on:click="{() => { menu = "neural-upgrade" }}" class:selected={menu == "neural-upgrade"}>Neural upgrade</button>
	</nav>

	{#if menu == "combat-report"}
		<CombatReport />
	{:else if menu == "0-2 runs"}
		<ZeroTwo />
	{:else if menu == "neural-upgrade"}
		<NeuralUpgrade />
	{/if}
</main>

<style>
	main {
		text-align: center;
		max-width: 240px;
		margin: 0 auto;
		font-size: 1.1rem;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 3.5em;
		font-weight: 100;
		margin-top: 1.5rem;
		margin-bottom: 1.5rem;
	}

	.selected {
		background-color: #ff3e00;
		color: white;
	}

	nav {
		height: 3rem;
	}

	button:hover {
		background-color: #ff3e00;
		color: white;
		cursor: pointer;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>