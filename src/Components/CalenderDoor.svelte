<script>
	import { fade, blur } from 'svelte/transition';
	const APIKEY = import.meta.env.VITE_API_KEY;
	let date = new Date();
	let today = date.getDate();
	let month = date.getMonth();
	let december = 11;
	let src;
	let altText;
	let show = false;
	let clicked = false;
	let url = `https://api.giphy.com/v1/gifs/random?api_key=${APIKEY}&rating=G&tag=christmas`;

	export async function fetchGif() {
		//Check to see if todays date is larger or equal to the door number. Also check wheather the door has been clicked previously. Should only generate new GIF the first time the door is opened.
		if (today >= doorNumber && month == december && !clicked) {
			const response = await fetch(url);
			const gif = await response.json();
			src = gif.data.images.original.url;
			altText = gif.data.title;
			show = !show;
			clicked = true;
			//set show status to opposite of current status to hide or show fetched GIF.
		} else if (today >= doorNumber && month == december && clicked) show = !show;
	}

	export let doorNumber;
</script>

<div class={show ? 'door showing' : 'door'} on:click={fetchGif}>
	<!-- show image if conditions are met -->
	{#if show}
		<img id={doorNumber} in:blur={{ delay: 250, duration: 300 }} {src} alt={altText} />
	{:else}
		<!-- If the image is not be be shown, render the door number -->
		<p in:blur={{ duration: 400 }}>{doorNumber}</p>
	{/if}
</div>

<style>
	.door {
		display: inline-block;
		text-align: center;
		margin: 0.5rem;
		font-size: 2em;
		color: rgb(194, 14, 14);
		border: 6px solid rgb(194, 14, 14);
		border-radius: 10px;
		overflow: hidden;
		cursor: pointer;
		box-shadow: 1px 1px 5px rgb(250, 242, 242);
		font-family: 'Roboto Mono', monospace;
	}
	.door:hover {
		box-shadow: 3px 3px 10px rgb(250, 242, 242);
		color: rgb(250, 242, 242);
	}
	.showing img {
		position: absolute;
		margin: auto;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		min-width: 50%;
		min-height: 50%;
		max-height: 97%;
	}
	.showing {
		position: fixed;
		width: 95%;
		height: 79%;
		margin: 0.35em;
		background-color: rgba(33, 31, 31, 0.9);
		z-index: 2;
		cursor: pointer;
		text-align: center;
		border: 4px solid rgb(32, 220, 15);
	}
</style>
