<script>
	import {fade} from "svelte/transition";
	import {randomStore} from "./store";


	import Child from "./Child.svelte"


	let data = {
		userId: 12345,
		name: 'Solomon',
		email: 'Solomon.Pierce@utdallas.edu'
	}

	export let name;

	let randos = [];
	
	function setRando(){
		const rando = Math.random();
		randos = [...randos, rando];
	}

	function delay(ms){
		return new Promise(resolve => setTimeout(resolve, ms));
	}

	let rando = delay(2000).then(v => Math.random());

</script>

<main>
	<h1>Hello {name}</h1>
	<button on:click={setRando}>Push</button>
	<ul>
		{#each randos as val, idx}
			<li in:fade>{val}</li>
		{/each}
	</ul>

	{#await rando}
		<p>thinking about it...</p>
	{:then number}
		<p> Result {number}</p>
	{:catch error}
		<p> {error.message}</p>
	{/await}

	{$randomStore}
	<button on:click={() => randomStore.set(Math.random())}></button>

	<Child {...data}></Child>
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