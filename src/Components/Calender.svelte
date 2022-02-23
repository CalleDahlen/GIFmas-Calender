<script>
	import CalenderDoor from './CalenderDoor.svelte';
	export let daysOfChristmas;
</script>

<div id="container">
	<!-- render the Calenderdoors -->
	{#each Array(daysOfChristmas) as day, i}
		<CalenderDoor doorNumber={i + 1} />
	{/each}
</div>

<style>
	#container {
		display: grid;
		grid-template-columns: repeat(4, 1fr);
		margin: 1em;
	}
</style>
