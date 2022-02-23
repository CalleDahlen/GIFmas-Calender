<script>
	import Navbar from '../Components/Navbar.svelte';
</script>

<body>
	<Navbar />
	<slot />
</body>

<style>
	body {
		background-color: #211f1f;
		min-height: 100%;
	}
</style>
