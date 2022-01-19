<script>
	import { fade, fly } from "svelte/transition";
	export let name;

	let rando;
	$: result = Math.round(rando * 100) ;
	function setRando(){
		rando = Math.random();
	}
</script>

<main>
	<h1>Hello {name}</h1>
	<h1>{rando}</h1>
	<h1>{result}</h1>
	<button on:click={setRando}>Randomize</button>
	<input bind:value={rando}>

	<p>Your score is {result}</p>
	{#if result > 75}
		<p in:fade>You passed!</p>
	{:else if result < 75}
		<p in:fade>You failed!</p>
	{:else}
		<p in:fade>You didn't take the test!</p>
	{/if}
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
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