<script>
	import Calender from '../Components/Calender.svelte';
	const daysOfChristmas = 24;
</script>

<svelte:head>
	<title>GIFmas Calender</title>
</svelte:head>

<!-- Make a foreach day in days of christmas that renders a <CalendarDoor {day} /> -->

<Calender {daysOfChristmas} />
